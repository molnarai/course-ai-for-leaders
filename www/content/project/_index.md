---
title: Project
description: "The semester project is to shape a Study Buddy: an agentic AI learning partner that helps you prepare for class, test your understanding, apply course ideas to your own work, and improve over time. You work in your own n8n environment, focusing on a single workflow: either one of the provided starter projects (Socratic tutor, quiz preparation, document Q&A, document organization, role play with evaluation) that you adapt, or a workflow you build yourself. The project rewards the quality of your learning design, the strength of your prompts, and the evidence that you tested and improved the system and can show how it supports learning, more than it rewards decorative complexity."
layout: "project"
---
<!-- **[Guidelines for Final Project Presentation](project-final-presentation/)** -->

<!-- **Project Assignment: Building an AI-Powered Business Solution** -->
### Purpose
The semester project is to design and shape a [**Study Buddy**](../blog/study-buddy/), an agentic AI learning partner that helps you prepare for class, test understanding, apply course ideas, and improve over time. The goal is not to build a chatbot that gives polished answers on demand. The goal is to build an AI system that helps you think better, diagnose better, and participate better in class.

The strongest Study Buddy will act like a persistent coach. It should ask good questions, challenge weak reasoning, help you connect ideas across readings and courses, and adapt to your recurring strengths and weaknesses.

### Project Context
You will develop your own version of Study Buddy inside your personal n8n environment. You may work in teams to explore ideas, test approaches, and share design patterns, but **you must configure, document, evaluate, and demonstrate your own version**.

You are provided with:
- n8n for workflow and agent orchestration.
- Access to LLMs.
- SearXNG for internet search.
- CubeFS for document storage and file access through a provided file-management tool.
- PostgreSQL with pgvector for structured storage, memory, and retrieval-augmented generation.
- Working starter projects that run out of the box:
  - **Socratic Tutor**, which asks before it explains.
  - **Quiz Preparation**, which generates and scores practice questions.
  - **Document Q&A**, for asking questions about your course and personal documents.
  - **Document Organization**, for ingesting, tagging, and organizing materials.
  - **Role Play with Evaluation**, which runs a scenario and then evaluates your performance.

### Two Ways to Succeed
You can reach an excellent grade on either path. Either way, the project centers on **a single workflow** done well. Building your own is encouraged, but it is not required.

**Path 1: Adapt the starter projects.** Pick one of the starter projects and make it work for a real learning goal in this course or another course you are taking. Most of your work goes into:
- **Content:** writing scenarios, cases, role-play setups, quiz topics, and supplemental documents that the workflow uses.
- **Behavior:** rewriting the system prompts so the starter coaches, challenges, and evaluates the way you want it to.
- **Testing:** running the workflow on realistic study tasks, recording what worked and what didn't, and revising.
- **Examples:** keeping before-and-after conversations that show how your changes improved the learning experience.

**Path 2: Build your own.** Extend a starter with new nodes, branches, or tools, or build a new workflow, using the design versions and workflow patterns described below.

On either path, the central question is the same: **can you demonstrate how the workflow is used for learning?**

### Design Principle
The governing principle for this project is:

> **Do not let your Study Buddy do for you what you need to learn to do.**

Your Study Buddy should improve your judgment, not replace it. A strong system should challenge, coach, probe, and adapt. It should avoid becoming a summary vending machine.

### What Study Buddy Should Do
At minimum, your Study Buddy should support a simple chat-centered learning experience with access to course materials and your own context. The system should make it easy for you to work with:
- Course Materials.
- My Materials.
- My Profile or Memory.

The user experience should be simple. You should not need to manually manage a technical database or tune a retrieval system by hand. Your design should keep the interface lightweight while hiding the complexity inside a well-designed workflow.

### Learning Behaviors to Target
Your Study Buddy should clearly demonstrate a few high-value learning behaviors. You do not need all of them, and you do not need these exact labels in the interface. Two or three behaviors done well are better than six done thinly. Each starter project already covers one or more of them.

Behaviors to choose from:
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

### What Your Project Should Include
A successful project, on either path, includes:

1. **One learning workflow you have made your own**, either a starter you have adapted or a workflow you built, used for a real study task.
2. **Course or supplemental materials** that the workflow uses: readings, cases, scenarios, role-play setups, quiz topics, or your own notes.
3. **Some form of evaluation**, whether the built-in evaluation of the Role Play starter, an evaluation step in your workflow, or a structured review of conversations against criteria you define.

