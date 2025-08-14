# Note Template & Metadata Protocol

This protocol outlines the standardized method for creating and formatting notes. Its purpose is to ensure consistency, facilitate organization, and support a scalable and interconnected knowledge graph.

## I. Universal Metadata Schema

All notes in this workspace (with a few exceptions listed in Section IV) MUST begin with a YAML frontmatter block that adheres to the following universal schema. This is the single source of truth for note metadata.

```yaml
---
title: "Clear and Descriptive Title of the Note"
date: YYYY-MM-DD
status: [evergreen | fleeting | draft | in-review | completed]
tags:
  - tag-one
  - tag-two
source: "URL or reference to the original source (optional)"
related_notes:
  - "[[link-to-a-related-note]]"
parent_note: "[[link-to-the-parent-note]]"
child_notes:
  - "[[link-to-a-child-note]]"
  - "[[another-child-note]]"
---
```

### Field Definitions:

*   **`title`**: The official title of the note. Should be clear and descriptive.
*   **`date`**: The date the note was created or last significantly updated (YYYY-MM-DD).
*   **`status`**: The current lifecycle stage of the note.
    *   `evergreen`: For core, stable concepts that are unlikely to change.
    *   `fleeting`: For quick thoughts or ideas that may be developed later.
    *   `draft`: For work in progress.
    *   `in-review`: For notes that are ready for your review.
    *   `completed`: For notes that are considered finished.
*   **`tags`**: A list of tags for classification. See the [[tagging-protocol]] for detailed guidance.
*   **`source`**: The original source of the information, if applicable (e.g., a URL, a book title, a person's name).
*   **`related_notes`**: A list of wikilinks to other notes that are related but not in a direct hierarchical relationship.
*   **`parent_note`**: A wikilink to a single parent note. This is crucial for creating hierarchies, especially for atomized notes, where the parent would be the synthesis hub.
*   **`child_notes`**: A list of wikilinks to child notes. This is the inverse of `parent_note` and is used, for example, by a synthesis hub to link to all the atomic notes generated from it.

## II. Tagging

For detailed guidance on tagging principles, approved tag hierarchy, and specific tagging strategies, please refer to the dedicated [[tagging-protocol]].

## III. Internal Linking Convention

For all internal references to other notes or guides within this workspace, use the double-bracketed wikilink format: `[[kebab-case-filename]]`. This is the ONLY accepted format for internal links.

## IV. Exceptions to the Universal Schema

The following file types are exempt from the universal metadata schema, as they serve specific, non-note purposes:

*   `README.md` files
*   `GEMINI.md` files
*   Protocol and guide documents in `3-System/guides/`
*   Any other custom documents you create that are not intended to be part of the standard note-taking system.
