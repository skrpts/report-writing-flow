---
type: prompt
id: report-brief
title: "Report Brief"
description: "Collects the research topic, questions, methodology, and draft for the report"
tags: [Production, Academic, Writing]
inputs:
  research_topic:
    label: "Research Topic"
    description: "The research topic for the thesis or report"
    example: "The impact of remote working on team cohesion in UK tech startups"
    required: true
    type: string
  research_questions:
    label: "Research Questions"
    description: "The research questions guiding the report"
    example: "How does remote working affect team communication frequency?"
    required: true
    type: string
  methodology:
    label: "Methodology"
    description: "The research methodology used"
    example: "Qualitative case study with semi-structured interviews"
    required: true
    type: string
  completed_draft_or_near:
    label: "Completed Draft or Near-Final Content"
    description: "Completed draft, findings, or data to build the report on — paste text or upload a file"
    example: "Paste your draft, or upload a .txt/.md/.docx/.pdf"
    required: false
    type: file
    accept: ".txt,.md,.docx,.pdf"
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Collects the report inputs and assembles them into a single structured brief that the downstream outline, draft, and polish stages build on.

## Prompt

You are a research editor preparing a report brief. Organize the material below into a clear, structured brief that a research analyst can work from. Do not analyze or rewrite the content — restate it faithfully and flag anything missing.

### Research Topic

{{input.research_topic}}

### Research Questions

{{input.research_questions}}

### Methodology

{{input.methodology}}

### Draft, Findings, or Data

{{step.context.completed_draft_or_near}}

### Instructions

1. **Restate the brief** — present the topic, research questions, and methodology as a tidy summary, preserving the author's wording and intent.
2. **Frame the material** — summarize what the supplied draft, findings, or data covers, and note its apparent stage (early notes, near-final draft, raw data, and so on).
3. **Flag gaps** — if any required element is thin or the draft is absent, say so plainly so downstream steps can compensate.

### Output Format

**Topic** (one or two sentences)

**Research Questions** (as a list)

**Methodology** (concise description)

**Material Summary** (what the draft, findings, or data contains, and its stage)

**Gaps and Notes** (anything missing or requiring attention)

## Formatting Rules

- Use American English throughout
- Preserve the author's meaning — do not editorialize or add claims
- Structure the output clearly with headings and lists
