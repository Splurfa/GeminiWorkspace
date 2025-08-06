# README Protocol

This protocol defines the purpose, structure, and formatting conventions for all `README.md` files within this workspace. Unlike other notes, READMEs serve as immediate, human-readable overviews for directories and projects.

## I. Purpose of README.md Files

`README.md` files are designed to provide a quick, at-a-glance understanding of the content, purpose, and usage of the directory or project they reside in. They are the entry point for anyone exploring a specific part of your workspace.

## II. Standard Content Structure

Each `README.md` file should adhere to the following structure, including relevant sections as needed:

1.  **Title:** A descriptive H1 title that clearly identifies the directory or project. This title does NOT need to match the filename.

    Example:

    # My Awesome Project

2.  **Purpose/Overview:** A brief, concise summary of what the directory or project is for.

3.  **Contents/Structure:** An outline or list of key files, subdirectories, or components within the current directory.

4.  **Usage/Getting Started:** Instructions on how to use, interact with, or get started with the contents of the directory or project.

5.  **Related Documents/Links:** Internal wikilinks to relevant notes, project manifests, or external resources that provide more detailed information.

    Example:

    *   Project Manifest: [[my-awesome-project-manifest]]
    *   Daily Note: [[daily-note-2025-08-01]]
    *   External Resource: [Project Documentation](https://example.com/docs)

## III. Formatting Conventions

*   **No YAML Front Matter:** `README.md` files should NOT include YAML front matter. Their purpose is immediate readability, not structured metadata for a knowledge graph.
*   **No Backticks:** As with all documentation in this workspace, backticks are NOT to be used for formatting. Use bolding, italics, or indentation for emphasis or code examples.
*   **Internal Links:** All internal references to other notes or guides must use the double-bracketed wikilink format: [[kebab-case-filename]]. Do NOT include the .md extension.
*   **Tags (Optional):** Tags can be used inline if appropriate for classification, following the guidelines in the Tagging Protocol. They should be lowercase and kebab-case for multi-word tags (e.g., #project #my-awesome-project).
*   **Headings:** Use standard Markdown headings (H1, H2, etc.) to structure content logically.

## IV. Integration with Workspace

This protocol is referenced in the main System Guides and Workspace Context documents to ensure its discoverability and adherence across the workspace.