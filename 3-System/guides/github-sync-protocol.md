# GitHub Synchronization Protocol

This protocol defines the process for synchronizing the local workspace with the GitHub repository, treating GitHub as a backup of the local file system. The local file system is always considered the single source of truth.

## I. Purpose

To provide a clear, non-interactive method for backing up the local workspace to GitHub.

## II. Trigger

This protocol is triggered when the user explicitly requests a "sync to GitHub" or similar phrasing (e.g., "push to GitHub," "backup to GitHub") outside of the Captain's Log update process.

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
    *   Gemini will automatically generate a commit message including a timestamp and a brief, inferred summary of the work completed in the current session. This commit message will be concise and focused on the backup purpose.

3.  **Push to Remote Repository:**
    ```bash
    git push
    ```
    *   This command pushes all committed changes from the local repository to the configured remote GitHub repository.

## IV. Local as Source of Truth

It is critical to understand that the local file system remains the authoritative source of all data. GitHub serves solely as a remote backup.

## V. Non-Interactive Operation

This synchronization process is designed to be non-interactive. The user's command to "sync to GitHub" is considered explicit approval for the `git add`, `git commit`, and `git push` operations. Gemini will not prompt for further confirmation for these specific steps when this protocol is triggered.

## VI. Integration with Captain's Log Protocol

When a Captain's Log entry is created or amended (as per `captains-log-protocol.md`), Gemini will *still* prompt the user for GitHub sync approval (as per `captains-log-protocol.md` sections 1.7 and 2.9). If approved in that context, the same `git add`, `git commit`, `git push` sequence will be executed. This `github-sync-protocol.md` defines the *mechanics* of that sync.
