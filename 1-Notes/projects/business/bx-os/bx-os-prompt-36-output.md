Step 1: Requirements Analysis
We need a lean schema that (1) captures incidents → student reflections → teacher review/approval, (2) powers a kiosk-only flow (no student logins), (3) enforces least-privilege access (teachers see only their students), and (4) supports admin views (live kiosk status, trends, exports) with auditable history. Concurrency-safe queue/assignment logic is required to fix ‘Clear Queue’ race conditions.

Step 2: Entity Relationship Design
Core Entities
Entity: profiles (teachers/admins)
• Purpose: Local profile for auth.users (Supabase) with role metadata.
• Key attributes: id (uuid, PK → auth.users.id), full_name, role ENUM(‘teacher’,‘admin’).
• Relationships: 1–n incidents (by teacher_id), m–n students via teacher_students.
• Volume: 30–60.

Entity: students
• Purpose: Directory of students (no login).
• Key attributes: id (uuid), external_id (SIS ID), full_name, grade, homeroom.
• Relationships: 1–n incidents, m–n profiles via teacher_students.
• Volume: 300–800.

Entity: incidents
• Purpose: The behavior report/record.
• Key attributes: id, teacher_id, student_id, category_id, summary, status ENUM(‘open’,‘assigned’,‘reflecting’,‘submitted’,‘approved’,‘revision_requested’,‘archived’), current_kiosk_id?, timestamps.
• Relationships: 1–1 reflections, 1–n incident_events, 1–n kiosk_assignments, n–1 categories.
• Volume: 100–300/mo (~3k/yr).

Entity: reflections
• Purpose: Student’s 4-Q reflection attached to one incident.
• Key attributes: incident_id (PK/FK), Q1–Q4 text, status ENUM(‘draft’,‘submitted’,‘approved’,‘revision_requested’), submitted_at, approved_by.
• Relationships: 1–1 with incidents, n–1 profiles (approver).
• Volume: ~= incidents.

Entity: kiosks
• Purpose: Physical/specific kiosk devices.
• Key attributes: id, name, location, device_token_hash, is_active, last_seen_at.
• Relationships: 1–n kiosk_assignments.
• Volume: 2–5.

Entity: kiosk_assignments
• Purpose: Concurrency-safe mapping of an incident to a kiosk session.
• Key attributes: id, incident_id, kiosk_id, assigned_at, released_at NULLABLE.
• Relationships: n–1 incidents, n–1 kiosks.
• Volume: ≈ incidents (some retries).

Entity: categories
• Purpose: Controlled vocabulary for incident type.
• Key attributes: id, name, is_active.
• Relationships: 1–n incidents.
• Volume: 10–25.

Entity: incident_events (history/audit)
• Purpose: Append-only event log (status changes, approvals, assignments).
• Key attributes: id, incident_id, event_type, meta JSONB, created_at, actor_id?.
• Relationships: n–1 incidents, n–1 profiles.
• Volume: ~2–6 per incident.

