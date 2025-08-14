# Simplified Session Log Protocol

This protocol defines a streamlined approach to logging session work, leveraging existing Git processes for efficiency and consistency.

## I. Purpose

To provide a simple, automated, and auditable record of work performed during a session, integrated directly with the project's version control history.

## II. Primary Session Log: Git Commit Messages

The primary record of session work will be the commit messages generated during the GitHub synchronization process, as defined in the [[github-sync-protocol]].

*   **Automation:** Each time a `git push` is performed (typically at the end of a session or significant checkpoint), a commit message will automatically summarize the work.
*   **Content:** Commit messages will be concise but descriptive, highlighting key actions, decisions, and outcomes since the last commit.

## III. Optional Internal Session Summary

For more detailed notes or specific points that may not fit into a concise commit message, an optional internal session summary can be maintained.

*   **File:** `3-System/session-logs/current-session-summary.md`
*   **Mechanism:**
    *   During a session, you can instruct the AI (me) to "add to session summary" followed by the bullet point you wish to add.
    *   I will append a timestamped bullet point to `current-session-summary.md`.
    *   This file will be automatically staged and committed with the regular GitHub sync.
*   **Lifecycle:**
    *   At the start of a new session, the `current-session-summary.md` can be cleared or archived (e.g., moved to a dated file in `3-System/session-logs/archive/`) to start fresh.

## IV. Deprecation of Old Protocol

The previous `captains-log-protocol.md` has been deprecated and moved to `4-Archive/old-protocols/` to simplify the system.
