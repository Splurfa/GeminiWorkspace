---
note_title: ABA Rail Initial Idea Synthesis
date: 2025-08-12
source: Internal Document
tags:
  - aba-rail
  - strategy
  - synthesis
related_notes:
  - "[[aba-rail-manifest]]"
---
# ABA Rail Initial Idea Synthesis

#synthesis #idea #strategy

## Checkpoint Summary

Your partner is describing a glaring workflow gap in ABA: there’s no end‑to‑end system that starts with the behavior tech’s ground‑level data capture and programmatically moves the case up the chain (field supervisor → BCBA → payer authorization → admin/RCM), with the right reviews, alerts, and artifacts at each ‘stage gate.’ They believe (1) providers would adopt it immediately if well executed, (2) insurers would love it even more, because it prevents back‑billing and shortens the auth/claims loop, and (3) you have a practical path to build it with a design‑partner clinic (—True Care—) and a willing collaborator (Danny).

Below is a full synthesis plus a concrete plan to run with.

---

## 1) Comprehension

- **Problem**: Fragmented tools force ABA staff to juggle notes, supervision, authorizations, and billing in disconnected systems. The first mile (tech on site) is the weakest link; everything upstream inherits that mess.
- **Vision**: A**ground‑up, stage‑gated workflow OS**for ABA that (a) captures high‑fidelity data at point of service, (b) routes it through required clinical review/approval, (c) packages the exact artifacts payers require, and (d) auto‑hands off to billing—closing the loop.
- **Why now**: Provider burnout, payer pressure on fraud/waste/abuse, state EVV and audit demands, and the rise of lightweight APIs/clearinghouses make a tight, auditable pipeline both feasible and valuable.
- **Go‑to‑market wedge**: Build with a design partner; make insurers the economic buyer/ally (or co‑sponsor) by preventing back‑billing and denials.

## 2) Analysis

### Value chain (who wins and why)

- **Behavior Tech (RBT)**: One tap to start/end a session, embedded protocol steps, required fields enforced, offline‑first, EVV‑friendly, supervisor ping when a threshold/event triggers.
- **Field Supervisor / BCBA**: Inbox of ‘cases needing action,’ side‑by‑side data + policy checklists, treatment plan and goals linked, sign‑offs tracked.
- **Admin/RCM**: Authorizations and units tracked automatically; clean claims generated; fewer reworks/denials.
- **Payers/UM teams**: Standardized packets, real‑time status, fewer retro‑auths, audit trail by default.
- **Owners**: Higher utilization of authorized units, faster cash, fewer write‑offs.

### Strategic opportunity

- **First‑mile as the product moat**: If you own accurate, structured source data at capture, you own the downstream truth. Everyone else must integrate with you.
- **Network effects**: Standardized pre‑auth and claim packets become a de‑facto spec that payers prefer, making providers likelier to adopt.
- **Defensibility**: State‑by‑state payer quirks encoded as rules; as that library hardens, you get a living compliance engine competitors can’t quickly copy.

### What this implicitly asks for

- **A rigorous state machine**(stage‑gates, SLAs, and required artifacts per step).
- **Interoperability rail**for eligibility, pre‑auth, claims, remits (use a clearinghouse/API; fall back to portal automation where needed).
- **Audit‑by‑design**: immutable logs, signatures, timestamps, EVV, versioned artifacts.
- **Human‑centered UX**for the lowest‑leverage, highest‑impact users (RBTs) so the rest of the chain works.

## 3) Plan (from 0 → credible product)

### 3.1 Product thesis

> **“ABA Rail”**(placeholder name): the ground‑to‑payout operating rail for ABA.
> Capture once at the point of care → guided clinical review → payer‑ready packet → clean claim → closed‑loop analytics.

### 3.2 MVP scope (must‑haves)

1. **RBT mobile app**(offline‑first):
   - Check‑in/out, EVV, required note template, goal tracking, incident/flag button.
   - Auto‑builds a**Session Packet**(data + required attestations).
2. **Supervisor/BCBA worklist**:
   - Queue of packets needing review; red/yellow/green gating; templated feedback; e‑sign.
   - **Treatment Plan & Auth link**shown inline (authorized units left, dates, CPT lines).
3. **Authorization tracker**:
   - One place showing**status, units, expiration**;triggers**auto‑renew workflows**early.
4. **Payer packet generator**:
   - Standardized “pre‑auth” & “progress/update” packets with exactly the attachments payers ask for.
5. **Billing handoff**:
   - Creates a clean claim from approved sessions; exports to clearinghouse; reconciliation inbox for denials.
6. **Audit trail + dashboards**:
   - Every stage change, who/when/where; simple KPIs (see below).

> **Out of scope for MVP**: scheduling, payroll, parent portal, inventory—unless a single design partner insists and it unblocks adoption.

### 3.3 Non‑negotiables

- HIPAA posture (BAA cloud, least‑privilege access, encryption at rest/in‑transit).
- **Role‑based access**(RBT vs Supervisor vs BCBA vs Admin).
- **Immutable logs**of signatures, timestamps, geo‑signals (where allowed).
- **Configurable rules per payer/state**(units, modifiers, documentation checklists).

