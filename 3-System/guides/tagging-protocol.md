# Tagging Protocol: Your Cross-Cutting Organization System

This protocol outlines the principles and best practices for applying tags across your notes. Tags are orthogonal axes for filtering, retrieval, and understanding the *nature* and *context* of your thoughts. They enhance, rather than duplicate, your folder structure.

## I. Tagging Principles

*   **Consistency:** Apply tags consistently within their defined categories.
*   **Lowercase:** All tags must be in **lowercase**.
*   **Kebab-Case:** For multi-word tags, use **kebab-case** (e.g., `#multi-word-tag`).
*   **Clarity & Specificity:** Tags should be clear, concise, and specific enough to be useful for retrieval.
*   **Obsidian Compatibility:** Always ensure tags are recognized by Obsidian.
    *   **YAML Frontmatter Syntax:** When adding tags to the `tags:` field in YAML frontmatter, list them as plain strings without the `#` prefix (e.g., `tags: [strategy, system, bx-os]`).
    *   **Inline Tag Recognition:** Ensure all inline tags (`#tag`) are immediately followed by a space, newline, or punctuation (e.g., `#tag.`, `#tag,`) to ensure correct parsing by Obsidian. **Crucially, inline tags should be formatted as `#tag` without any surrounding apostrophes or other characters that might interfere with Obsidian's recognition.**

## II. The Three Pillars of Tagging (Categories & Examples)

This framework categorizes tags into three core pillars, each serving a distinct purpose for knowledge retrieval. New tags can be created as needed, provided they adhere to the Tagging Principles and fit within one of these categories.

### A. Subject/Topic Tags (The "What")

*   **Purpose:** Describe the primary subject matter or domain of the content. These are the high-level themes.
*   **Placement:** Primarily in **YAML Frontmatter** for the overall note's themes. Can be used **inline** if a specific section introduces a new, distinct subject.
*   **Characteristics:** Broad, evergreen, consistent.
*   **Examples:** `#strategy`, `#system`, `#tooling`, `#ai`, `#business`, `#personal`, `#finance`, `#health`, `#learning`, `#workflow`, `#protocol`, `#framework`, `#marketing`, `#operations`, `#sales`, `#consulting`, `#library`, `#project`.

### B. Content/Thought Type Tags (The "How")

*   **Purpose:** Describe the *nature* or *form* of the content or thought being expressed. This is crucial for understanding *what kind* of information you're looking at.
*   **Placement:** Primarily **inline**, next to the specific thought or idea. Can be in **YAML Frontmatter** if the entire note is of a specific type (e.g., a dedicated `insight` note).
*   **Characteristics:** Action-oriented, descriptive of cognitive process.
*   **Examples:** `#idea`, `#question`, `#insight`, `#reflection`, `#experiment`, `#deliverable`, `#efficiency`, `#synthesis`, `#discovery`.

### C. Context/Entity Tags (The "Where/Who")

*   **Purpose:** Link content to specific projects, people, organizations, or unique entities. These provide a direct connection to a specific "place" or "actor" in your knowledge graph.
*   **Placement:** Can be in **YAML Frontmatter** for project manifests or notes primarily about an entity. **Crucially, for Daily Notes, use in Frontmatter if the entity represents a primary input or defining event for the day's content.** Often **inline** when an entity is mentioned within a broader note.
*   **Characteristics:** Specific, often proper nouns or unique identifiers.
*   **Examples:** `#bx-os`, `#common-thread`, `#board-meeting`, `#nate-jones`, `#lovable`, `#supabase`, `#client`, `#family`, `#friends`, `#hillel-academy`.

## III. Tagging Specific Note Types

### Daily Notes

Daily notes are designed for capturing and processing daily inputs.

*   **Frontmatter Tags:** Use Subject/Topic Tags (A) and primary Context/Entity Tags (C) in the YAML frontmatter to describe the overall themes and defining events/sources of the day.
*   **Inline Tags:** Use Content/Thought Type Tags (B) inline to describe the nature of specific thoughts, ideas, questions, or insights within the note. Use Subject/Topic Tags (A) and Context/Entity Tags (C) inline only when they add specific, localized meaning beyond the frontmatter.
*   **Action Items:** For concrete action items, use Obsidian's checkbox formatting (`- [ ]`) instead of a `#task` tag.
*   **Avoid:** Over-tagging with project-specific tags unless the daily note is *primarily* about a single project's progress. Link to project notes for detailed project context.

### Project Notes

Project notes (e.g., Project Manifests, specific project-related research) are the primary location for project-specific tags.

*   **Frontmatter Tags:** Use Subject/Topic Tags (A) and Context/Entity Tags (C) in the YAML frontmatter to describe the project's nature, phase, or key areas.
*   **Inline Tags:** Use Content/Thought Type Tags (B) inline for specific thoughts or insights related to the project.

## IV. Tag Management & Evolution

*   **Adding New Tags:** If you identify a need for a new tag not currently in this protocol, ensure it adheres to the "Tagging Principles" (Section I) and fits within one of the "Three Pillars of Tagging" (Section II). Once used, consider adding it to the examples in the protocol if it represents a recurring concept.
*   **Deprecation/Migration:** If an old tag needs to be deprecated, it will be noted here, and a simple strategy (e.g., search and replace) will be suggested for migration in existing notes.
*   **Consistency:** Ensure the primary project tag is consistently applied to all notes directly related to that project.

## IV. Tag Management & Evolution

*   **Adding New Tags:** If you identify a need for a new tag not currently in this protocol, ensure it adheres to the "Tagging Principles" (Section I). Once used, consider adding it to the "Approved Tag Hierarchy" as an example if it represents a recurring concept.
*   **Deprecation/Migration:** If an old tag needs to be deprecated, it will be noted here, and a simple strategy (e.g., search and replace) will be suggested for migration in existing notes.

## V. Tool-Specific Considerations - Obsidian

*   **YAML Frontmatter Syntax:** When adding tags to the `tags:` field in YAML frontmatter, list them as plain strings without the `#` prefix (e.g., `tags: [strategy, system, bx-os]`).
*   **Inline Tag Recognition:** Ensure all inline tags (`#tag`) are immediately followed by a space, newline, or punctuation (e.g., `#tag.`, `#tag,`) to ensure correct parsing by Obsidian.
