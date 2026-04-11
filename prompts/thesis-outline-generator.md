---
type: prompt
id: thesis-outline-generator
title: Thesis Outline Generator
description: "Creates a detailed thesis or dissertation outline"
tags: [Production, Academic, Writing]
inputs:
  research_topic:
    label: "Research Topic"
    description: "The research area or question to investigate"
    example: "Machine learning applications in early disease detection"
    required: true
    type: text
  research_questions:
    label: "Research Questions"
    description: "The research questions guiding the study"
    example: "RQ1: What factors influence adoption? RQ2: How do outcomes vary by demographic?"
    required: true
    type: text
  methodology:
    label: "Methodology"
    description: "The research methodology"
    example: "Mixed methods: survey (n=200) + semi-structured interviews (n=15)"
    required: true
    type: text
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
{{input.research_topic}}

## Research Questions
{{input.research_questions}}

## Methodology
{{input.methodology}}
