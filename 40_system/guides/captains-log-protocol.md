# Captain's Log Protocol

To ensure continuous context, shared understanding, and process memory across sessions and personas:

1.  **Log Creation:** At the beginning of a new major task or session, Gemini will create a new log file in `system/session/logs/` following the convention `log-YYYYMMDD-XX-short-description.md`, where `XX` is a two-digit sequential number (01, 02, etc.) for logs created on that specific day.
    *   **Process for Generation (Trigger: "update the captain's log")**:
        1.  User saves the terminal output as `Terminal Saved Output.txt` into `00_inbox/`.
        2.  User instructs Gemini by saying "update the captain's log".
        3.  Gemini automatically processes `00_inbox/Terminal Saved Output.txt`.
        4.  **Decision Logic:**
            *   If a log file for the current date's primary session (`log-YYYYMMDD-01-*.md`) already exists, Gemini will re-synthesize the summary based on the new `Terminal Saved Output.txt` content and overwrite that existing log file.
            *   If no such log exists, Gemini will create a new log file with `XX=01`.
        5.  Gemini then deletes the inbox file.
        6.  Gemini prompts the user for GitHub sync approval.

2.  **Log Amendment/Appending (Trigger: "amend the log" or "append the log")**:
    *   **Purpose:** To update the most recently created log file for the current day, ensuring a single, evolving log for continuous chat sessions, by processing only the new conversation exchanges.
    *   **Process:**
        1.  User saves *only the new conversation exchanges* (the part of the transcript since the last log update) into `Terminal Saved Output.txt` in `00_inbox/`.
        2.  User instructs Gemini by saying "amend the log" or "append the log".
        3.  Gemini prompts the user for confirmation that `Terminal Saved Output.txt` contains only the new content.
        4.  Upon user confirmation, Gemini reads `00_inbox/Terminal Saved Output.txt`.
        5.  Gemini synthesizes a summary *only of this new content*.
                4.  Gemini identifies the log file with the highest sequential number (`XX`) for the current date in `40_system/session-logs/`.
        7.  Gemini appends this new summary (and potentially a new "Detailed Session Breakdown" section for the appended content) to the existing log file.
        8.  Gemini re-reads the *entire* updated log file, re-synthesizes and overwrites *only* the "Key Outcomes & Decisions" section based on the full, updated log content.
        9.  Gemini then deletes the inbox file.
        10. Gemini prompts the user for GitHub sync approval.

3.  **Real-time Log Entries:** Throughout the session, for significant actions, decisions, forks in the plan, or important information, a new, concise entry will be appended to the current log file. Each entry will follow this format:
    ```
    ## YYYY-MM-DD HH:MM:SS [Persona: Name] [Type: Action/Decision/Fork/Info/Summary] [Tags: #tag1 #tag2]
    [Concise, single-line or very short summary of the event/update.]
    ```
    *   **Timestamp:** `YYYY-MM-DD HH:MM:SS` for precise chronological tracking.
    *   **Persona:** Indicates which persona (e.g., Default, Prompt Engineer) is making the entry.
    *   **Type:** Categorizes the entry (e.g., `Action`, `Decision`, `Fork`, `Info`, `Summary`).
    *   **Tags:** Short, descriptive hashtags for quick filtering and context.
    *   **Content:** Extremely concise, single-line or very short summary.

4.  **Log Review (by Personas):** When a persona (e.g., Prompt Engineer) is activated, its first action will be to review the latest session log to gain immediate context.

5.  **Session Summary & Archiving:** At the end of a session or major task, a final `[Type: Summary]` entry will be added to the log, providing a high-level overview.
    *   **Purpose:** A comprehensive overview of the session's key achievements, decisions, and open items, synthesized by Gemini based on the provided conversation history.
    *   **Process for Generation:**
        1.  User saves the terminal output as `Terminal Saved Output.txt` into `00_inbox/`.
        2.  User instructs Gemini by saying "update the captain's log".
        3.  Gemini automatically processes `00_inbox/Terminal Saved Output.txt`, synthesizes the content, generates the summary, writes it to the session log, and then deletes the inbox file.
    *   **Content:**
        *   **Working Directory:** The absolute path of the primary working directory for the session.
        *   **Initiated Agent/Stack:** The specific agent, stack, or mode that initiated the session (e.g., Default instance, Sandbox Creation Engineer).
        *   **Relational Connections:** Indicates if this session is part of a multi-session sequence, a fork from a previous session, or a standalone session.
        *   Key achievements and completed tasks.
        *   Major decisions made and their rationale.
        *   Significant forks in the plan or challenges encountered and their resolutions.
        *   Outstanding questions, next steps, or open items.
        *   Any critical context for future sessions.