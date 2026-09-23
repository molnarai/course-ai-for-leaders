---
title: Project
description: "The semester project is to design and build a Study Buddy: an agentic AI learning partner that helps you prepare for class, test your understanding, apply course ideas to your own work, and improve over time. You build it in your own n8n environment using LLMs, web search, document storage, and a vector database, and you develop it across four reviews that carry increasing weight toward your project grade. The project rewards the quality of your learning design, the clarity of your workflow architecture, the strength of your prompts, and the evidence that you tested and improved the system, more than it rewards decorative complexity."
layout: "project"
---
<!-- **[Guidelines for Final Project Presentation](project-final-presentation/)** -->

<!-- **Project Assignment: Building an AI-Powered Business Solution** -->
### Purpose
The semester project is to design and build a [**Study Buddy**](../blog/study-buddy/), an agentic AI learning partner that helps you prepare for class, test understanding, apply course ideas, and improve over time. The goal is not to build a chatbot that gives polished answers on demand. The goal is to build an AI system that helps you think better, diagnose better, and participate better in class.

The strongest Study Buddy will act like a persistent coach. It should ask good questions, challenge weak reasoning, help you connect ideas across readings and courses, and adapt to your recurring strengths and weaknesses.

### Project Context
You will build your own version of Study Buddy inside your personal n8n environment. You may work in teams to explore ideas, test approaches, and share design patterns, but **you must build, document, evaluate, and demonstrate your own agents and workflows**.

You are provided with:
- n8n for workflow and agent orchestration.
- Access to LLMs.
- SearXNG for internet search.
- CubeFS for document storage and file access through a provided file-management tool.
- PostgreSQL with pgvector for structured storage, memory, and retrieval-augmented generation.
- Starter examples for a simple AI agent, a document-processing pipeline, and a chat-evaluation pipeline.

### Design Principle
The governing principle for this project is:

> **Do not let your Study Buddy do for you what you need to learn to do.**

Your Study Buddy should improve your judgment, not replace it. A strong system should challenge, coach, probe, and adapt. It should avoid becoming a summary vending machine.

### What Study Buddy Should Do
At minimum, your Study Buddy should support a simple chat-centered learning experience with access to course materials and your own context. The system should make it easy for you to work with:
- Course Materials.
- My Materials.
- My Profile or Memory.

The user experience should be simple. You should not need to manually manage a technical database or tune a retrieval system by hand. Your design should keep the interface lightweight while hiding the complexity behind well-designed workflows.

### Required Learning Behaviors
Your Study Buddy should demonstrate several high-value learning behaviors. Your implementation does not need to use these exact labels in the interface, but the behaviors should be clearly present.

Required behaviors include:
- **Preparation coaching:** Help you get ready for class through questions, checks, and targeted practice rather than immediate summary.
- **Concept mastery checking:** Diagnose what you actually understand and where you are weak.
- **Application practice:** Generate cases, scenarios, managerial situations, or decision contexts that require use of course concepts.
- **Challenge mode:** Push back on premature conclusions and test alternative explanations.
- **Cross-reading or cross-course synthesis:** Help you connect ideas, compare frameworks, and identify tensions or boundary conditions.
- **Persistent improvement:** Use memory or profile mechanisms to track recurring strengths, weaknesses, or patterns over time.

### Example Uses
A strong Study Buddy should be able to support interactions such as:
- “Prepare me for class tomorrow.”
- “Quiz me on the readings.”
- “Help me apply this concept to a managerial situation.”
- “Challenge my interpretation.”
- “Help me connect these readings.”
- “Help me come up with something worth saying in class.”
- “Use my own work experience to interpret this topic.”
- “Give me an integrative problem that uses several topics at once.”

### Functional Requirements
Your final project must include multiple working workflows or agents. At minimum, your solution should include:

1. **A conversational Study Buddy workflow** that manages dialogue and chooses an appropriate coaching behavior.
2. **A materials-ingestion workflow** that accepts and processes course resources such as syllabi, readings, notes, transcripts, or cases.
3. **A retrieval or memory workflow** using Postgres/pgvector, structured memory, or an equivalent design that supports persistence and personalization.
4. **An evaluation workflow** that tests or reviews agent responses, conversation quality, or learning behavior.
5. **At least one advanced workflow** beyond the starter examples, such as synthesis generation, challenge-mode branching, class-prep coaching, scenario generation, weakness tracking, or evidence-based feedback.

