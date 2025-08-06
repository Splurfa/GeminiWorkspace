# Prompt Assembly Protocol

This document provides the detailed, step-by-step workflow for the "Orchestration Cycle" described in the `prompt-engineer-architecture.md`. It is the standard operating procedure for taking a prompt template from the `30_library` and preparing it for execution.

## Objective
To produce a clean, runnable, production-ready prompt file based on user-provided context and a template from the prompt library.

## The 5-Step Protocol

1.  **User Provides Context:** The user initiates the process by providing a structured or unstructured dump of their context, goals, and any other relevant information.

2.  **AI Maps to Library Template:** The assistant's first task is to analyze the user's input and identify the most appropriate prompt template from the `30_library`. The assistant will state which template it believes is the best fit.

3.  **Collaborative Refinement:** The assistant and user will then work together to gather any missing information required by the template's `Your Input` section. This is a conversational step to ensure all necessary data is present and correct.

4.  **AI Assembles Final Prompt:** Once all inputs are gathered, the assistant will assemble the final prompt. This involves taking the user's specific data and inserting it into the template structure.

5.  **AI Delivers Production-Ready File:** This is the critical final step. The assistant will:
    *   Create a new Markdown file in the `00_inbox` directory.
    *   The filename should be descriptive and end with `-prompt.md` (e.g., `runnable-board-of-directors-prompt.md`).
    *   The content of this file must be **production-ready**, which means:
        *   **No Metadata:** All template metadata (e.g., the `---` block with id, source, tags) MUST be removed.
        *   **No Template Titles:** All user-facing template titles or headers (e.g., `# 5. Personal Board of Directors` or `### Your Input`) MUST be removed.
        *   **Starts Cleanly:** The file content must begin directly with the first line of the user's actual input data (e.g., `**My Challenge/Decision:**`).
    *   The assistant will then notify the user of the file's creation and location.

This protocol ensures a consistent, error-free process that delivers a ready-to-use prompt for the user, respecting the distinction between a template and a runnable instance.
