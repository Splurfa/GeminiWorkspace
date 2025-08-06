# Project Manifest Protocol

This protocol defines the structure and usage of `project-manifest.md` files, which serve as the single, living source of truth for individual projects within the `20_projects/` directory. Each manifest acts as a project's dashboard, providing essential details, status, objectives, and key links.

## 1. Purpose of a Project Manifest

A `project-manifest.md` file is designed to:
*   Provide a concise, at-a-glance overview of a specific project.
*   Act as the central hub for key project information.
*   Facilitate quick understanding of a project's status and current focus.
*   Integrate with other system protocols (e.g., daily notes, tagging).

## 2. Location and Naming Convention

*   Each project must have its own project manifest file, named `[project-name]-manifest.md` (using kebab-case for the project name).
*   This manifest file must be located at the root of its dedicated project folder within `20_projects/` (e.g., `20_projects/your-project-name/your-project-name-manifest.md`).

## 3. Standard Content Structure

Each `project-manifest.md` file should adhere to the following Markdown structure:

```markdown
# Project Manifest: [Project Name]

## Overview
*   **Project ID:** [Unique Identifier, e.g., `PROJ-COMMONTHREAD`, `PROJ-BXOS`]
*   **Mission:** [Concise statement of the project's purpose and overarching goal.]
*   **Description:** [Brief summary of what the project entails.]
*   **Status:** [Use a tag from the approved status tags, e.g., `#status-active`, `#status-on-hold`, `#status-completed`, `#status-archived`]
*   **Date Initiated:** YYYY-MM-DD
*   **Last Updated:** YYYY-MM-DD

## Objectives
*   [Key Objective 1: Specific, Measurable, Achievable, Relevant, Time-bound]
*   [Key Objective 2]
*   ...

## Key Resources
*   **Project Folder:** `[[Project Folder Name]]` (e.g., `[[common-thread]]`, `[[behavior-support-app]]`) - *Use a wikilink to the project's own folder for easy navigation.*
*   **External Links:** [List any relevant external links, e.g., `[Figma Board](URL)`, `[Google Drive Folder](URL)`]
*   **Related Notes:** [List any key internal notes related to this project, e.g., `[[Client Strategy]]`, `[[Project X Meeting Notes]]`]

## Next Actions (High-Level)
*   [High-level action 1: Strategic actions that advance the project. Granular tasks should be managed in daily notes.]
*   [High-level action 2]
*   ...

## Success Metrics
*   [How will the success of this project be measured?]

## Project History (Optional)
*   [Brief log of major milestones, decisions, or status changes. Use YYYY-MM-DD format.]
```

## 4. Maintenance and Integration

*   **Regular Updates:** The `project-manifest.md` should be regularly updated to reflect the project's current status, objectives, and next actions. It should always be a true reflection of the project's state.
*   **Integration with Daily Notes:** The "Next Actions (High-Level)" in the manifest serve as strategic pointers. Granular, day-to-day tasks related to these actions should be managed within your daily notes. Daily notes can link back to the project manifest for context.
*   **Tagging:** All `project-manifest.md` files and related project notes must adhere to the `[[note-template-protocol#tagging-protocol-your-cross-cutting-organization-system|tagging protocol]]`.
    *   Always include a project-specific tag (e.g., `#project-common-thread`, `#project-bx-os`).
    *   Always include a status tag (e.g., `#status-active`, `#status-on-hold`).
*   **Wikilinks:** Use `[[Title Case]]` wikilinks for all internal references to other notes or system documents.

## 5. Starting a New Project

When initiating a new project:
1.  Create a new dedicated folder for the project within `20_projects/` (e.g., `20_projects/new-project-name/`).
2.  Create a `project-manifest.md` file within this new project folder.
3.  Populate the `project-manifest.md` file following the "Standard Content Structure" outlined above.
