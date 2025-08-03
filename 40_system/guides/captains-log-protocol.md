# Captain's Log Protocol

To ensure continuous context, shared understanding, and process memory across sessions and personas:

1.  **Log Creation:** At the beginning of a new major task or session, Gemini will create a new log file in `system/session/logs/` following the convention `log-YYYYMMDD-XX-short-description.md`, where `XX` is a two-digit sequential number (01, 02, etc.) for logs created on that specific day.
2.  **Real-time Log Entries:** Throughout the session, for significant actions, decisions, forks in the plan, or important information, a new, concise entry will be appended to the current log file. Each entry will follow this format:
    ```
    ## YYYY-MM-DD HH:MM:SS [Persona: Name] [Type: Action/Decision/Fork/Info/Summary] [Tags: #tag1 #tag2]
    [Concise, single-line or very short summary of the event/update.]
    ```
    *   **Timestamp:** `YYYY-MM-DD HH:MM:SS` for precise chronological tracking.
    *   **Persona:** Indicates which persona (e.g., Default, Prompt Engineer) is making the entry.
    *   **Type:** Categorizes the entry (e.g., `Action`, `Decision`, `Fork`, `Info`, `Summary`).
    *   **Tags:** Short, descriptive hashtags for quick filtering and context.
    *   **Content:** Extremely concise, single-line or very short summary.
3.  **Log Review (by Personas):** When a persona (e.g., Prompt Engineer) is activated, its first action will be to review the latest session log to gain immediate context.
4.  **Session Summary & Archiving:** At the end of a session or major task, a final `[Type: Summary]` entry will be added to the log, providing a high-level overview.
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