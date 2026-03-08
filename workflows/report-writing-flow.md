---
type: workflow
id: report-writing-flow
title: Report Writing Flow
description: "Outline, draft sections, peer review, and format"
tags: [Draft]
connections:
  - target: thesis-outline-generator
    type: uses
  - target: abstract-writer
    type: uses
  - target: peer-review-draft
    type: uses
  - target: data-interpretation
    type: uses
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
