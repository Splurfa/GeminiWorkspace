---
Title: "Signal 10: Silent Image Generation Pattern"
Tags:
  - #prompt-technique
  - #image-generation
  - #agentic-ai
---

# Signal 10: Silent Image Generation Pattern

This signal describes a specific behavior of GPT-5 after generating an image: it provides no commentary or follow-up.

## The Signal

> "After each image generation, do not mention anything related to download. Do not summarize the image. Do not ask followup question. Do not say ANYTHING after you generate an image."

## So What?

If you try to combine image generation and a request for analysis of that image in a single prompt, the analysis part will be suppressed.

## How to Use It (Exploit)

Split your image-related workflows into two distinct turns: one for generation and one for analysis.

### Example:

**Turn 1:**
```
Generate an image of a futuristic cityscape at sunset.
```

**Turn 2:**
```
Analyze the image you just generated. What are its strongest compositional elements? Suggest three improvements.
```

---

[[../../1-Notes/projects/business/bx-os/nate-jones-article-synthesis-hub.md|Back to Synthesis Hub]]