### Technical Expectations
You will not build these workflows from scratch. We will provide **working n8n templates** for the core workflows. Each template runs out of the box with default behavior.

Your job is to make them your own:
- **Required: customize behavior through system prompts.** Rewrite the system prompts to define your Study Buddy's role, coaching style, tone, and how it uses course materials and memory. This is where most of your design work will show.
- **Optional: change the workflow structure.** If you are comfortable, you can also add, remove, or rewire nodes. For example, you might add a branching step, a new tool, or an extra workflow. This is not required, but it is a way to go further.

Your final project should show:
- Clear, deliberate system prompts for each workflow you use.
- Course materials loaded and retrieved in a way that supports your design.
- Memory that carries over between conversations.
- Each workflow playing a clear role in the overall system.
- Evidence that you tested your Study Buddy and improved it based on what you saw.

---

## Choosing Your Design

There is no single correct Study Buddy. The sections below describe viable versions of the project and the dimensions along which they differ. Use them to choose a scope you can actually finish and demonstrate well.

### Design Dimensions
Your version can sit anywhere along these dimensions. You do not need to be at the high-complexity end of every row.

| Dimension | Lower-complexity option | Higher-complexity option |
|---|---|---|
| Interaction style | Single chat agent | Routed multi-workflow coach |
| Knowledge access | Basic RAG over uploaded files | Hybrid retrieval with metadata, memory, and task-based retrieval |
| Personalization | Session-only context | Persistent learner profile and weakness tracking |
| Pedagogy | Q&A and summaries | Socratic coaching, challenge mode, and adaptive practice |
| Evaluation | Manual spot checks | Automated conversation and response evaluation pipeline |
| Architecture | Monolithic workflow | Specialized workflows/agents with orchestration |

Because you have LLMs, web search, document storage, a vector database, and an orchestration platform, you can build well beyond basic RAG. You can combine workflow routing, memory, self-evaluation, retrieval, critique, and targeted study behaviors without building a custom software stack from scratch.

<details>
<summary><strong>Version A: Basic Course Study Buddy</strong></summary>

The minimum credible version. It uses uploaded course documents, a vector store, and a single conversational workflow that can answer questions and perform simple quizzes.

Core features:
- Upload and process course materials.
- Retrieve relevant passages.
- Maintain a simple chat history.
- Offer short quizzes or concept checks.

Best use: a lower-complexity implementation, or a baseline you extend later.

</details>

<details>
<summary><strong>Version B: Socratic Coach</strong></summary>

This version centers on learning behavior rather than retrieval alone. The chat workflow classifies your intent and responds with questioning strategies instead of immediate explanation.

Core features:
- Intent detection such as prepare, quiz, apply, challenge, synthesize.
- Prompting strategies that delay answers and ask diagnostic questions first.
- Selective reveal of explanation after you have made a genuine attempt.
- Feedback on the quality of your reasoning.

Best use: aligns most directly with the design principle above.

</details>

<details>
<summary><strong>Version C: Persistent Personal Tutor</strong></summary>

This version adds memory and adaptation. The system stores observations about you across time, such as repeated conceptual gaps, overreliance on one kind of explanation, or difficulty with application.

Core features:
- A learner profile with strengths, weaknesses, preferences, and history.
- Conversation summaries written to Postgres.
- Weakness tags or competency tags.
- Adaptive prompt strategies based on prior performance.

Best use: demonstrates persistence and personalized coaching.

</details>

<details>
<summary><strong>Version D: Case and Application Coach</strong></summary>

This version emphasizes application to managerial situations and course cases.

Core features:
- Case upload or retrieval.
- Scenario generation from current course concepts.
- Role-play or diagnosis prompts.
- Follow-up critique that compares your diagnosis with plausible alternatives.

Best use: when discussion quality, diagnosis, and managerial action matter more than recall.

</details>

<details>
<summary><strong>Version E: Cross-Course Integrator</strong></summary>

This version helps you connect ideas across courses in the EMBA program.

Core features:
- Course tagging and metadata on materials.
- Retrieval across courses, not only within one class.
- Prompts that compare frameworks, identify contradictions, and surface complementary lenses.
- Integrative problem generation that combines multiple subjects.

Best use: program-level learning and late-semester synthesis.

</details>

<details>
<summary><strong>Version F: Multi-Agent Workflow System</strong></summary>

This version explicitly decomposes roles across several workflows or agents.

Possible agent/workflow roles:
- Planner/router.
- Retriever.
- Socratic coach.
- Quiz generator.
- Case generator.
- Critic/evaluator.
- Learner-model updater.

