---
type: workflow
id: report-writing-flow
title: Report Writing Flow
description: "Outline, draft sections, peer review, and format"
tags: [Production, Academic, Review, Writing]
connections:
  - target: report-intake
    type: uses
  - target: report-authoring
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
  - "report-authoring"
  - "language-polish"
  - "evidence-claim-check"
execution:
  - skill: "report-intake"
    prompt: "report-brief"
    step_type: "synthesis"
    output: { name: "research_brief", type: "text" }
    bindings:
      completed_draft_or_near:
        from_input: "completed_draft_or_near"
  - skill: "report-authoring"
    prompt: "outline-report"
    step_type: "synthesis"
    output: { name: "outline", type: "text" }
  - skill: "report-authoring"
    prompt: "draft-report"
    step_type: "content"
    output: { name: "draft", type: "text" }
    bindings:
      brief:
        from_step: "Report Intake"
        field: output
  - skill: "language-polish"
    prompt: "polish-report"
    step_type: "content"
    output: { name: "polished_report", type: "text" }
    context:
      voice_profile: "Neutral professional tone"
      grammar_strictness: "Professional"
  - parallel:
    - skill: "evidence-claim-check"
      prompt: "check-evidence-claims"
      step_type: "review"
      output: { name: "evidence_report", type: "text" }
      context:
        evidence_rigour: "Standard"
---

## Overview

This workflow produces a structured academic report or thesis chapter from a brief: it collects your topic, research questions, methodology, and any draft or data, generates a section outline, drafts the report in full prose, and polishes it into a publication-ready final. It **writes the report** — it does not merely review or summarize your input.

## Pipeline Stages

### Stage 1: Report Brief

**Input:** Research topic, research questions, methodology, and (optionally) a completed draft, findings, or data

The **report-intake** step (via the **report-brief** prompt) collects the inputs and assembles them into a single structured brief for the stages that follow.

**Output:** A structured research brief.

### Stage 2: Outline

**Input:** The report brief

The **report-authoring** skill (via the **outline-report** prompt) turns the brief into a section or chapter outline — headings, per-section purpose, key points to cover, and rough word targets.

**Output:** A structured section outline.

### Stage 3: Draft

**Input:** The outline, grounded in the original brief

The **report-authoring** skill (via the **draft-report** prompt) expands the outline into full drafted prose, section by section, grounded in the topic, research questions, methodology, and any supplied material.

**Output:** A complete drafted report.

### Stage 4: Language Polish

**Input:** The drafted report

The **language-polish** skill (via the **polish-report** prompt) polishes the draft for clarity, grammar, and consistency, producing the final report.

**Output:** The publication-ready report (the workflow's final output).

### Advisory: Evidence Check

Running alongside the final stage, the **evidence-claim-check** skill (via the **check-evidence-claims** prompt) flags claims in the report that may need stronger support or a citation. It is advisory and does not block the output.

## Error Handling

- If the outline lacks sufficient depth, provide more detail in the research questions and methodology and re-run
- If the draft drifts from the brief, tighten the brief inputs — the draft is grounded in what the brief carries
- If the evidence check flags unsupported claims, supply the missing sources or data as part of the draft input

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.research_topic}}` | Yes | The research topic for the thesis or report | `The impact of remote working on team cohesion in UK tech startups` |
| `{{input.research_questions}}` | Yes | The research questions guiding the report | `How does remote working affect team communication frequency?` |
| `{{input.methodology}}` | Yes | The research methodology used | `Qualitative case study with semi-structured interviews` |
| `{{input.completed_draft_or_near}}` | No | Completed draft, findings, or data to build the report on — paste text or upload a file (`.txt`, `.md`, `.docx`, `.pdf`) | `Paste your draft, or upload a .txt/.md/.docx/.pdf` |

These inputs are collected by the **report-intake** step, which assembles them into a structured brief that the outline, draft, and polish stages build on.

## Outputs

| Name | Description |
|------|-------------|
| Polished report | The publication-ready report — the workflow's final output |
| Section outline | The structured outline the draft was built from |
| Report draft | The full drafted report before polishing |
| Evidence report | Advisory list of claims that may need stronger support or citation |

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

