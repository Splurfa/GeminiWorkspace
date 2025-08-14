# Daily Note Atomization Protocol

## 1. Purpose

This protocol outlines the standardized process for deconstructing a completed daily note into a network of atomic notes. Its purpose is to transform the rich, synthesized content of a daily note into a web of interconnected, reusable ideas within your broader knowledge graph.

## 2. Trigger

This protocol is initiated when the user gives a clear command, such as: **"Atomize my daily note for [date]."**

## 3. The Atomization Process

This process treats the entire daily note as the source material for the [[atomic-notes-protocol]].

### Step 1: Source Identification

*   The source for this process is the daily note file specified by the user (e.g., `daily-note-2025-08-13.md`).

### Step 2: Synthesis Hub Creation

*   A new "synthesis hub" note will be created to serve as the map for the atomization process.
*   **Location:** `1-Notes/daily-notes/synthesis-hubs/` (a new sub-folder for these hubs)
*   **Naming:** `daily-note-synthesis-hub-YYYY-MM-DD.md`
*   **Content:** The hub note's metadata must adhere to the [[note-template-protocol]]. The `child_notes` field will be used to link to the newly created atomic notes. The body of the note should contain a link back to the original daily note.

### Step 3: Atomic Concept Extraction

*   I will read the *entire* content of the specified daily note, including the raw sources, structured insights, and the synthesized "Active Processing & Exploration" sections.
*   I will identify all potential atomic concepts, which could be:
    *   Key takeaways from articles or videos.
    *   New ideas or insights that you developed.
    *   Actionable experiments or workflow improvements.
    *   Core questions that emerged.
    *   Strategic connections between different topics.

### Step 4: Atomic Note Generation

*   For each concept identified, a new atomic note will be created in your library, following the structure defined in the [[atomic-notes-protocol]]. The `parent_note` field will link back to the synthesis hub.

### Step 5: Network Inter-linking

*   I will populate the `child_notes` field of the synthesis hub with wikilinks to all the newly created atomic notes.
*   I will then review the new atomic notes and add links *between* them in their `related_notes` field where appropriate, creating a web of related ideas.

## 4. Roles & Responsibilities

*   **User:** Initiates the process by providing the target daily note. You will then review the generated atomic notes and the synthesis hub to ensure they accurately reflect the day's insights.
*   **AI (Me):** I will execute the five steps of the atomization process, creating the necessary files and performing the inter-linking.