Best use: demonstrates orchestration and workflow design maturity. Attempt this only if you are confident you can keep it reliable.

</details>

---

## Workflow Patterns You Can Build

You already receive a simple agent, a document pipeline, and a chat evaluation pipeline. The patterns below go beyond that plumbing and emphasize learning design. Pick the ones that fit your chosen version.

1. **Intent Router for Study Modes** — Detects whether you want preparation, quiz, challenge, synthesis, application, or reflection, and routes to different prompt templates and downstream workflows.
2. **Socratic Response Workflow** — Takes your question and responds with diagnostic or probing questions first, delaying direct explanation until you have shown sufficient effort.
3. **Case/Scenario Generator** — Uses course concepts plus uploaded materials to generate a realistic managerial situation, optionally with rubric fields such as concept targets, difficulty, and likely misconceptions.
4. **Weakness Tracker and Profile Updater** — Summarizes a conversation and writes structured observations to Postgres, tracking recurring errors, missed concepts, or reasoning habits.
5. **Class Preparation Coach** — Uses the materials assigned for a given date or topic and produces a readiness conversation with checks, gaps, and suggested class contributions.
6. **Cross-Reading Synthesizer** — Retrieves multiple readings, asks you to propose connections first, then generates prompts about complementarities, contradictions, assumptions, and boundary conditions.
7. **Challenge / Devil's Advocate Workflow** — Takes your interpretation and systematically tests alternative explanations or counterarguments.
8. **Evidence Checker** — Reviews an agent response or a claim and verifies whether it is grounded in retrieved materials, memory, or external search. Helps discourage hallucinated confidence.
9. **Reflection Workflow** — At the end of a session, prompts you to reflect on what changed in your understanding, and saves a concise reflection plus next-step recommendations.
10. **Demonstration Capture Workflow** — Creates a structured transcript, summary, or scorecard from a demo session. Useful for milestone reviews.

### A Reference Architecture
A practical pattern that works for many projects:

- CubeFS stores files and source documents.
- A document-processing workflow extracts text, chunks it, stores embeddings in Postgres/pgvector, and attaches metadata such as course, module, topic, source type, and date.
- A main chat workflow receives the message.
- A lightweight intent router chooses the study mode.
- Retrieval, memory lookup, and prompt assembly occur based on that mode.
- A response-generation step produces a coaching response.
- An evaluation or reflection workflow reviews the session and updates the learner profile.

### A Note on Scope
Do not push yourself toward unnecessary complexity. A polished, well-tested Socratic coach with persistent memory and three to five strong workflows is better than an unreliable swarm of agents.

**Prefer fewer workflows with strong learning behaviors over many weak features.**

At minimum, your final system should include:
- Three to five meaningful workflows.
- One document/materials workflow.
- One conversation workflow.
- One evaluation or critique workflow.
- One personalization, memory, or learner-model feature.
- One realistic demonstration with several use cases.

---

## Deliverables
You must submit:
- A working n8n-based Study Buddy system with multiple workflows.
- A short architecture overview with workflow descriptions.
- Prompt designs or system-instruction designs for the major agents/workflows.
- A description of how course materials, memory, and retrieval are handled.
- An evaluation plan with examples of tests or review criteria.
- A demonstration showing how the system is used in realistic study situations.
- A brief reflection describing what improved over time and what still remains limited.

---

## Milestones and Reviews

The project runs across four reviews. Each review contributes to your project grade, so early progress and responsiveness to feedback matter, while the final system still carries the most weight.

Each milestone page below states what to deliver, what to show at the review, and the criteria that review is graded on. Due dates and grade weights are in the milestone table at the bottom of this page.

### Capability Checklist
Use this table to judge whether you are on track at each review.

<details>
<summary><strong>Show the capability checklist</strong></summary>

| Capability | M01 | M02 | M03 | M04 |
|---|---|---|---|---|
| Problem framing and architecture | Expected | Refined | Stable | Finalized |
| Chat workflow | Planned | Working | Improved | Polished |
| Materials ingestion | Planned | Working | Improved | Polished |
| Retrieval or memory | Planned | Baseline | Improved | Integrated |
| Multiple workflows | Proposed | At least 2 | At least 3 to 4 | Coherent portfolio |
| Learning behaviors | Proposed | At least 1 strong behavior | Several behaviors | Integrated and adaptive |
| Evaluation workflow | Planned | Baseline | Working and informative | Used in final analysis |
| Demonstration quality | Outline | Early demo | Stronger demo | Final polished demo |
| Iteration evidence | Plan | Initial revisions | Clear improvement | Strong reflective analysis |

