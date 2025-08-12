---
Title: "Signal 3: Tool Bias Over Chat Bias"
Tags:
  - #prompt-technique
  - #tool-usage
  - #agentic-ai
---

# Signal 3: Tool Bias Over Chat Bias

This signal highlights that GPT-5 is designed to proactively use its available tools rather than relying solely on its training data.

## The Signal

> Detailed tool policies for web, Python, Canvas, image generation, automations, memory—all first-class with specific usage rules.

## So What?

GPT-5 interprets ambiguous requests as opportunities for tool usage. For example, "Tell me about recent developments" will likely trigger a web search, and "show me the data" may trigger a Python analysis.

## How to Use It (Exploit)

Set explicit boundaries for tool usage in your prompt to control the AI's behavior.

### Example:

```
# To prevent tool use
No tools—reason from training knowledge only.

# To allow specific tool use
Web search limited to 2 academic sources.
```

---

[[../../1-Notes/projects/business/bx-os/nate-jones-article-synthesis-hub.md|Back to Synthesis Hub]]
