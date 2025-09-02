# Meeting Summary Generation Protocol

## 1. Purpose

This protocol outlines the automated workflow for generating static HTML meeting summaries from a source transcript.

## 2. Workflow Overview

This process combines a source transcript, structured conversation flow data (Markdown), and executive summary data (Markdown) with an HTML template to produce a final, formatted HTML summary.

## 3. Inputs

*   **Source Transcript:** A Markdown file containing the meeting transcript, placed in the `0-Inbox/assistant/` directory.
    *   Example: `0-Inbox/assistant/Bx OS Stakeholder Meeting.md`
*   **Conversation Flow Data (Markdown):** A Markdown file containing the structured conversation flow and key takeaways, derived from the transcript, placed in the `0-Inbox/assistant/` directory.
    *   Expected filename: `[transcript_filename_base]-flow.md` (e.g., `Bx OS Stakeholder Meeting-flow.md`)
    *   **Format:** Expected to contain a Markdown table for the conversation journey and an unordered list for key takeaways.
*   **Executive Summary Data (Markdown):** A Markdown file containing the structured executive summary, derived from the transcript, placed in the `0-Inbox/assistant/` directory.
    *   Expected filename: `[transcript_filename_base]-summary.md` (e.g., `Bx OS Stakeholder Meeting-summary.md`)
    *   **Format:** Expected to contain an introductory paragraph followed by sections with headings, introductory paragraphs, and bulleted lists for points.

## 4. Processing Steps

Upon receiving a command to generate a meeting summary (e.g., `create meeting summary for [entity] [transcript_filename_base]`), the following steps are executed:

1.  **Read Markdown Inputs:** The specified conversation flow Markdown and executive summary Markdown are read from `0-Inbox/assistant/`. The source transcript is also present for archival and filename inference, but its content is not directly parsed for HTML generation in this step.
2.  **Markdown Parsing:** The Markdown content from the conversation flow and executive summary files is parsed into structured data by the `generation_script.js`.
3.  **HTML Generation:**
    *   The `generation_template.html` (located in `portal/_template_test/generation_template.html`) is read.
    *   The parsed data is used to populate the template's placeholders.
    *   This process is managed by `generation_script.js` (located in `portal/_template_test/generation_script.js`).
4.  **Output HTML Creation:** A final HTML file is generated.

## 5. Output & Deployment

*   **Output File:** The generated HTML summary (e.g., `test_summary_output.html` for testing, or `YYYY-MM-DD-[meeting-topic].html` for production) is created. The filename is derived from the source transcript.
*   **Deployment:** The generated HTML file is committed to the appropriate location within the `portal` repository (e.g., `portal/[entity]/meetings/`). This deployment follows the [[github-sync-protocol]].

## 6. Command Structure

The command to initiate this workflow is:
`create meeting summary for [company|derek|zach] [transcript_filename_base]`

*   **`[transcript_filename_base]`**: This refers to the main part of your transcript's filename (e.g., `Bx OS Stakeholder Meeting` for `Bx OS Stakeholder Meeting.md`). I will use this base name to find the associated flow and summary JSON files in the inbox.