</details>

---

## Grading

Your project is evaluated on how well your Study Buddy supports learning, how thoughtfully your workflows are designed, and how clearly you demonstrate and improve the system over time. Prompt quality, ingenuity, evaluation, and realistic demonstration count for more than decorative complexity. Bells and whistles count, but they do not dominate.

### Grading Categories
The rubric uses 100 points total.

| Category | Weight | What is being judged |
|---|---:|---|
| Learning design and pedagogy | 25 | Does the system help you think, diagnose, apply, and improve rather than just answer? |
| Workflow architecture and implementation | 20 | Are there multiple coherent workflows or agents with clear responsibilities and reliable behavior? |
| Prompt quality and orchestration | 15 | Are prompts well designed, purposeful, and adapted to task or mode? |
| Retrieval, memory, and data use | 10 | Does the project use materials, memory, retrieval, or structured context effectively? |
| Evaluation and iterative improvement | 15 | Is there evidence of testing, critique, analysis, and revision over time? |
| Demonstration and use cases | 10 | Do you convincingly show realistic use and explain the value? |
| Polish and advanced features | 5 | Are there useful refinements, interface quality, or technically interesting extensions? |

### Detailed Rubric

<details>
<summary><strong>Show the full rubric</strong></summary>

| Category | Excellent | Good | Developing | Weak |
|---|---|---|---|---|
| Learning design and pedagogy (25) | System consistently coaches, challenges, and adapts; clearly improves your thinking | Often supports learning well, though some behaviors are uneven | Shows some coaching behavior but often falls back to direct answering | Mostly a generic chatbot with little learning design |
| Workflow architecture and implementation (20) | Multiple workflows are distinct, integrated, and reliable | Several workflows work well with minor gaps | Some workflows exist but integration is weak or fragile | Minimal workflow design; mostly one path or unreliable automation |
| Prompt quality and orchestration (15) | Prompts are precise, mode-aware, and pedagogically strong | Prompts are mostly good with some generic sections | Prompts work but are shallow or inconsistent | Prompting is weak, generic, or poorly matched to goals |
| Retrieval, memory, and data use (10) | Materials, retrieval, and persistence are used thoughtfully and effectively | Good baseline use of retrieval or memory | Basic retrieval or context use but limited adaptation | Little meaningful use of data, retrieval, or memory |
| Evaluation and iterative improvement (15) | Strong evidence of testing, critique, analysis, and a clear improvement cycle | Good testing and revision with some analysis | Some testing is present but shallow or incomplete | Little evidence of evaluation or improvement |
| Demonstration and use cases (10) | Demo is realistic, persuasive, and clearly tied to study value | Demo shows clear use and reasonable range | Demo works but is narrow or not fully convincing | Demo is weak, unclear, or disconnected from use case |
| Polish and advanced features (5) | Refinements are useful and well executed | Some valuable extensions or polish | Limited polish or minor extras | Little polish or poorly chosen extras |

</details>

### Feedback You Will Receive
The criteria for each individual review are on that milestone's page. Every review then uses the same set of questions, so you can anticipate them and address them in advance:

- What is already strong?
- What learning behaviors are present or missing?
- Where does the system still do too much for the student?
- How strong are the prompts and workflow decomposition?
- How well do retrieval, memory, and data handling support the learning goal?
- What should be improved before the next milestone?

### Teaming
You may work in teams for ideation, testing, peer critique, and shared infrastructure patterns. Grading still preserves individual accountability: **you submit your own workflows, prompts, evaluations, and demo.**

---

## What Will Be Valued Most
The project rewards quality of learning design more than flashy features. Strong projects will show:
- High-quality prompts and interaction design.
- Ingenuity in how the agent guides learning.
- Thoughtful workflow decomposition.
- Evidence that the system helps you think rather than merely receive answers.
- Clear demonstrations of use.
- Iterative refinement based on testing and feedback.

## What a Strong Final Project Looks Like
A strong final submission will:
- Feel like a coherent learning system rather than a pile of disconnected automations.
- Demonstrate several excellent learning behaviors behind a simple interface.
- Show persistence across time through memory, personalization, or weakness tracking.
- Include multiple functional workflows that work together reliably.
- Show prompt quality, testing discipline, and good judgment about when to challenge, retrieve, quiz, or synthesize.
- Include realistic demonstrations using actual course-related materials and scenarios.
