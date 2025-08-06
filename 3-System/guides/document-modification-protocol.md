# Document Modification Protocol

This protocol outlines the principles and procedures Gemini will follow when modifying structured documents within this workspace (e.g., daily notes, other protocol documents, project manifests).

## I. Purpose

To ensure that all modifications to structured documents are performed consistently, accurately, and non-destructively, preserving the integrity, organization, and readability of the information.

## II. Core Principles for Modification

1.  **Analyze Existing Structure:** Before making any changes, Gemini will thoroughly analyze the target document's existing format, including:
    *   Heading hierarchies (H1, H2, etc.)
    *   Entry patterns (e.g., bulleted lists, numbered lists, distinct paragraphs per entry)
    *   Logical flow and chronological order (if applicable)
    *   Any specific formatting conventions unique to that document or section.

2.  **Preserve Content and Hierarchy:** When adding, updating, or removing content, Gemini will ensure that:
    *   All existing, relevant information is preserved.
    *   The document's established logical flow and heading hierarchy are maintained.
    *   New content is integrated in a way that respects the surrounding context and does not disrupt the overall structure.

3.  **Precise Insertion and Modification:** Gemini will identify the exact insertion or modification points to:
    *   Append new entries to existing lists or sections without overwriting previous content.
    *   Insert new sections at appropriate logical positions.
    *   Modify specific lines or blocks of text by accurately matching the `old_string` to prevent unintended changes.

4.  **Idiomatic Integration:** New content will be formatted to match the existing style and conventions of the document, ensuring a seamless and idiomatic integration.

## III. Application

These principles apply to all operations involving the modification of structured Markdown files, particularly when using tools like `replace` or `write_file` to append or insert content into existing sections.
