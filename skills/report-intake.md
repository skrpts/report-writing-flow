---
type: skill
id: report-intake
title: Report Intake
description: "Collects the report topic, questions, methodology, and draft into a single structured brief"
tags: [Production, Academic, Writing]
connections:
  - target: llm-service
    type: runs_on
---

## Capability

Gathers the report inputs — research topic, research questions, methodology, and any completed draft, findings, or data — and organizes them into a single structured brief. The brief becomes the shared starting point for the downstream interpretation, evidence-checking, and language-polish steps, so the user's inputs actually flow through the pipeline.

## When to Use

- At the start of a report-writing run, to capture the brief before any analysis
- When several inputs must be consolidated into one coherent hand-off for later steps

## Inputs

Research topic, research questions, methodology, and (optionally) a completed draft, findings, or data.

## Outputs

A structured research brief: topic, research questions, methodology, a summary of the supplied material and its stage, and any flagged gaps.
