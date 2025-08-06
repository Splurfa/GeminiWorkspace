# Captain's Log Protocol

To ensure continuous context, shared understanding, and process memory across sessions and personas:

## 1. Log Creation (Trigger: "update the captain's log")

*   **Purpose:** To create a new Captain's Log entry for a new major task or session.
*   **Process:**
    1.  **User Action:** User synthesizes the terminal output (or relevant conversation history) using an external LLM (e.g., ChatGPT) into a structured summary. This summary should adhere to the "Standard Captain's Log Entry Format" outlined below.
    2.  **User Action:** User saves this pre-synthesized summary as a Markdown file (e.g., `log-summary-YYYYMMDD-XX.md` or a descriptive name) into `0-Inbox/user/`.
    3.  **User Action:** User instructs Gemini by saying "update the captain's log".
    4.  **Gemini Action:** Gemini reads the provided summary file from `0-Inbox/user/`.
    5.  **Gemini Action:** Gemini takes the provided summary content and uses it to create the new Captain's Log file in `3-System/session-logs/`. The filename will follow the convention `log-YYYYMMDD-XX-short-description.md`, where `XX` is a two-digit sequential number (01, 02, etc.) for logs created on that specific day. If a log file for the current date's primary session (`log-YYYYMMDD-01-*.md`) already exists, Gemini will overwrite that existing log file.
    6.  **Gemini Action:** Gemini then deletes the input summary file from `0-Inbox/user/`.
    7.  **Gemini Action:** Gemini prompts the user for GitHub sync approval.

## 2. Log Amendment/Appending (Trigger: "amend the log" or "append the log")

*   **Purpose:** To update the most recently created log file for the current day, ensuring a single, evolving log for continuous chat sessions.
*   **Process:**
    1.  **User Action:** User synthesizes *only the new conversation exchanges* (the part of the transcript since the last log update) using an external LLM (e.g., ChatGPT) into a structured summary of the new content. This summary should focus on "Key Outcomes & Decisions" and "Detailed Session Breakdown" for the new content.
    2.  **User Action:** User saves this pre-synthesized summary as a Markdown file (e.g., `log-amendment-YYYYMMDD-XX.md` or a descriptive name) into `0-Inbox/user/`.
    3.  **User Action:** User instructs Gemini by saying "amend the log" or "append the log".
    4.  **Gemini Action:** Gemini reads the provided summary file from `0-Inbox/user/`.
    5.  **Gemini Action:** Gemini identifies the log file with the highest sequential number (`XX`) for the current date in `3-System/session-logs/`.
    6.  **Gemini Action:** Gemini appends the new summary content to the "Detailed Session Breakdown" section of the existing log file.
    7.  **Gemini Action:** Gemini re-reads the *entire* updated log file, re-synthesizes and overwrites *only* the "Key Outcomes & Decisions" section based on the full, updated log content.
    8.  **Gemini Action:** Gemini then deletes the input summary file from `0-Inbox/user/`.
    9.  **Gemini Action:** Gemini prompts the user for GitHub sync approval.

## 3. Real-time Log Entries

*   **Purpose:** For Gemini's internal use to append concise, real-time notes for significant actions, decisions, forks in the plan, or important information throughout a session.
*   **Format:**
    ```
    ## YYYY-MM-DD HH:MM:SS [Persona: Name] [Type: Action/Decision/Fork/Info/Summary] [Tags: #tag1 #tag2]
    [Concise, single-line or very short summary of the event/update.]
    ```
*   **Components:**
    *   **Timestamp:** `YYYY-MM-DD HH:MM:SS` for precise chronological tracking.
    *   **Persona:** Indicates which persona (e.g., Default, Prompt Engineer) is making the entry.
    *   **Type:** Categorizes the entry (e.g., `Action`, `Decision`, `Fork`, `Info`, `Summary`).
    *   **Tags:** Short, descriptive hashtags for quick filtering and context.
    *   **Content:** Extremely concise, single-line or very short summary.

## 4. Log Review (by Personas)

*   **Purpose:** To ensure context continuity.
*   **Process:** When a persona (e.g., Prompt Engineer) is activated, its first action will be to review the latest session log to gain immediate context.

## 5. Standard Captain's Log Entry Format

All pre-synthesized summaries provided by the user for Captain's Log entries (for both creation and amendment) should adhere to this standard Markdown format:

```markdown
# Captain's Log - YYYY-MM-DD-XX: [Short Description of Session]

**Working Directory:** [Absolute path of the primary working directory for the session]
**Initiated Agent/Stack:** [The specific agent, stack, or mode that initiated the session (e.g., Default instance, Sandbox Creation Engineer)]
**Relational Connections:** [Indicates if this session is part of a multi-session sequence, a fork from a previous session, or a standalone session]

## Key Outcomes & Decisions:

*   [Key achievement 1]
*   [Major decision 1 and its rationale]
*   [Significant fork in plan or challenge encountered and its resolution]

## Detailed Session Breakdown:

*   [Chronological summary of key interactions, tasks, and their outcomes.]
*   [Reference specific user prompts or Gemini actions if relevant.]

## Outstanding Questions, Next Steps, or Open Items:

*   [Outstanding question 1]
*   [Next step 1]
*   [Open item 1]
```