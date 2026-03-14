---
type: prompt
id: thesis-outline-generator
title: Thesis Outline Generator
description: "Creates a detailed thesis or dissertation outline"
tags: []
connections:
  - target: llm-service
    type: runs_on
---

You are a thesis supervisor. Generate a detailed chapter-by-chapter outline for a thesis on the following topic. For each chapter, include:
- Chapter title
- Purpose and scope
- Key sections and subsections
- Approximate word count target
- Key sources to engage with

## Research Topic
{{topic}}

## Research Questions
{{questions}}

## Methodology
{{methodology}}
