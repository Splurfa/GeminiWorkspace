# GitHub Synchronization Protocol

This protocol defines the process for synchronizing the local workspace with the GitHub repository, treating GitHub as a backup of the local file system. The local file system is always considered the single source of truth.

## I. Purpose

To provide a clear, non-interactive method for backing up the local workspace to GitHub.

## II. Trigger

This protocol is triggered when the user explicitly requests a "sync to GitHub" or similar phrasing (e.g., "push to GitHub," "backup to GitHub").

## III. Automated Synchronization Process

Upon receiving a trigger, Gemini will perform the following sequence of Git commands:

1.  **Stage All Changes:**
    ```bash
    git add .
    ```
    *   This command stages all modified, deleted, and newly created files in the local repository.

2.  **Commit Changes:**
    ```bash
    git commit -m "Automated backup sync: YYYY-MM-DD HH:MM:SS - [Brief summary of session work]"
    ```
    *   Gemini will automatically generate a commit message including a timestamp and a descriptive summary of the work completed in the current session. This commit message serves as the primary session log, detailing key actions, decisions, and outcomes.

3.  **Push to Remote Repository:**
    ```bash
    git push
    ```
    *   This command pushes all committed changes from the local repository to the configured remote GitHub repository.

## IV. Local as Source of Truth

It is critical to understand that the local file system remains the authoritative source of all data. GitHub serves solely as a remote backup.

## V. Non-Interactive Operation

This synchronization process is designed to be non-interactive. The user's command to "sync to GitHub" is considered explicit approval for the `git add`, `git commit`, and `git push` operations. Gemini will not prompt for further confirmation for these specific steps when this protocol is triggered.

## VI. Integration with Simplified Session Logging

This protocol works in conjunction with the [[simplified-session-log-protocol]]. The commit messages generated here serve as the primary session log, and any content in the optional internal session summary file will be included in the commit.
