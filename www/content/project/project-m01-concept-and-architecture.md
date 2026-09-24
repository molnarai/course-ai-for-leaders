---
title: 'M01'
date: 2026-10-03
due_date: 2026-10-03
weight: 10
draft: false
milestone: M01
description: 'Concept and architecture: the Study Buddy you intend to build, the learning behaviors you will prioritize, your planned workflows, and your evaluation plan.'
submission: 2026-10-03
percent: 10
---

## Purpose
This first review is about **framing and design**, not code. You should leave it with a credible plan and a clear scope, having settled which version of Study Buddy you are building and why it will genuinely help you learn.

The reviewers are looking for pedagogical ambition matched to a feasible architecture. A modest design you can finish and demonstrate well is worth more than an ambitious design you cannot build.

## What to Define
- **The version of Study Buddy you intend to build.** See [Choosing Your Design](../#choosing-your-design) for Versions A through F. You may combine elements, but say clearly what you are aiming at.
- **The main learning behaviors you will prioritize.** Pick the behaviors that matter most for how you actually study. You do not have to promise all of them.
- **Your planned workflows and how they interact.** Name each workflow, state its single responsibility, and show how a message flows through the system.
- **Your approach to course materials, retrieval, and memory.** What gets ingested, how it is chunked and tagged, what gets remembered across sessions.
- **Your prompting strategy and interface concept.** How the system decides to coach rather than answer, and what the experience looks like from the chat window.
- **Your evaluation plan.** How you will know whether the system is actually helping you think.

## Written Component: Three Workflow Pattern Briefs
Pick **three** of the [Workflow Patterns You Can Build](../#workflow-patterns-you-can-build) and describe how you picture each one helping you learn. Write one brief per pattern. Each brief, including its press release and requirements, must fit on **one page**.

Each brief has two parts.

### 1. Press Release
Write a short, high-level description as if the workflow had already launched and you were announcing it. Focus on the learner (you) and the benefit, not on the technology. A good press release includes:
- **Headline:** the workflow's name and the benefit in one line.
- **Subheading:** who it is for and what it helps them do, in one sentence.
- **The problem:** what is hard about learning this material today, or what habit gets in your way.
- **The solution:** what the workflow does and how it changes the way you study.
- **A quote from you as the learner:** how it felt to use it and what improved.
- **How to get started:** one or two sentences on when and how you would use it, such as before class, after a reading, or at the end of a session.

Aim for about half a page.

### 2. Requirements
List the **functional** and **non-functional** requirements for the workflow. Aim for about 4 to 8 functional and 3 to 5 non-functional requirements. See [Writing Functional and Non-Functional Requirements](#writing-functional-and-non-functional-requirements) at the bottom of this page for guidance.

## What to Show at the Review
- Problem framing and the target user (usually yourself, described concretely).
- Your initial design and architecture diagram.
- The proposed workflows, with roles and interactions.
- Initial prompts, even in draft form.
- Your data and materials plan.

## Expected Outcome
A credible design with clear scope.

## How This Review Is Evaluated
Problem framing, pedagogical ambition, architecture clarity, planned workflows, and feasibility. This review contributes **10%** of your project grade.

Against the [capability checklist](../#capability-checklist), you should be at: architecture *expected*; chat workflow, materials ingestion, and retrieval/memory *planned*; multiple workflows *proposed*; learning behaviors *proposed*; evaluation workflow *planned*; demonstration *outlined*; iteration *planned*.

## Submission Guidelines
- Open your project on GitLab https://git.insight.gsu.edu (VPN connection required)
- Navigate to the folder `documentation/Milestone_1`
- Upload your Markdown, PDF, or DOCX to the folder. Only one file for all three.

> See [Instructions to upload documents to GitLab](../../blog/upload-docs-to-gitlab/)

---

## Writing Functional and Non-Functional Requirements
Requirements turn your vision into statements you can build and test. They are split into two kinds.

### Functional Requirements
Functional requirements describe **what the workflow does**: its behaviors, inputs, outputs, and decisions. Ask yourself: *What should happen when I use it?*

Examples for a Socratic Response Workflow:
- **FR-1:** When I ask a conceptual question, the workflow responds with at least one diagnostic question before giving an explanation.
- **FR-2:** The workflow gives a direct explanation only after I have made at least one attempt at an answer, or after I explicitly ask for it.
- **FR-3:** Every explanation cites at least one retrieved passage from the course materials.
- **FR-4:** The workflow saves any misconception it detects to my learner profile.

### Non-Functional Requirements
Non-functional requirements describe **how well the workflow does it**: quality, tone, speed, reliability, privacy, and cost. Ask yourself: *What makes the experience good enough to actually use?*

Examples for the same workflow:
- **NFR-1:** Responses arrive within 10 seconds in normal use.
- **NFR-2:** The tone is encouraging and professional, never condescending.
- **NFR-3:** Responses stay under about 150 words unless I ask for more detail.
- **NFR-4:** Course materials and my learner profile are never shared outside my n8n environment.

### Tips for Writing Good Requirements
- **One requirement, one statement.** If a sentence contains "and," check whether it should be two requirements.
- **Make it testable.** You should be able to try it and say "yes, it does this" or "no, it doesn't." Replace vague words like *fast*, *helpful*, or *user-friendly* with something observable, such as *within 10 seconds*, *cites a source*, or *asks a question first*.
- **Describe what, not how.** "The workflow remembers my recurring mistakes" is a requirement. "Use a Postgres table with three columns" is a design decision and belongs in your architecture, not here.
- **Use consistent wording.** Start with "The workflow..." or "When I..., the workflow...", and use "must" or "should" consistently.
- **Number them** (FR-1, NFR-1, ...) so you can refer back to them later when you test and evaluate your Study Buddy.
- **Connect them to learning.** Each requirement should trace back to a benefit in your press release. If it doesn't, ask whether you need it.
