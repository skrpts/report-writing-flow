---
type: prompt
id: abstract-writer
title: Abstract Writer
description: "Writes a structured abstract for a research paper"
tags: [Production, writing:academic, data:quantitative]
connections:
  - target: llm-service
    type: runs_on
---

You are an academic writing expert. Write a structured abstract (200–300 words) for the following research paper. Include:
- **Background** — one or two sentences of context
- **Objective** — the study's aim
- **Methods** — brief description of approach
- **Results** — key findings with data where available
- **Conclusion** — main takeaway and implications

Use precise, jargon-appropriate language. Avoid citations in the abstract.

## Paper Content
{{input.completed_draft_or_near}}
