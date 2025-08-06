# Note Template & Tagging Protocol

This protocol outlines the standardized method for creating and formatting notes. Its purpose is to ensure consistency, facilitate organization, and support your discovery and synthesis workflow.

## I. Core Principles

1.  **Title Case for Everything:** All filenames and note titles (the H1 heading) MUST use Title Case (e.g., `This Is a Title.md`). This improves readability in the file explorer and graph.
2.  **Wikilinks for Inter-Note Connections:** For linking *between* different notes or to broader topics, use the `[[Title Case]]` wikilink format. This is for building your knowledge graph across multiple documents.
3.  **Inline Stacked Tags for Classification:** Tags are for classification and cross-cutting organization. Use multiple, simple, single-word tags stacked together directly within the note content (e.g., `#business #strategy #client`). We do NOT use slashes or hyphens within a single tag.

## II. The General Note Template

This is the universal structure for all standard notes.

```markdown
# [Title Case Note Title]

[A brief, one-sentence summary of the note's core idea.]

[Optional: Source (e.g., URL, book title, or person)]

[Date: YYYY-MM-DD]

#tagOne #tagTwo #tagThree #tagFour

[The main content of the note begins here. Use standard Markdown for formatting.]

[Content...]
```

## III. The Daily Note Template: Your Daily Synthesis Framework

The daily note is a dynamic workspace designed for organizing and processing your structured insights. It is located at: `/Users/splurfa/Documents/GeminiWorkspace/40_system/guides/daily-note-template.md`

Refer to that file for its specific structure and guidance on how to use its sections for input, active synthesis, emergent insights, parking, and daily reflection.

## IV. Tagging Protocol: Your Cross-Cutting Organization System

Tags are your flexible, cross-cutting organizational tool. They enable smart folder organization, rapid retrieval, and provide context across your notes, regardless of their physical location.

### Format & Usage

*   All tags must be in **lowercase**.
*   Use **stacked tags** to combine independent concepts (e.g., `#business #strategy #client`).
*   For multi-word individual tags, use **kebab-case** (e.g., `#common-thread`, `#personal-finance`). Do not use kebab-case to combine categories that should be separate tags.
*   Tags should be applied consistently across all notes where relevant.

### Conceptual Hierarchy & Specificity

The 'hierarchy' of your tags is formed by the *combination* of independent, non-redundant tags you stack. Each additional tag adds specificity.

Aim for **2-4 independent tags** per note to provide sufficient context without redundancy. For example:
*   `#business #strategy #client` (combines three distinct concepts)
*   `#personal #health #fitness #running` (combines four distinct concepts)

Avoid redundancy: If `#business` and `#strategy` are separate tags, do not create a single tag like `#business-strategy`.

### Approved Top-Level Categories & Initial Tag List

The following are the **approved top-level categories** for your tags. All other tags should conceptually fall under one of these. This list is the starting point and can be expanded.

*   `#personal`
    *   `#health` (e.g., `#fitness`, `#nutrition`, `#mindfulness`)
    *   `#finance` (e.g., `#investing`, `#budgeting`, `#income`)
    *   `#household` (e.g., `#tasks`, `#maintenance`)
    *   `#relationships` (e.g., `#family`, `#friends`)

*   `#business`
    *   `#strategy` (e.g., `#growth`, `#marketing`, `#sales`)
    *   `#client` (e.g., `#acquisition`, `#retention`, `#project-name`)
    *   `#operations` (e.g., `#process`, `#efficiency`)
    *   `#consulting` (e.g., `#engagement`, `#deliverable`)

*   `#project`
    *   `#project-name` (e.g., `#common-thread`, `#behavior-support-app`, `#bx-os`) - *Specific project tags should be defined as needed, using kebab-case for multi-word project names.*

*   `#system`
    *   `#protocol` (e.g., `#note-taking`, `#tagging`)
    *   `#template` (e.g., `#daily-note`, `#meeting-note`)
    *   `#workflow` (e.g., `#discovery`, `#synthesis`)

*   `#library`
    *   `#prompt` (e.g., `#business-strategy`, `#creative-thinking`)
    *   `#reference` (e.g., `#book`, `#article`, `#video`)
    *   `#framework` (e.g., `#para`, `#eisenhower`)

*   `#tooling`
    *   `#ai` (e.g., `#llm`, `#automation`)
    *   `#software` (e.g., `#obsidian`, `#gemini-cli`)
    *   `#hardware`

### Tag Management & Coherence

*   **Strict Adherence:** Only tags listed in this `note-template-protocol.md` document are considered 'active' and approved for use. This document is the single source of truth for your tagging schema.
*   **Adding New Tags:** If you identify a need for a new tag not currently in this protocol, please inform me. I will propose its addition and conceptual placement within the hierarchy for your approval. Once approved, I will update this document.
*   **Deprecation/Migration:** If an old tag needs to be deprecated, it will be noted here, and a simple strategy (e.g., search and replace) will be suggested for migration in existing notes.

## V. Process for Formatting Notes

1.  **Create or Rename File:** Ensure the filename is in `Title Case.md`.
2.  **Add H1 Title:** The first line of the note must be an H1 heading (`#`) that exactly matches the filename.
3.  **Add Metadata (Inline Tags & Optional YAML):**
    *   Place inline tags directly within the note content (e.g., `#tagOne #tagTwo`).
    *   Optional: For general notes, you may still use a YAML frontmatter block for `date`, `description`, and `source` if desired, but tags should be inline.
4.  **Write Content:** Add the body of the note below the metadata.
5.  **Adjust Heading Hierarchy:** When copying content from one note to another, ensure that the heading levels (e.g., `##`, `###`) are adjusted to maintain a logical and consistent hierarchy within the *target* note. The top-level heading of the copied content should align with the appropriate sub-level in the new document.
