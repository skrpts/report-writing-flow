---
type: prompt
id: interpret-data
title: "Interpret Research Data"
description: "Identifies patterns, trends, and contradictions across research findings"
tags: [Production, Academic, Research]
inputs:
  research_data:
    label: "Research Data"
    description: "The research findings, data, or source material to interpret"
    example: "Paste your research data or findings here"
    required: true
    type: file
    accept: ".txt,.md,.csv,.docx,.pdf"
  report_topic:
    label: "Report Topic"
    description: "The topic or question this report addresses"
    example: "Impact of remote work on team productivity across distributed engineering teams"
    required: true
    type: text
inputs:
  research_data:
    label: "Research Data"
    description: "The research findings, data, or source material to interpret"
    example: "Paste your research data or findings here"
    required: true
    type: file
    accept: ".txt,.md,.csv,.docx,.pdf"
  report_topic:
    label: "Report Topic"
    description: "The topic or question this report addresses"
    example: "Impact of remote work on team productivity across distributed engineering teams"
    required: true
    type: text
connections:
  - target: data-interpretation
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Drives the data interpretation skill.

## Prompt

You are a research analyst. Interpret the findings below, identifying patterns and building a synthesis.

### Research Findings

**Topic:** {{input.report_topic}}

### Research Data

{{input.research_data}}

### Analysis

**Topic:** {{input.report_topic}}

### Research Data

{{input.research_data}}

### Analysis

{{steps.previous.output}}

### Instructions

1. **Pattern identification** — what themes or trends appear across multiple findings?
2. **Contradictions** — where do findings disagree? What might explain the inconsistency?
3. **Strength of evidence** — which findings are well-supported and which rely on limited evidence?
4. **Gaps** — what questions remain unanswered by these findings?
5. **Synthesis** — what overall narrative emerges from the combined findings?

### Output Format

**Key Themes** (3-5 themes with supporting evidence from multiple findings)

**Contradictions and Tensions** (where findings conflict, with possible explanations)

**Evidence Assessment** (which conclusions are strong vs. tentative)

**Remaining Questions** (what further research would address)

**Synthesis** (one-paragraph summary of the state of knowledge based on these findings)

## Formatting Rules

- Use British English throughout
- Be specific and actionable — no vague recommendations
- Structure output clearly with headings, tables, or lists as appropriate