### 3.4 Data & object model (starter)

- **Client**(payer(s), plan, auths)
- **Staff**(roles: RBT, Supervisor, BCBA)
- **Treatment Plan**(goals, CPT lines expected)
- **Authorization**(payer, units, start/end, utilization)
- **Session**(start/end, EVV, note, goal data, signatures)
- **Review**(supervisor actions, comments, approvals)
- **Packet**(pre‑auth/update packet with attachments, status)
- **Claim**(lines, modifiers, status)
- **Remittance**(payments, denials, codes)

### 3.5 Integrations strategy

- **Clearinghouse/API**for: eligibility checks, prior auth status (where available), claims, remits.
- **RPA/portal fallback**for payers with weak APIs (scripted, monitored, and rate‑limited).
- **Document templates**for payers that demand their PDF forms—auto‑fill from the packet.

### 3.6 GTM & business model

- **Design partners**: True Care + 1–2 more clinics of different sizes. Exchange discounted pricing for structured access and published ROI metrics.
- **Pricing**(test these): per member per month (PMPM), per active staff seat, or usage‑based on packets/claims.
  Optional**RCM add‑on**(%) for clinics that want a full service.
- **Payer route**: Pilot a “preferred packet” with one insurer; offer them**denial reduction + cycle‑time reduction**;they co‑sponsor provider onboarding.
- **Paperwork**: LOIs, data‑use/BAAs, pilot success criteria in writing before buildout.

### 3.7 KPIs (north‑star and proof points)

- **Days to authorization**(first request & renewals).
- **Denied claims rate**and**denials per reason**.
- **% of sessions approved without rework**(clean‑first‑pass).
- **Utilization of authorized units**(used vs expired).
- **Time‑in‑queue by stage**(RBT → Supervisor → BCBA → Payer → RCM).
- **Documentation completeness**(all checklist items present at submission).

### 3.8 Risks & how we counter them

- **Ground‑level adoption**: RBTs won’t tolerate clunky UX → build mobile‑first, <60‑second session closeout, offline mode, and only the required fields at the right moment.
- **Payer heterogeneity**: rules differ by state/plan → rule engine + payer/state profiles; start with 1–2 high‑impact payers and grow the library.
- **Automation liability**: never auto‑submit without a review by a human with a clear e‑signature and preview of what will be sent.
- **Security/compliance**: SOC‑2 program early; strong audit logging; formal BAAs; data retention policy.

## 4) Execution (what we can produce immediately)

### 4.1 Artifacts to create now

1. **One‑pager (providers)**– promise, screenshots/wireframes, how it shortens the workday and reduces denials.
2. **One‑pager (payers)**– standardized packets, fewer retro‑auths, clearer medical‑necessity evidence.
3. **Process map**(swimlanes): RBT → Supervisor → BCBA → Payer → Admin; with stage‑gates and required artifacts.
4. **Packet specs**(v0): required fields, attachments, and signature flows for “pre‑auth,” “update,” and “claim.”
5. **Pilot plan**with success metrics and reporting cadence.
6. **Data model & permissions matrix**(who can see/edit what).
7. **Risk register**with owners and mitigations.

### 4.2 First build slice (walking skeleton)

- **Mobile session capture**(check‑in/out, EVV, required note) →**Supervisor inbox**(approve/request fix) →**Auth tracker**(units, dates) →**Packet PDF**preview →**Export claim**(sandbox) →**Dashboard**(KPIs).
  This proves the rail works end to end with one payer and one clinic.

### 4.3 Design principles for the RBT app

- **One big button**: “Start Session.”
- Contextual micro‑prompts (show only what’s required at that moment).
- **Flag**button for incidents—auto‑notifies supervisor and bookmarks the context.
- **Finish**flow enforces completeness (signatures, goals updated, note present).
- Offline cache with safe retry and no duplicate sessions.

## 5) Review (assumptions, uncertainties, and next moves)

**Assumptions I made**(explicit so we can accept/adjust):

- Design partner “True Care” will grant access to shadow workflows and co‑define packet requirements.
- “Danny” can help with clinic outreach and payer conversations.
- You want to bias toward**provider delight**while building**payer‑credible packets**(not the other way around).
- We will begin with 1–2 payer profiles, not attempt “all payers” at launch.

**Immediate next moves I recommend**

- Approve the**MVP slice**and KPI list above.
- Green‑light creation of the**two one‑pagers**,**swimlane map**, and**packet v0 spec**(I can draft all of these next).
- Line up 2–3 payer contacts (even informal) to validate packet content and willingness to pilot*standardized submissions*.
- Secure written**pilot LOIs**from True Care and one additional clinic with explicit success criteria.

### Bottom line

This isn’t “another ABA EMR.” It’s a**ground‑truth rail**that turns messy first‑mile behavior data into payer‑ready evidence, with stage‑gates and audit baked in. Providers get fewer headaches and faster cash; payers get cleaner packets and less retro‑auth exposure. That’s a wedge you can drive into the market—and with a small, tough MVP you can prove it quickly and expand from there.

---

[[aba-rail-manifest|Back to ABA Rail Project Manifest]]