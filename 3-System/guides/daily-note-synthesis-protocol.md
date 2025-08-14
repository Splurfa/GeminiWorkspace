# Daily Note Synthesis Protocol

This protocol outlines the process for the AI agent (Gemini) to assist with the synthesis of a user's daily note.

## 1. Trigger

The AI agent will initiate this protocol when the user explicitly requests assistance with "daily note synthesis" for a specific daily note (e.g., "Synthesize my daily note for August 5th").

## 2. Input for Synthesis

When performing daily note synthesis, the AI agent will primarily focus on the content within the following sections of the specified daily note:

*   **"1. Raw Sources for Synthesis (Your Daily Capture)"**: This section contains initial thoughts and references to external source materials.
*   **"2. Today's Structured Insights (Your Daily Input Hub)"**: This section contains pre-processed and structured insights provided by the user.

## 3. Synthesis Tool

The AI agent will leverage the `40-idea-organization-prompt.md` from the `30_library/prompts/writing-communication/` directory to facilitate the synthesis process.

## 4. Synthesis Process

1.  **Read Daily Note:** The AI agent will read the specified daily note, paying close attention to the content in the designated input sections (1 and 2).
2.  **Apply Prompt #40:** The AI agent will internally apply the principles and guidance from the `40-idea-organization-prompt.md` to the gathered input, identifying connections, themes, questions, and potential areas for organization.
3.  **Formulate Synthesized Output:** The AI agent will present the synthesized output to the user. This output will aim to:
    *   Highlight key themes or connections across the raw sources and structured insights.
    *   Suggest potential ways to organize or categorize the information further.
    *   Propose how the synthesized content might map to the "Active Synthesis & Exploration" sections (e.g., Emerging Themes & Core Questions, Tool & Workflow Ideas, Strategic Connections & Implications) within the daily note, or suggest new insights for the "Emergent Insights" section.

## 5. Output Presentation

The synthesized output will be presented in a clear, concise, and actionable format, guiding the user on how to further refine and integrate their daily note content.

## 6. Stage 2: Optional Atomic Deconstruction

After a daily note has been synthesized using the process above, you can choose to take it one step further by atomizing its contents. This powerful next step deconstructs the daily note into a network of interconnected atomic notes, fully integrating the day's most valuable insights into your permanent knowledge base.

This process is not automatic. It should be triggered when you feel a daily note is particularly rich with ideas that deserve to be preserved and connected.

**For the detailed workflow, see the [[daily-note-atomization-protocol]].**