Persistent memory, retrieval across many documents, or routing between study modes are welcome and will be credited when they strengthen your workflow, but they are not required. Focus on one workflow rather than spreading your effort across several.

### Technical Expectations
You do not need to build a workflow from scratch. The starter projects are **working n8n templates** that run out of the box with default behavior.

Your job is to pick one and make it your own:
- **Required: customize behavior through system prompts.** Rewrite the system prompts to define your Study Buddy's role, coaching style, tone, and how it uses your materials. This is where most of your design work will show.
- **Required: supply the content.** Create the scenarios, cases, quiz topics, or supplemental documents that make the workflow useful for a specific learning goal.
- **Optional: change the workflow structure.** If you are comfortable, you can also add, remove, or rewire nodes. For example, you might add a branching step or a new tool. This is not required, but it is a way to go further.

Your final project should show:
- Clear, deliberate system prompts for your workflow.
- Materials and scenarios prepared in a way that supports your learning goal.
- Test conversations and examples, with evidence that you improved the behavior based on what you saw.
- A clear demonstration of how the workflow is used for learning.

---

## Choosing Your Design

There is no single correct Study Buddy. The sections below describe viable versions of the project and the dimensions along which they differ. Use them to choose a scope you can actually finish and demonstrate well. If you are on Path 1, the starter projects already sit at the lower-complexity end of most dimensions. That is a perfectly good place to be. Whichever version you choose, realize it as a single workflow.

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

Best use: demonstrates orchestration and workflow design maturity. This goes beyond the single-workflow scope of the project; attempt it only if you are confident you can keep it reliable.

</details>

---

## Workflow Patterns You Can Build

The starter projects already implement several of these patterns. The list below is for students on Path 2, or anyone who wants to go further. Each pattern can be the focus of your single workflow; pick the one that fits your chosen version.

1. **Intent Router for Study Modes** — Detects whether you want preparation, quiz, challenge, synthesis, application, or reflection, and routes to different prompt templates and downstream workflows.
2. **Socratic Response Workflow** — Takes your question and responds with diagnostic or probing questions first, delaying direct explanation until you have shown sufficient effort.
3. **Case/Scenario Generator** — Uses course concepts plus uploaded materials to generate a realistic managerial situation, optionally with rubric fields such as concept targets, difficulty, and likely misconceptions.
4. **Weakness Tracker and Profile Updater** — Summarizes a conversation and writes structured observations to Postgres, tracking recurring errors, missed concepts, or reasoning habits.
5. **Class Preparation Coach** — Uses the materials assigned for a given date or topic and produces a readiness conversation with checks, gaps, and suggested class contributions.
6. **Cross-Reading Synthesizer** — Retrieves multiple readings, asks you to propose connections first, then generates prompts about complementarities, contradictions, assumptions, and boundary conditions.
7. **Challenge / Devil's Advocate Workflow** — Takes your interpretation and systematically tests alternative explanations or counterarguments.
8. **Evidence Checker** — Reviews an agent response or a claim and verifies whether it is grounded in retrieved materials, memory, or external search. Helps discourage hallucinated confidence.
9. **Reflection Workflow** — At the end of a session, prompts you to reflect on what changed in your understanding, and saves a concise reflection plus next-step recommendations.
10. **Demonstration Capture Workflow** — Creates a structured transcript, summary, or scorecard from a demo session. Useful for documenting your demonstration.

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
Do not push yourself toward unnecessary complexity. A single well-tuned Socratic Tutor or Role Play, with carefully written scenarios, tested prompts, and convincing examples, is better than an unreliable swarm of agents.

**Prefer one workflow with strong learning behaviors over many weak features.**

---

## Deliverables
You feature **one workflow** (which may be built from several connected workflows) and submit three deliverables:

1. **Report (1–3 pages), submitted on iCollege.** A short document about your featured workflow that covers:
   - **Intent:** the learning goal and how the workflow is meant to help teaching and learning.
   - **How it works:** how the workflow, or the set of workflows, operates.
   - **Your contribution:** what you built, changed, or tuned yourself (for example, system prompts and the reasons for your changes).
   - **List of materials:** every artifact you created for the project, such as prompts, scenarios, cases, quiz topics, and supplemental documents.
   - **Playbook:** step-by-step instructions for running it.
   - **Example runs:** sample dialogs or screenshots from realistic study situations.
   - **Summary and outlook:** what worked, what is still limited, and how you envision using and enhancing the project.
