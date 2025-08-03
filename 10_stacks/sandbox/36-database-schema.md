## **36\. Database Schema Designer**

**Purpose:** Design a normalized, efficient, and scalable database schema from a list of application features.

**When to use:** After the planning phase, before backend development begins.

**Input needed:**

*   A list of the application's key features and user stories.
*   The main objects or nouns in the system.
*   The target database technology (e.g., PostgreSQL, MySQL, MongoDB).

---

### **Your Input**

**Application Features:** \[List the key features, user stories, or operations from your project plan]

**Core Objects:** \[List the main nouns, e.g., Users, Products, Orders, Posts, Comments]

**Target Database:** \[e.g., PostgreSQL, MySQL, MongoDB, Firestore]

**Key Queries:** \[List 2-3 of the most important data questions you'll need to answer, e.g., "Find all orders for a given user," "List all comments on a specific post in chronological order"]

---

### **Instructions**

Please generate a complete database schema based on my input. Follow these steps:

#### **Step 1: Identify Tables and Columns**

*   For each core object, define a primary table.
*   Identify all necessary columns for each table, including data types.
*   Use a consistent and clear naming convention (e.g., `snake_case`).

#### **Step 2: Define Relationships**

*   Identify all relationships between the tables (One-to-One, One-to-Many, Many-to-Many).
*   Specify foreign keys to enforce these relationships.
*   For Many-to-Many relationships, define the necessary join tables.

#### **Step 3: Specify Constraints and Indexes**

*   Add `NOT NULL` constraints where appropriate.
*   Define `UNIQUE` constraints for fields that require it (e.g., usernames, email addresses).
*   Add indexes to columns that will be frequently used in `WHERE` clauses or `JOIN` operations to optimize for your key queries.

#### **Step 4: Generate the Schema**

*   Produce the complete schema in valid SQL `CREATE TABLE` statements (for SQL databases) or a clear JSON/object structure (for NoSQL databases).
*   Include comments explaining non-obvious choices.

---

### **Output Format**

Present the final schema with:

1.  **Schema Overview:** A high-level summary of the tables and their relationships.
2.  **SQL `CREATE TABLE` Statements:** The complete, ready-to-use SQL code.
3.  **Relationship Diagram (as text):** A simple text-based diagram showing how the tables connect (e.g., `users --< posts --< comments`).
4.  **Indexing Strategy:** A brief explanation of the indexes chosen and why.