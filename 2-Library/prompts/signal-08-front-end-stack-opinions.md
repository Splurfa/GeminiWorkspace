---
Title: "Signal 8: Front-End Stack Opinions"
Tags:
  - #prompt-technique
  - #code-generation
  - #front-end-development
---

# Signal 8: Front-End Stack Opinions

This signal reveals that GPT-5 has opinionated defaults for code generation, specifically for front-end development.

## The Signal

> "Use Tailwind for styling, no import needed. All NPM libraries are available to use. Use shadcn/ui for basic components... Code should be production-ready with a minimal, clean aesthetic."

## So What?

Code generation comes with built-in preferences that produce high-quality, production-ready UI components without the need for manual dependency management.

## How to Use It (Exploit)

Lean into the model's opinions by specifying your requirements within its preferred stack. This will result in more robust and complete code.

### Example:

```
Task: Build a React component for user authentication.

Requirements:
- Use React, Tailwind, and shadcn/ui.
- Must be accessible (ARIA labels, keyboard navigation).
- Include dark mode support.
- Show loading states and error boundaries.
```

---

[[../../1-Notes/projects/business/bx-os/nate-jones-article-synthesis-hub.md|Back to Synthesis Hub]]
