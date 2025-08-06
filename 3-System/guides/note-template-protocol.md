# Note Template & Tagging Protocol

This protocol outlines the standardized method for creating and formatting notes. Its purpose is to ensure consistency, facilitate organization, and support your discovery and synthesis workflow.

## I. Core Principles

1.  **Wikilinks for Inter-Note Connections:** For linking *between* different notes or to broader topics, use the [[kebab-case-filename]] wikilink format. This is for building your knowledge graph across multiple documents. Crucially, wikilinks should be formatted without any surrounding backticks or apostrophes, or any other characters that might interfere with Obsidian's recognition.
2.  **Inline Stacked Tags for Classification:** Tags are for classification and cross-cutting organization. Use multiple, simple, single-word tags stacked together directly within the note content (e.g., #business #strategy #client). We do NOT use slashes or hyphens within a single tag. Crucially, inline tags should be formatted without any surrounding backticks or apostrophes, or any other characters that might interfere with Obsidian's recognition.

## II. The General Note Template

This is the universal structure for all standard notes. It begins with YAML frontmatter, followed by the H1 title, a brief summary, optional source and date, inline tags, and then the main content.

Example Structure:

---
title: Example Note Title
date: YYYY-MM-DD
source: Optional Source Description
related_notes: [[related-note-one]], [[related-note-two]]
---
# Example Note Title

This is a brief, one-sentence summary of the note's core idea.

#tag-one #tag-two #tag-three #tag-four

This is where the main content of the note begins. Use standard Markdown for formatting.

[Content...]

## III. The Daily Note Template: Your Daily Synthesis Framework

The daily note is a dynamic workspace designed for organizing and processing your structured insights. It is located at: /Users/splurfa/Documents/GeminiWorkspace/3-System/guides/daily-note-template.md

Refer to that file for its specific structure and guidance on how to use its sections for input, active synthesis, emergent insights, parking, and daily reflection.

## IV. Tagging Protocol

For detailed guidance on tagging principles, approved tag hierarchy, and specific tagging strategies for different note types (e.g., daily notes vs. project notes), please refer to the dedicated Tagging Protocol document: [[3-System/guides/tagging-protocol.md]]

## V. Process for Formatting Notes

1.  **Add H1 Title:** The first line of the note must be an H1 heading, indicated by a single hash symbol, that exactly matches the filename.
2.  **Add Metadata (Inline Tags & Optional YAML):**
    *   Place inline tags directly within the note content (e.g., #tag-one #tag-two).
    *   Optional: For general notes, you may still use a YAML frontmatter block for date, description, source, and related_notes if desired. Related notes can be listed inline (e.g., related_notes: [[note-a]], [[note-b]]) or stacked with line breaks, but tags should be inline.
3.  **Write Content:** Add the body of the note below the metadata.
4.  **Adjust Heading Hierarchy:** When copying content from one note to another, ensure that the heading levels (e.g., two hash symbols, three hash symbols) are adjusted to maintain a logical and consistent hierarchy within the *target* note. The top-level heading of the copied content should align with the appropriate sub-level in the new document.

## VI. Internal Linking Convention

For all internal references to other notes or guides within this workspace, use the double-bracketed wikilink format: [[kebab-case-filename]]. This is the ONLY accepted format for internal links, ensuring proper recognition and navigation within your knowledge graph. Do NOT use backticks or any other characters around these links.

## VII. Scope of this Protocol

This protocol primarily applies to general notes and daily notes. `README.md` files follow their own dedicated protocol: [[readme-protocol]].