2. **Video (5–10 minutes), uploaded to iCollege.** Briefly introduce how your solution is built, then demonstrate how it works. You can use screen recordings, PowerPoint slides, or both.
3. **Workflows on your Study Buddy system, synced to GitLab.** Keep your workflows on your Study Buddy system and sync them to GitLab with the **Submit for review** button on the *n8n* panel.

---

## Grading

Your project is evaluated on how well your Study Buddy supports learning, how thoughtfully your workflow is designed, and how clearly you demonstrate its use for learning. Prompt quality, ingenuity, well-prepared materials, and realistic demonstration count for more than decorative complexity. Bells and whistles count, but they do not dominate. Projects that adapt the starters are graded on the same rubric: for workflow architecture, what counts is how well you chose and configured the workflow for your learning goal, not how many nodes you built.

### Grading Categories
The rubric uses 100 points total.

| Category | Weight | What is being judged |
|---|---:|---|
| Learning design and pedagogy | 30 | Does the system help you think, diagnose, apply, and improve rather than just answer? |
| Workflow architecture and implementation | 10 | Is the workflow well chosen for your goal, well configured, and reliable? |
| Prompt quality and orchestration | 20 | Are prompts well designed, purposeful, and adapted to task or mode? |
| Materials and data use | 15 | Do the materials, scenarios, and supplemental documents you prepared (and any retrieval or memory) support the learning goal? |
| Demonstration and use cases | 20 | Do you convincingly show realistic use and explain the value? |
| Polish and advanced features | 5 | Are there useful refinements, interface quality, or technically interesting extensions? |

### Detailed Rubric

<details>
<summary><strong>Show the full rubric</strong></summary>

| Category | Excellent | Good | Developing | Weak |
|---|---|---|---|---|
| Learning design and pedagogy (30) | System consistently coaches, challenges, and adapts; clearly improves your thinking | Often supports learning well, though some behaviors are uneven | Shows some coaching behavior but often falls back to direct answering | Mostly a generic chatbot with little learning design |
| Workflow architecture and implementation (10) | Workflow is well chosen for the goal, carefully configured, and reliable | Workflow works well with minor gaps | Workflow runs but is only lightly adapted or somewhat fragile | Starter used unchanged, or automation is unreliable |
| Prompt quality and orchestration (20) | Prompts are precise, mode-aware, and pedagogically strong | Prompts are mostly good with some generic sections | Prompts work but are shallow or inconsistent | Prompting is weak, generic, or poorly matched to goals |
| Materials and data use (15) | Scenarios, documents, and any retrieval or memory are prepared thoughtfully and clearly serve the goal | Good, relevant materials with some gaps | Materials are generic or only loosely tied to the goal | Little meaningful use of materials or data |
| Demonstration and use cases (20) | Demo is realistic, persuasive, and clearly tied to study value | Demo shows clear use and reasonable range | Demo works but is narrow or not fully convincing | Demo is weak, unclear, or disconnected from use case |
| Polish and advanced features (5) | Refinements are useful and well executed | Some valuable extensions or polish | Limited polish or minor extras | Little polish or poorly chosen extras |

</details>

### Teaming
You may work in teams for ideation, testing, peer critique, and shared infrastructure patterns. Grading still preserves individual accountability: **you submit your own workflow, prompts, evaluations, and demo.**

---

## What Will Be Valued Most
The project rewards quality of learning design more than flashy features. Strong projects will show:
- High-quality prompts and interaction design.
- Ingenuity in how the agent guides learning.
- Thoughtful choice and configuration of your workflow.
- Well-crafted scenarios and supporting materials.
- Evidence that the system helps you think rather than merely receive answers.
- Clear demonstrations of use.
- Iterative refinement based on testing and feedback.

## What a Strong Final Project Looks Like
A strong final submission will:
- Feel like a focused learning tool with a clear purpose rather than a generic chatbot.
- Demonstrate a few excellent learning behaviors behind a simple interface.
- Use scenarios, cases, or documents you prepared that make the workflow genuinely useful for a specific course or goal.
- Show prompt quality, testing discipline, and before-and-after examples of improved behavior.
- Include realistic demonstrations that show how the workflow is used for learning.
- Optionally, add persistence, routing, or extra tools within the workflow where they clearly add value.
