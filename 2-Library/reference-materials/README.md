# Reference Materials

**Purpose:** This folder contains foundational and permanent reference documents, including major reports, datasets, and other materials that serve as a knowledge base for your work.

## Usage:

*   Files in this folder are considered "source-of-truth" materials.
*   Do not edit these files directly.
*   Reference these materials from other notes or documents as needed.

## Metadata for Reference Documents

To ensure consistent tracking and referencing, all new reference documents added to this folder should include the following YAML front matter at the very top of the Markdown file:

```yaml
---
Source: [URL of the original source, e.g., a website, paper, or book]
Date: [Date of publication or access in YYYY-MM-DD format]
Author: [Author(s) of the material, if applicable]
Related_Documents: [List of related document filenames, e.g., related-doc-1.md, related-doc-2.md]
---
```

**Example:**

```yaml
---
Source: https://natesnewsletter.substack.com/p/beyond-the-chat-12-specialist-ai
Date: 2025-08-05
Author: Nate Jones
Related_Documents: [nate-jones-ai-tools-supplement.md]
---
```