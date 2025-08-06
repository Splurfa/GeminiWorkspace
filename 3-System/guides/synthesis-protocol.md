# Synthesis Protocol

This protocol outlines the process for the AI agent (Gemini) to assist with the synthesis of a given context into structured output. It is designed to be universal, applicable whenever a large amount of information needs to be distilled and organized.

## 1. Trigger & Input Context

The AI agent will initiate this protocol when the user explicitly requests synthesis for a specified context (e.g., "Synthesize this document," "Synthesize the content of my daily note for [date]").

The user will provide the context for synthesis. This can be:

*   Directly provided text.
*   A reference to a specific file or section within a file (e.g., "the raw sources section of my daily note").
*   A collection of files or a directory.

## 2. Synthesis Tool

The AI agent will leverage the `40-idea-organization-prompt.md` from the `30_library/prompts/writing-communication/` directory to facilitate the synthesis process.

## 3. Synthesis Process

*   **Read Context:** The AI agent will read and understand the provided context.
*   **Apply Prompt #40:** The AI agent will internally apply the principles and guidance from `40-idea-organization-prompt.md` to the gathered input, identifying connections, themes, questions, and potential areas for organization.
*   **Formulate Synthesized Output:** The AI agent will formulate the synthesized output.

## 4. Output Presentation & Structuring

The synthesized output will be presented in a clear, concise, and actionable format.

*   **Target Structure:** The AI agent will ask the user to specify a desired target structure or template for the output (e.g., "as a general note," "to fit into my daily note's active synthesis sections"). If no target is specified, a general, organized summary will be provided.
*   **Tag Suggestions (for Notes Universe):** When the specified target structure is a note (e.g., daily note, general note), the AI agent will suggest relevant tags from the `[[note-template-protocol]]` schema to help organize the synthesized content. These suggestions will strictly adhere to the lowercase, stacked, kebab-case (for multi-word individual tags), and non-redundant principles outlined in that protocol.
*   **Content Mapping:** The AI agent will propose how the synthesized content might map to specific areas of the target template (e.g., "This theme could go into your 'Emerging Themes & Core Questions' section").