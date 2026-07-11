---
type: workflow
id: report-writing-flow
title: Report Writing Flow
description: "Outline, draft sections, peer review, and format"
tags: [Production, Academic, Review, Writing]
connections:
  - target: report-intake
    type: uses
  - target: data-interpretation
    type: uses
  - target: llm-service
    type: runs_on
  - target: apa-7th-edition
    type: references
  - target: research-protocol-template
    type: references
  - target: thematic-coding-framework
    type: references
  - target: language-polish
    type: uses
  - target: evidence-claim-check
    type: uses
metadata:
  estimated_duration: "15-30 minutes"
  trigger: manual
output_step: "language-polish"
composite_steps:
  - "report-intake"
  - "data-interpretation"
  - "language-polish"
  - "evidence-claim-check"
execution:
  - skill: "report-intake"
    prompt: "report-brief"
    step_type: "synthesis"
    output: { name: "research_brief", type: "text" }
  - skill: "data-interpretation"
    prompt: "interpret-data"
    step_type: "synthesis"
    output: { name: "interpretation", type: "text" }
  - parallel:
    - skill: "evidence-claim-check"
      prompt: "check-evidence-claims"
      step_type: "review"
      output: { name: "evidence_report", type: "text" }
      context:
        evidence_rigour: "Standard"
  - skill: "language-polish"
    prompt: "polish-language"
    step_type: "content"
    output: { name: "polished_report", type: "text" }
    context:
      voice_profile: "Neutral professional tone"
      grammar_strictness: "Professional"
    bindings:
      source:
        from_step: "Data Interpretation"
        field: output
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
| `{{input.completed_draft_or_near}}` | No | Completed draft or near-final content, findings, or data to interpret and polish | `Paste your full draft, findings, or data here` |

These inputs are collected by the **report-intake** step, which assembles them into a structured brief that the interpretation, evidence-checking, and language-polish steps build on.

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
2. Review the included documents, assets, or source nodes and customize them to match your team, brand, or domain conventions where needed.
3. No specific AI provider or API key is required beyond your configured skrptiq LLM provider.

## Provider Notes

- Most stages work with any capable model; stronger models usually improve synthesis, judgement, and writing quality.
- Extraction, classification, and formatting steps generally run well on smaller or faster models.
- Because there are no vendor-specific integrations here, provider choice is mostly a trade-off between speed, quality, and cost.

## Example Input

To test this workflow immediately after import:

```
Research Topic: "The impact of remote working on team cohesion in UK tech startups"
Research Questions: "How does remote working affect team communication frequency? How does it shape informal knowledge-sharing?"
Methodology: "Qualitative case study with semi-structured interviews across six startups"
Completed Draft Or Near: "Interviews suggest cohesion holds where teams keep deliberate synchronous rituals, but informal knowledge-sharing drops sharply without them..."
```

