# Atomic Notes Synthesis Protocol

## 1. Purpose

This protocol outlines a standardized process for synthesizing long-form content (e.g., articles, documents, transcripts) into a network of "atomic notes." The goal is to deconstruct a single, large piece of information into its core, reusable concepts, making them easier to understand, connect, and utilize in future work. This transforms a static library of articles into a dynamic, interconnected knowledge graph.

## 2. The Process

The synthesis process consists of five main steps, moving from a single source document to a web of interconnected, atomic ideas.

### Step 1: Ingest and Standardize the Source

Before synthesis can begin, the source material must be processed and stored in a standardized format within your library.

1.  **Convert to Markdown:** Convert the source material (e.g., from RTF, PDF, web page) into a clean Markdown file.
2.  **Add Metadata:** Add a YAML frontmatter block to the top of the Markdown file, following the [[note-template-protocol]]. The `status` should be set to `evergreen` and the `source` field should be filled out.
3.  **Store in Library:** Save the formatted Markdown file to the `2-Library/reference-materials/` directory.

### Step 2: Create the Synthesis Hub Note

This note is the central map for the synthesized content.

1.  **Create the Hub Note:** In the relevant project folder (e.g., `1-Notes/projects/business/bx-os/`), create a new note named `[source-title]-synthesis-hub.md`.
2.  **Structure the Hub Note:** The hub note must follow the [[note-template-protocol]].
    *   The `title` should be `[Source Title] - Synthesis Hub`.
    *   The `status` should be `evergreen`.
    *   The `child_notes` field will be used to link to the newly created atomic notes.
    *   The body of the note should contain a brief **Summary** of the source material's core thesis, a section for **Key Concepts**, and a link to the full source article in the library.

### Step 3: Identify and Extract Atomic Concepts

With the hub note in place, systematically read through the source material to identify the core, self-contained ideas. An "atomic concept" is an idea that can be understood on its own.

*   Examples: A specific prompting technique, a key philosophical principle (like "Bias to Ship"), a comparison between two tools, a mental model.

### Step 4: Create an Atomic Note for Each Concept

For each concept identified, create a new, separate Markdown file.

1.  **Naming Convention:** Name the file clearly and concisely in kebab-case (e.g., `signal-01-delegated-initiative.md`, `concept-bias-to-ship.md`).
2.  **Location:**
    *   Actionable templates or prompts go in `2-Library/prompts/`.
    *   General concepts, frameworks, or reference-style notes go in `2-Library/reference-materials/`.
3.  **Structure of an Atomic Note:** Each atomic note must follow the [[note-template-protocol]].
    *   The `title` should be the name of the concept.
    *   The `status` should be `evergreen`.
    *   The `parent_note` field must link back to the Synthesis Hub note.
    *   The body of the note should contain a **Core Definition**, a **Detailed Explanation**, and **Actionable Advice** (if applicable).

### Step 5: Inter-link the Network

The final step is to connect the notes.

1.  **Update the Hub Note:** Populate the "Key Concepts" and "Actionable Techniques" sections of the hub note with `[[wikilinks]]` to the newly created atomic notes.
2.  **Link Between Atomic Notes:** Where relevant, add wikilinks *between* atomic notes to show relationships between different concepts.

---

This protocol ensures that every piece of long-form content you find valuable is not just stored, but fully integrated into your personal knowledge system.
