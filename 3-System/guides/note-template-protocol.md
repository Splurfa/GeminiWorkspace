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

## IV. Tagging Protocol

For detailed guidance on tagging principles, approved tag hierarchy, and specific tagging strategies for different note types (e.g., daily notes vs. project notes), please refer to the dedicated Tagging Protocol document: [[3-System/guides/tagging-protocol.md]]

## V. Process for Formatting Notes

1.  **Create or Rename File:** Ensure the filename is in `Title Case.md`.
2.  **Add H1 Title:** The first line of the note must be an H1 heading (`#`) that exactly matches the filename.
3.  **Add Metadata (Inline Tags & Optional YAML):**
    *   Place inline tags directly within the note content (e.g., `#tagOne #tagTwo`).
    *   Optional: For general notes, you may still use a YAML frontmatter block for `date`, `description`, and `source` if desired, but tags should be inline.
4.  **Write Content:** Add the body of the note below the metadata.
5.  **Adjust Heading Hierarchy:** When copying content from one note to another, ensure that the heading levels (e.g., `##`, `###`) are adjusted to maintain a logical and consistent hierarchy within the *target* note. The top-level heading of the copied content should align with the appropriate sub-level in the new document.
