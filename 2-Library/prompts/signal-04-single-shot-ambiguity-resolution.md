---
Title: "Signal 4: Single-Shot Ambiguity Resolution"
Tags:
  - #prompt-technique
  - #ambiguity-resolution
  - #agentic-ai
---

# Signal 4: Single-Shot Ambiguity Resolution

This signal explains that GPT-5 will only ask one clarifying question before committing to a course of action.

## The Signal

> Only one clarifying question permitted before execution begins.

## So What?

If you don't provide key assumptions upfront, the model will make its own best guess and execute fully based on that guess. A wrong assumption can lead to a completely wrong deliverable.

## How to Use It (Exploit)

Front-load your prompts with all the necessary decision variables to remove ambiguity.

### Example:

```
Assumptions: 
- B2B SaaS
- North American market
- Technical audience

Non-goals: 
- Consumer applications
- International markets
```

---

[[../../1-Notes/projects/business/bx-os/nate-jones-article-synthesis-hub.md|Back to Synthesis Hub]]
