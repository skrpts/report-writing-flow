---
type: workflow
id: report-writing-flow
title: Report Writing Flow
description: "Outline, draft sections, peer review, and format"
tags: [Production, Academic, Review, Writing]
connections:
  - target: thesis-outline-generator
    type: uses
  - target: abstract-writer
    type: uses
  - target: peer-review-draft
    type: uses
  - target: data-interpretation
    type: uses
  - target: llm-service
    type: runs_on
  - target: apa-7th-edition
    type: references

metadata:
  estimated_duration: "15-30 minutes"
  trigger: manual
---

## Overview

This workflow guides the production of a structured academic report or thesis chapter, from initial outlining through to peer-reviewed final draft. It combines structural planning with iterative review to produce publication-ready academic writing.

## Pipeline Stages

### Stage 1: Thesis Outline

**Input:** Research topic, research questions, methodology

Invoke the **thesis-outline-generator** prompt to produce a chapter-by-chapter outline with section breakdowns, word count targets, and key sources to engage with.

**Output:** Detailed structural outline.

### Stage 2: Abstract & Summary

**Input:** Completed draft or near-final content

Invoke the **abstract-writer** prompt to produce a structured abstract covering background, objective, methods, results, and conclusion.

**Output:** Publication-ready abstract (200–300 words).

### Stage 3: Peer Review

**Input:** Complete manuscript draft

Invoke the **peer-review-draft** prompt to generate constructive feedback covering strengths, major concerns, minor concerns, and a recommendation.

**Gate:** Major concerns must be addressed before proceeding.

**Output:** Annotated review with specific improvement suggestions.

### Stage 4: Data Analysis

**Input:** Research data, statistical outputs, qualitative coding summaries

Invoke the **data-interpretation** skill to identify patterns, assess significance, and suggest follow-up analyses for the results section.

**Output:** Interpretive summary for incorporation into the report.

## Error Handling

- If the outline lacks sufficient depth, provide more detail on the research questions and methodology
- If peer review flags fundamental structural issues, return to Stage 1 rather than patching
- If data interpretation reveals unexpected findings, consider whether they warrant revising the research questions

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.research_topic}}` | Yes | The research topic for the thesis or report | `The impact of remote working on team cohesion in UK tech startups` |
| `{{input.research_questions}}` | Yes | The research questions guiding the report | `How does remote working affect team communication frequency?` |
| `{{input.methodology}}` | Yes | The research methodology used | `Qualitative case study with semi-structured interviews` |
| `{{input.completed_draft_or_near}}` | No | Completed draft or near-final content for abstract writing and peer review | `Paste your full draft here` |

## Outputs

| Name | Description |
|------|-------------|
| Detailed structural outline | Detailed structural outline |
| Publication-ready abstract | Publication-ready abstract |
| Annotated review | Annotated review with specific improvement suggestions |
| Interpretive summary for incorporation into the report | Interpretive summary for incorporation into the report |

## Setup

Before running this workflow:

1. No external services required — paste your content directly and provide any supporting context as inputs or source nodes.
2. Review the included documents, assets, or source nodes and customise them to match your team, brand, or domain conventions where needed.
3. No specific AI provider or API key is required beyond your configured skrptiq LLM provider.

## Provider Notes

- Most stages work with any capable model; stronger models usually improve synthesis, judgement, and writing quality.
- Extraction, classification, and formatting steps generally run well on smaller or faster models.
- Because there are no vendor-specific integrations here, provider choice is mostly a trade-off between speed, quality, and cost.

## Example Input

To test this workflow immediately after import:

```
Research Topic: "Paste the relevant brief, notes, source material, or dataset here."
Research Questions: "Paste the relevant brief, notes, source material, or dataset here."
Methodology: "Paste the relevant brief, notes, source material, or dataset here."
Completed Draft Or Near: "Paste the relevant brief, notes, source material, or dataset here."
```