Entity: teacher_students (visibility map)
• Purpose: Which students a teacher may view.
• Key attributes: teacher_id, student_id (composite PK).
• Relationships: m–n between profiles and students.
• Volume: (#teachers × avg roster).

Relationship Map
auth.users (1) ---- (1) profiles
profiles (1) ----< (n) incidents
students (1) ----< (n) incidents
incidents (1) ---- (1) reflections
incidents (1) ----< (n) incident_events
incidents (1) ----< (n) kiosk_assignments
kiosks (1) ----< (n) kiosk_assignments
categories (1) ----< (n) incidents
profiles (n) ----< (m) teacher_students >---- (n) students

Step 3: Detailed Table Specifications
Assumes pgcrypto for gen_random_uuid() and UTC timestamptz.

```sql
-- ENUMs
CREATE TYPE role_enum AS ENUM ('teacher','admin');
CREATE TYPE incident_status_enum AS ENUM
  ('open','assigned','reflecting','submitted','approved','revision_requested','archived');
CREATE TYPE reflection_status_enum AS ENUM
  ('draft','submitted','approved','revision_requested');

-- profiles (mirror of auth.users with role)
CREATE TABLE profiles (
  id uuid PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
  full_name text NOT NULL,
  role role_enum NOT NULL DEFAULT 'teacher',
  created_at timestamptz NOT NULL DEFAULT now()
);

-- students
CREATE TABLE students (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  external_id text UNIQUE,
  full_name text NOT NULL,
  grade text,
  homeroom text,
  created_at timestamptz NOT NULL DEFAULT now()
);

-- teacher_students (visibility)
CREATE TABLE teacher_students (
  teacher_id uuid NOT NULL REFERENCES profiles(id) ON DELETE CASCADE,
  student_id uuid NOT NULL REFERENCES students(id) ON DELETE CASCADE,
  PRIMARY KEY (teacher_id, student_id)
);

-- categories
CREATE TABLE categories (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  name text UNIQUE NOT NULL,
  is_active boolean NOT NULL DEFAULT true
);

-- kiosks
CREATE TABLE kiosks (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  name text NOT NULL,
  location text,
  device_token_hash text UNIQUE NOT NULL,   -- store a hash, not the token
  is_active boolean NOT NULL DEFAULT true,
  last_seen_at timestamptz
);

-- incidents
CREATE TABLE incidents (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  teacher_id uuid NOT NULL REFERENCES profiles(id),
  student_id uuid NOT NULL REFERENCES students(id),
  category_id uuid REFERENCES categories(id),
  summary text,                    -- brief teacher-entered description
  status incident_status_enum NOT NULL DEFAULT 'open',
  current_kiosk_id uuid REFERENCES kiosks(id), -- nullable; for fast joins
  created_at timestamptz NOT NULL DEFAULT now(),
  updated_at timestamptz NOT NULL DEFAULT now()
);

-- reflections (1-1 with incidents)
CREATE TABLE reflections (
  incident_id uuid PRIMARY KEY REFERENCES incidents(id) ON DELETE CASCADE,
  q1 text, q2 text, q3 text, q4 text,
  status reflection_status_enum NOT NULL DEFAULT 'draft',
  submitted_at timestamptz,
  approved_by uuid REFERENCES profiles(id),
  approved_at timestamptz,
  updated_at timestamptz NOT NULL DEFAULT now()
);

-- kiosk_assignments
CREATE TABLE kiosk_assignments (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  incident_id uuid NOT NULL REFERENCES incidents(id) ON DELETE CASCADE,
  kiosk_id uuid NOT NULL REFERENCES kiosks(id) ON DELETE CASCADE,
  assigned_at timestamptz NOT NULL DEFAULT now(),
  released_at timestamptz
);

-- incident_events (append-only audit)
CREATE TABLE incident_events (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  incident_id uuid NOT NULL REFERENCES incidents(id) ON DELETE CASCADE,
  event_type text NOT NULL,            -- e.g., 'status_change','assigned','submitted','approved'
  actor_id uuid REFERENCES profiles(id),
  meta jsonb NOT NULL DEFAULT '{}',
  created_at timestamptz NOT NULL DEFAULT now()
);

-- updated_at trigger (incidents, reflections)
CREATE OR REPLACE FUNCTION touch_updated_at() RETURNS trigger AS $$
BEGIN
  NEW.updated_at = now();
  RETURN NEW;
END$$ LANGUAGE plpgsql;

CREATE TRIGGER tr_incidents_touch
BEFORE UPDATE ON incidents
FOR EACH ROW EXECUTE FUNCTION touch_updated_at();

CREATE TRIGGER tr_reflections_touch
BEFORE UPDATE ON reflections
FOR EACH ROW EXECUTE FUNCTION touch_updated_at();
```

Queue/Assignment RPCs (fixes ‘Clear Queue’ race)
Use FOR UPDATE SKIP LOCKED to assign atomically.

```sql
-- Next-incident assignment to a kiosk (atomic)
CREATE OR REPLACE FUNCTION rpc_assign_next_incident(_kiosk_id uuid)
RETURNS TABLE(incident_id uuid) AS $$
DECLARE
  _iid uuid;
BEGIN
  -- Claim one OPEN incident not already assigned
  SELECT i.id
  INTO _iid
  FROM incidents i
  LEFT JOIN kiosk_assignments ka
    ON ka.incident_id = i.id AND ka.released_at IS NULL
  WHERE i.status = 'open'
    AND ka.id IS NULL
  ORDER BY i.created_at
  FOR UPDATE SKIP LOCKED
  LIMIT 1;

  IF _iid IS NULL THEN
    RETURN; -- no work
  END IF;

  INSERT INTO kiosk_assignments (incident_id, kiosk_id) VALUES (_iid, _kiosk_id);
  UPDATE incidents SET status = 'assigned', current_kiosk_id = _kiosk_id WHERE id = _iid;

  INSERT INTO incident_events (incident_id, event_type, meta)
  VALUES (_iid, 'assigned', jsonb_build_object('kiosk_id', _kiosk_id));

  RETURN QUERY SELECT _iid;
END
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Release assignment when reflection submitted/abandoned
CREATE OR REPLACE FUNCTION rpc_release_assignment(_incident_id uuid)
RETURNS void AS $$
BEGIN
  UPDATE kiosk_assignments
  SET released_at = now()
  WHERE incident_id = _incident_id AND released_at IS NULL;

  UPDATE incidents SET current_kiosk_id = NULL WHERE id = _incident_id;
END
$$ LANGUAGE plpgsql SECURITY DEFINER;
```

Reflection submit/approve flow

```sql
-- Student submits reflection (kiosk)
CREATE OR REPLACE FUNCTION rpc_submit_reflection(_incident_id uuid, _q1 text,_q2 text,_q3 text,_q4 text)
RETURNS void AS $$
BEGIN
  INSERT INTO reflections (incident_id, q1,q2,q3,q4, status, submitted_at)
  VALUES (_incident_id, _q1,_q2,_q3,_q4, 'submitted', now())
  ON CONFLICT (incident_id)
  DO UPDATE SET q1 = EXCLUDED.q1, q2 = EXCLUDED.q2, q3 = EXCLUDED.q3, q4 = EXCLUDED.q4,
                status = 'submitted', submitted_at = now();

  UPDATE incidents SET status = 'submitted' WHERE id = _incident_id;

  INSERT INTO incident_events (incident_id, event_type) VALUES (_incident_id, 'submitted');

  PERFORM rpc_release_assignment(_incident_id);
END
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Teacher approves
CREATE OR REPLACE FUNCTION rpc_approve_reflection(_incident_id uuid, _approver uuid)
RETURNS void AS $$
BEGIN
  UPDATE reflections
  SET status = 'approved', approved_by = _approver, approved_at = now()
  WHERE incident_id = _incident_id;

  UPDATE incidents SET status = 'approved' WHERE id = _incident_id;

  INSERT INTO incident_events (incident_id, event_type, actor_id)
  VALUES (_incident_id, 'approved', _approver);
END
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Auto-archive on approval (nightly or immediate)
CREATE OR REPLACE FUNCTION rpc_archive_incident(_incident_id uuid)
RETURNS void AS $$
BEGIN
  UPDATE incidents SET status = 'archived' WHERE id = _incident_id;
  INSERT INTO incident_events (incident_id, event_type) VALUES (_incident_id, 'archived');
END
$$ LANGUAGE plpgsql SECURITY DEFINER;
```

Step 4: Performance Optimizations
• Indexes
  ◦ incidents(teacher_id, status, created_at DESC)
  ◦ incidents(student_id, status)
  ◦ reflections(incident_id) (PK already)
  ◦ kiosk_assignments(incident_id) and partial:
    ```sql
    CREATE UNIQUE INDEX ux_kiosk_open ON kiosk_assignments(kiosk_id) WHERE released_at IS NULL;
    CREATE UNIQUE INDEX ux_incident_open_assignment ON kiosk_assignments(incident_id) WHERE released_at IS NULL;
    ```
  ◦ incident_events(incident_id, created_at)
• Partial indexes for fast dashboards:
  ```sql
  CREATE INDEX ix_incidents_open ON incidents(id) WHERE status IN ('open','assigned','reflecting','submitted');
  ```
• Denormalization for kiosk speed: snapshot student_name and teacher_name on incidents (optional), maintained via triggers.
• History growth: keep incident_events only (no heavy copies). If volume grows (>100k), partition incident_events by month.

Step 5: Data Integrity Rules
• FKs: All relationships enforce referential integrity as defined.
• Checks:
  ◦ Status fields constrained by ENUMs.
  ◦ Prevent multiple active assignments via the partial unique indexes above.
  ◦ Optional: one active incident per student:
    ```sql
    CREATE UNIQUE INDEX ux_student_active_incident
      ON incidents(student_id)
      WHERE status IN ('open','assigned','reflecting','submitted','revision_requested');
    ```
• Idempotency: rpc_submit_reflection uses UPSERT; assignment uses SKIP LOCKED to avoid double-claims.
• Auditability: Every status/assignment change writes to incident_events.

Step 6: Migration and Scaling Plan
• Order:
  1. Enable pgcrypto; create ENUMs.
  2. Create base tables: profiles, students, categories, kiosks.
  3. Create incidents, reflections, kiosk_assignments, incident_events.
  4. Add indexes & partial unique indexes.
  5. Create RPC functions & triggers.
  6. Seed categories; insert profiles; load students.
  7. Enable RLS & policies (below).
• Version control: Store SQL migrations; one migration per step; avoid destructive changes.
• Zero-downtime: Add columns as nullable, backfill, then add NOT NULL; create indexes CONCURRENTLY; add constraints with NOT VALID → VALIDATE CONSTRAINT.

RLS Policies (Supabase)
Pattern: teachers/admins authenticated; kiosks use short-lived JWT with role: "kiosk" and kiosk_id claim (issued by an Edge Function).

```sql
-- Enable RLS
ALTER TABLE profiles ENABLE ROW LEVEL SECURITY;
ALTER TABLE students ENABLE ROW LEVEL SECURITY;
ALTER TABLE teacher_students ENABLE ROW LEVEL SECURITY;
ALTER TABLE incidents ENABLE ROW LEVEL SECURITY;
ALTER TABLE reflections ENABLE ROW LEVEL SECURITY;
ALTER TABLE kiosk_assignments ENABLE ROW LEVEL SECURITY;
ALTER TABLE kiosks ENABLE ROW LEVEL SECURITY;
ALTER TABLE incident_events ENABLE ROW LEVEL SECURITY;

-- Helpers
CREATE OR REPLACE FUNCTION is_admin() RETURNS boolean
LANGUAGE sql STABLE AS $$ SELECT coalesce((auth.jwt()->>'role') = 'admin', false) $$;

CREATE OR REPLACE FUNCTION is_teacher(uid uuid) RETURNS boolean
LANGUAGE sql STABLE AS $$ SELECT EXISTS (SELECT 1 FROM profiles p WHERE p.id = uid AND p.role = 'teacher') $$;

-- profiles
CREATE POLICY "read own profile" ON profiles
FOR SELECT USING (id = auth.uid() OR is_admin());

-- students: teacher can see students in their map; admin all
CREATE POLICY "teacher sees mapped students" ON students
FOR SELECT USING (
  is_admin() OR EXISTS (
    SELECT 1 FROM teacher_students ts WHERE ts.teacher_id = auth.uid() AND ts.student_id = id
  )
);

-- teacher_students
CREATE POLICY "teacher reads own map" ON teacher_students
FOR SELECT USING (teacher_id = auth.uid() OR is_admin());

-- incidents: teacher sees own students; admin sees all
CREATE POLICY "select incidents by visibility" ON incidents
FOR SELECT USING (
  is_admin() OR EXISTS (
    SELECT 1 FROM teacher_students ts WHERE ts.teacher_id = auth.uid() AND ts.student_id = incidents.student_id
  )
);

-- Teacher may INSERT incidents for visible students
CREATE POLICY "teacher inserts incidents" ON incidents
FOR INSERT WITH CHECK (
  is_admin() OR EXISTS (
    SELECT 1 FROM teacher_students ts WHERE ts.teacher_id = auth.uid() AND ts.student_id = student_id
  )
);

-- Reflections: teachers/admin read if they can read incident
CREATE POLICY "read reflections via incident" ON reflections
FOR SELECT USING (
  is_admin() OR EXISTS (
    SELECT 1 FROM incidents i
    JOIN teacher_students ts ON ts.student_id = i.student_id AND ts.teacher_id = auth.uid()
    WHERE i.id = reflections.incident_id
  )
);

-- Kiosk access: allow INSERT/UPDATE via RPC (SECURITY DEFINER) only; SELECT limited by kiosk claim
CREATE POLICY "kiosk reads own assignments" ON kiosk_assignments
FOR SELECT USING (
  is_admin() OR (auth.jwt()->>'role' = 'kiosk' AND kiosk_id::text = auth.jwt()->>'kiosk_id')
);

-- Kiosks table read for admin only (or minimal fields)
CREATE POLICY "admin reads kiosks" ON kiosks
FOR SELECT USING (is_admin());

-- Events: readable if incident visible
CREATE POLICY "read events via incident" ON incident_events
FOR SELECT USING (
  is_admin() OR EXISTS (
    SELECT 1 FROM incidents i
    JOIN teacher_students ts ON ts.student_id = i.student_id AND ts.teacher_id = auth.uid()
    WHERE i.id = incident_events.incident_id
  )
);
```

Kiosk writes happen through SECURITY DEFINER RPCs above, so you don’t need broad INSERT rights for the kiosk JWT.

Step 7: Sample Queries (with perf notes)

```sql
-- Teacher dashboard: my open incidents (index: incidents(teacher_id,status,created_at))
SELECT id, student_id, category_id, summary, status, created_at
FROM incidents
WHERE teacher_id = $1 AND status IN ('open','assigned','reflecting','submitted')
ORDER BY created_at DESC
LIMIT 50;

-- Get reflection for an incident (PK lookup, ~O(1))
SELECT * FROM reflections WHERE incident_id = $1;

-- Admin: live kiosk status (requires admin role)
SELECT k.id, k.name, k.location, k.is_active, k.last_seen_at,
       (SELECT count(*) FROM kiosk_assignments ka WHERE ka.kiosk_id = k.id AND ka.released_at IS NULL) AS active_assignments
FROM kiosks k
ORDER BY k.name;

-- Trends by category/time (uses incidents(category_id) + created_at)
SELECT c.name, date_trunc('week', i.created_at) AS week, count(*) AS incident_count
FROM incidents i
LEFT JOIN categories c ON c.id = i.category_id
GROUP BY c.name, date_trunc('week', i.created_at)
ORDER BY week DESC, incident_count DESC;

-- Concurrency-safe: assign next incident to kiosk (call RPC)
SELECT * FROM rpc_assign_next_incident($1::uuid);

-- Approve reflection and (optionally) archive
SELECT rpc_approve_reflection($1::uuid, $2::uuid);
SELECT rpc_archive_incident($1::uuid);
```

Expected performance: With the proposed indexes and modest scale, all dashboard and assignment queries should return in <50 ms on warmed caches; aggregation queries remain sub-100 ms for year-1 volumes.

Bonus: Minimal API Contract (for Lovable/Next.js)
• Teacher creates incident: supabase.from('incidents').insert({student_id, category_id, summary}).single()
• Kiosk pulls next: supabase.rpc('rpc_assign_next_incident', { _kiosk_id })
• Kiosk submits reflection: supabase.rpc('rpc_submit_reflection', { _incident_id, _q1, _q2, _q3, _q4 })
• Teacher approves: supabase.rpc('rpc_approve_reflection', { _incident_id, _approver: user.id })

Recommended First Actions (3)
• Implement schema + indexes + RPCs in a sandbox; seed 10 students, 3 teachers, 2 kiosks, 6 categories.
• Run a race test (two kiosks spamming ‘assign next’) to confirm no duplicate assignments and stable status transitions.
• Wire teacher dashboard + kiosk app to the four RPC endpoints; verify report-to-submit-to-approve round-trip timing (target: 10–15s to file).
