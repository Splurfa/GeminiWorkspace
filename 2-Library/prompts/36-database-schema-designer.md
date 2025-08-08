---
source: "Nate Jones"
description: "Design database structures that match your product requirements."
date_added: "2025-08-02"
tags:
  - library
  - prompts
  - analysis-strategy
  - database-design
  - schema
  - data-modeling
  - SQL
  - NoSQL
  - data-architecture
  - scalability
  - performance-optimization
related_notes:
  - # No specific related notes identified at this time.
---
## 36. Database Schema Designer

**Purpose:** Design database structures that match your product requirements.

**When to use:** Starting a new project or refactoring existing data architecture.

**Input needed:**

*   Product requirements/user stories
*   Expected scale
*   Tech stack
*   Key operations

---

### Your Input

**Product Description:** [What you're building - features and functionality]

**User Stories:**

*   As a [user type], I want to [action] so that [outcome]
*   As a [user type], I want to [action] so that [outcome] [List key user stories]

**Tech Stack:**

*   Database: [PostgreSQL/MySQL/MongoDB/other]
*   Backend: [Language/framework]
*   Expected patterns: [REST/GraphQL/etc]

**Scale Expectations:**

*   Year 1 users: [Number]
*   Data growth rate: [Records/month]
*   Peak concurrent users: [Number]

**Key Operations:**

*   Most common queries: [List top 3-5]
*   Performance critical paths: [What must be fast]
*   Reporting needs: [Analytics requirements]

---

### Instructions

Design an optimal database structure:

#### Step 1: Requirements Analysis

Summarize the data needs based on user stories (2-3 sentences).

#### Step 2: Entity Relationship Design

**Core Entities:**

**Entity 1: [Name]**

*   Purpose: [What it represents]
*   Key attributes: [Main fields]
*   Relationships: [How it connects to others]
*   Volume: [Expected records]

**Entity 2: [Name]** [Same format]

[Continue for all main entities]

**Relationship Map:**

[Visual representation using text]
User (1) ----< (n) Order
Order (1) ----< (n) OrderItem
Product (1) ----< (n) OrderItem
etc.

#### Step 3: Detailed Table Specifications

**Table: users**

CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  username VARCHAR(50) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  is_active BOOLEAN DEFAULT true,
  -- Indexes
  INDEX idx_email (email),
  INDEX idx_username (username),
  INDEX idx_created_at (created_at)
);

*   **Purpose:** [Why this table exists]
*   **Key decisions:** [Why these fields/types]
*   **Growth:** [Expected records/year]

[Repeat for each table]

#### Step 4: Performance Optimizations

**Indexing Strategy:**

**For Query: "[Common query pattern]"**

*   Tables involved: [List]
*   Suggested index: CREATE INDEX idx_name ON table(field1, field2)
*   Why: [Explanation of optimization]

[Repeat for top 5 query patterns]

**Denormalization Decisions:**

*   What: [Field/data to denormalize]
*   Where: [Which table]
*   Why: [Performance gain vs. complexity]
*   Update strategy: [How to keep in sync]

**Partitioning Strategy:** (if applicable)

*   Table: [Which needs partitioning]
*   Method: [Range/List/Hash]
*   Key: [Partition column]
*   Rationale: [Why this approach]

#### Step 5: Data Integrity Rules

**Constraints:**

-- Foreign Keys
ALTER TABLE orders
ADD CONSTRAINT fk_user
FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE;

-- Check Constraints
ALTER TABLE products
ADD CONSTRAINT chk_price CHECK (price >= 0);

-- Unique Constraints
ALTER TABLE user_profiles
ADD CONSTRAINT uk_user_profile UNIQUE (user_id);

**Business Rules in Database:**

*   Rule: [Business requirement]
*   Implementation: [Trigger/constraint/function]
*   Code: [SQL implementation]

#### Step 6: Migration and Scaling Plan

**Initial Schema Setup:**

-- 1. Create database
CREATE DATABASE myapp_prod;

-- 2. Create tables in order
-- Users first (no dependencies)
[SQL]

-- Orders next (depends on users)
[SQL]

[Continue in dependency order]

**Migration Approach:**

*   Version control: [Migration tool/strategy]
*   Rollback plan: [How to undo changes]
*   Zero-downtime migrations: [Strategy]

**Scaling Considerations:**

*   At 10K users: [No changes needed]
*   At 100K users: [Add read replicas]
*   At 1M users: [Consider sharding strategy]
*   Sharding key: [If needed, what field]

#### Step 7: Sample Queries

**Common Operations:**

-- 1. Get user with profile
SELECT u.*, p.*
FROM users u
LEFT JOIN profiles p ON u.id = p.user_id
WHERE u.id = $1;

-- 2. Get recent orders with items
[Query with explanation]

-- 3. Analytics query example
[Query with performance notes]

**Query Performance Notes:**

*   Expected execution time: [X ms]
*   Index usage: [Which indexes help]
*   Optimization tips: [Any improvements]

---
