+++
title = "Agentic Systems"
description = "From a pattern that answers to a process that acts — the agentic loop, tools, memory, multi-agent teams, design patterns, and the autonomy decisions leaders own"
weight = 30
outputs = ["Reveal"]
math = true
thumbnail = "/imgs/slide-30-agentic-systems/Slide1.png"


[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"

+++

<!--
    Slide deck: Agentic Systems.

    Follows slide-20-rag and slide-21-engineering-robust-rag. The source images
    keep their original order; sections, framing slides and discussion
    questions are added around them.

    Two kinds of slides are used here:
      1. Image slides — the exported source slides.
         Format: {{</* slide content-image="/imgs/slide-30-agentic-systems/Slide2.png" */>}}
         Source images live in www/static/imgs/slide-30-agentic-systems
      2. Native slides — section dividers, framing and discussion questions,
         using the helper classes defined in the style block below.

    Every content slide carries speaker notes in a {{%/* note */%}} block.
-->

<style>
/* Helper classes for this deck. Palette follows reveal-robinson.css —
   GSU Blue #003478, GSU Crimson #CC0000. Kept in sync with slide-20-rag. */

/* reveal-robinson.css pads sections by 50px with box-sizing: content-box, which
   makes every section 1060px wide on a 960px stage and clips text off the right
   edge. Scoped correction so the native slides fit. */
.reveal .slides section { box-sizing: border-box; }

.reveal .slides section.fs66 { font-size: 0.66em; }
.reveal .slides section.fs60 { font-size: 0.60em; }
.reveal .slides section.fs55 { font-size: 0.55em; }
.reveal .slides section.fs50 { font-size: 0.50em; }
.reveal .slides section[class*="fs"] h1 { font-size: 52px; margin-bottom: 0.4em; }

.reveal .cols2 { display: grid; grid-template-columns: 1fr 1fr; gap: 0 1.8em; align-items: start; }
.reveal .cols3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0 1.4em; align-items: start; }
.reveal .cols2 p, .reveal .cols3 p { margin: 0.35em 0; }

.reveal .sub { color: #CC0000; font-weight: 700; margin: 0.8em 0 0.25em 0; }
.reveal .cols2 > div > .sub:first-child,
.reveal .cols3 > div > .sub:first-child { margin-top: 0; }

.reveal .card { background: #f4f6f9; border-left: 4px solid #003478;
                border-radius: 6px; padding: 0.5em 0.9em; margin: 0 0 0.55em 0; }
.reveal .card .hd { color: #003478; font-weight: 700; display: block; margin-bottom: 0.1em; }
.reveal .card.warn { border-left-color: #CC0000; }
.reveal .card.warn .hd { color: #CC0000; }

.reveal .term { color: #CC0000; font-weight: 700; }
.reveal .lead { font-style: italic; color: #555; margin-bottom: 0.8em; }
.reveal .refs { font-size: 0.62em; color: #777; margin-top: 0.9em; }
.reveal .refs a { color: #777; }

.reveal table.plain { width: 100%; border-collapse: collapse; }
.reveal table.plain th { color: #003478; text-align: left; border-bottom: 2px solid #003478;
                         padding: 0.3em 0.5em; }
.reveal table.plain td { border-bottom: 1px solid #ddd; padding: 0.3em 0.5em; vertical-align: top; }
.reveal table.plain td.lv { color: #CC0000; font-weight: 700; white-space: nowrap; }

/* Section dividers — flat GSU Blue panel. */
.reveal .slides section.section { text-align: center; }
.reveal .slides section.section h1 { color: #fff; font-size: 2.3em; margin: 0; }
.reveal .slides section.section p { color: #c9d6e8; font-size: 0.66em; margin-top: 0.7em; }

/* The theme's footer branding and slide number are dark, drawn for white
   slides. Reverse them to white while a dark divider is on screen. */
.reveal:has(.slides section.section.present) .slide-footer img { filter: brightness(0) invert(1); }
.reveal:has(.slides section.section.present) .slide-number { color: #EDEEEF; }

/* Discussion question slides */
.reveal .slides section.dq h3 { color: #CC0000; font-size: 0.75em; margin-bottom: 0.15em; }
.reveal .slides section.dq h1 { font-size: 1.6em; }
.reveal .slides section.dq .q { color: #003478; font-weight: 700; margin-top: 0.9em; }
</style>

<!-- ===== TITLE (the figure carries the title) ===== -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide1.png" >}}
<h1></h1>

{{% note %}}
- Welcome. The spy imagery is a joke with a point: an agent is something you send out to act on your behalf, with standing instructions, in an environment you do not fully control.
- Everything before today has been about systems that *answer*. Today is about systems that *do* — and that one word changes the engineering, the economics and the liability.
{{% /note %}}

***

<!-- ===== OUTLINE ===== -->
{{< slide class="fs60" >}}

# Outline

<p class="lead">EMBA 8160 &mdash; AI for Leaders &middot; Session 2</p>

<div class="cols2">
<div>
<p><span class="term">1.</span> What an agent actually is</p>
<p><span class="term">2.</span> From a pattern that answers to a process that acts</p>
<p><span class="term">3.</span> A worked example: the refund agent</p>
<p><span class="term">4.</span> AI agents vs. Agentic AI</p>
</div>
<div>
<p><span class="term">5.</span> Multi-agent systems and coordination</p>
<p><span class="term">6.</span> The four design patterns</p>
<p><span class="term">7.</span> Architectures and frameworks</p>
<p><span class="term">8.</span> What this looks like in industry</p>
</div>
</div>

{{% note %}}
- Hold one question throughout: **what is this system allowed to do without asking anyone?** That single question organises most of the governance work in this field.
- Sections 1&ndash;3 build the vocabulary and one concrete example. Sections 4&ndash;6 scale it up. Sections 7&ndash;8 are what you will actually be shown by vendors and internal teams.
{{% /note %}}

***

<!-- ===== SECTION 1 ===== -->
{{< slide background-color="#003478" class="section" >}}

# What Is an Agent?

<p>Definitions, components, and why this is not a chatbot</p>

{{% note %}}
Part one: the vocabulary. Most arguments about agent strategy are really arguments about what the word means.
{{% /note %}}

***

<!-- 2 — What Is an AI Agent? -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide2.png" >}}
<h1></h1>

{{% note %}}
- The working definition: a system that **perceives** its environment, **reasons** over what it finds, **plans** a course of action, and **executes** on behalf of a user.
- The foundational definition is fifty years older than ChatGPT — Russell and Norvig's &ldquo;anything perceiving its environment through sensors and acting upon it through actuators.&rdquo; Agents are a classical AI idea; the language model is a new engine dropped into an old architecture.
- The distinction that matters commercially is bottom left: a **perception-action loop** rather than a single prompt and response. The system keeps going until the goal is met or it gives up.
- &ldquo;Beyond chatbots&rdquo; is the sentence to repeat: decomposes problems, holds context over long horizons, and calls external tools. A chatbot's output is text. An agent's output is a *changed system*.
{{% /note %}}

***

<!-- 3 — Nature of AI agents -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide3.png" >}}
<h1></h1>

{{% note %}}
- Four properties worth pulling out for a business audience.
- **Continuous cycles** mean the system is adaptive — and also that it can loop, which is a cost and safety concern we will come back to.
- **Multimodal input** means text, images and sensor data: relevant for anyone in manufacturing, logistics or clinical settings where the signal is not a document.
- **Modularity** is the procurement point. Perception, reasoning, memory and tools are separable components, so you can replace one without rebuilding the system. Be sceptical of any vendor whose architecture does not let you swap the model.
{{% /note %}}

***

<!-- 4 — Core elements -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide4.png" >}}
<h1></h1>

{{% note %}}
- Eight components. Four are obvious — perception, reasoning, memory, action. Four are where projects succeed or fail: **planning**, **tool integration**, **learning**, and **safety**.
- Note that **safety** is drawn as a component, not a policy document. Guardrails, toxicity checks and human validation are things that are built, staffed and tested — or they do not exist.
- Ask the room to guess which box consumes the most engineering time in practice. It is usually tool integration: connecting to enterprise systems that were never designed to be driven by a language model.
- Use this slide as a checklist in design reviews. If a proposed &ldquo;agent&rdquo; has no memory and no planning, it is a chatbot with an API call, and it should be priced like one.
{{% /note %}}

***

<!-- ===== SECTION 2 ===== -->
{{< slide background-color="#003478" class="section" >}}

# From Pattern to Process

<p>Why RAG is a straight line and an agent is a loop</p>

{{% note %}}
Part two: the mechanical heart of the session, and the bridge from the last two sessions on RAG.
{{% /note %}}

***

<!-- 5 — RAG is a pattern, not a process -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide5.png" >}}
<h1></h1>

{{% note %}}
- Here is what we built in the last two sessions, drawn honestly: query, retrieve, generate, answer. A straight line.
- **Fixed control flow** — the path is decided in advance, and there is no branching. **Static goal** — answer one question from available context.
- The limitation is the whole reason for today: it cannot do multi-step reasoning and it cannot take external action. Ask it to *process* the refund rather than explain the refund policy and the architecture has nothing to offer.
{{% /note %}}

***

<!-- 6 — The agent: a process that controls patterns -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide6.png" >}}
<h1></h1>

{{% note %}}
- The inversion, and the single most important slide in the deck. The straight line becomes one option inside a loop: goal, plan, **decide**, act, evaluate — and back to plan if the goal is not met.
- Look at what sits behind &ldquo;decide&rdquo;: RAG, APIs, a code interpreter. **RAG becomes a tool the agent chooses to use**, not the architecture of the system.
- That sentence is worth saying twice, because it reframes every RAG project in the room. The retrieval system you just scoped is a component in something larger.
- The governance consequence arrives with the word &ldquo;decide.&rdquo; A system with a fixed path can be tested exhaustively. A system that chooses its own path cannot — you test the *policy*, not the path.
{{% /note %}}

***

<!-- 7 — The agentic loop -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide7.png" >}}
<h1></h1>

{{% note %}}
- The loop in four words: **perceive, decide, act, remember**. The next three slides open up three of those quadrants.
- Compare it to OODA if the room has a military or operations background — observe, orient, decide, act. Same structure, and the same insight: the advantage comes from cycling faster and from the quality of what you remember between cycles.
- &ldquo;Remember&rdquo; is the one people skip. Without state, an agent repeats itself, re-does work, and cannot explain what it did.
{{% /note %}}

***

<!-- 8 — The reasoning engine -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide8.png" >}}
<h1></h1>

{{% note %}}
- The **decide** quadrant. The foundation model is the brain, and it is doing three specific jobs.
- **Decomposition**: high-level goal into atomic steps. **Chain of thought**: an internal monologue used to validate its own logic. **Routing**: choosing which tool to engage.
- Self-reflection sits in the middle of the diagram — the agent critiquing its own plan before acting. That is cheap insurance and it is the Reflection pattern we come back to later.
- Caution worth voicing: the internal monologue is *generated text*, not a guaranteed account of the model's actual computation. It is extremely useful for debugging and it is not a compliance artifact. Do not let anyone present chain-of-thought as an audit trail.
{{% /note %}}

***

<!-- 9 — Tools and environment interfaces -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide9.png" >}}
<h1></h1>

{{% note %}}
- The **act** quadrant, and the slide where the risk conversation really begins. Connectors that let the agent &ldquo;affect the world, not just speak about it.&rdquo;
- Look at the tool list in the code box: `search_docs`, `update_record`, `issue_refund`. Three lines, and the third one moves money.
- The technical framing is a list of functions. The business framing is a **list of permissions granted to a non-deterministic system**. Those are the same list, and only one of them gets reviewed in most organisations.
- Practical guidance: every tool an agent holds should have its own authorisation, its own rate limit, and its own audit log. &ldquo;The agent has API access&rdquo; is not an acceptable answer to a control question.
{{% /note %}}

***

<!-- 10 — Memory, state and observation -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide10.png" >}}
<h1></h1>

{{% note %}}
- The **remember** quadrant, split two ways: short-term (the context window — chat history and the current plan) and long-term (a database of user preferences and domain knowledge).
- The right-hand box is the part engineers care about and leaders should too: **structured state**. `customer_verified: true`, `refund_amount: 75.00`, `status: pending_approval`.
- Why it matters: the state object, not the conversation, is the record of what the system believed and did. It is what you replay in a dispute, and it is what a regulator will ask for. Free-text chat history is not a substitute.
- Observation and self-correction loop back into both stores — the agent checks the result of its action and updates what it believes.
{{% /note %}}

***

<!-- Tools are permissions -->
{{< slide class="fs55" >}}

# Every tool is a permission

<div class="cols2">
<div>
<p class="sub">What the team sees</p>
<div class="card"><span class="hd">A function signature</span><code>payment.issue_refund(order_id, amount)</code><br>Two parameters, one line of configuration.</div>
<p>Adding a tool is a ten-minute task. That is genuinely what makes agents powerful.</p>
</div>
<div>
<p class="sub">What you are approving</p>
<div class="card warn"><span class="hd">A standing authority</span>A probabilistic system may move money, on its own judgement, at a rate limited only by how often people ask.</div>
<p>The same ten minutes, from the other side of the table.</p>
</div>
</div>

<p class="refs">Ask for four things per tool: <strong>who authorised it</strong>, <strong>what the blast radius is</strong>, <strong>what the ceiling is</strong>, and <strong>how it gets reversed</strong>.</p>

{{% note %}}
- This is the slide to spend real time on. The gap between how cheap it is to add a tool and how consequential the tool is, is the central governance problem of agentic systems.
- The four questions are the practical version. Blast radius: what is the worst single call? Ceiling: the hard limit that is enforced in code, not in the prompt. Reversal: is there an undo, and who can run it?
- Say clearly: a limit written in a prompt is a *request*. A limit enforced in the tool wrapper is a **control**. Auditors care about the second kind, and so should you.
{{% /note %}}

***

<!-- ===== SECTION 3 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Agents at Work

<p>Where they are deployed, and one example in detail</p>

{{% note %}}
Part three: from architecture to a concrete transaction.
{{% /note %}}

***

<!-- 11 — AI agents in business -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide11.png" >}}
<h1></h1>

{{% note %}}
- The deployment map across eight domains. Do not read it out — pick the two closest to the room and dwell there.
- A pattern worth naming: almost every entry replaces *coordination* work rather than *thinking* work. Routing a query, chasing a shipment, checking a contract against a playbook, assembling a report. That is where the near-term value is, and it is also where the headcount questions land.
- Note &ldquo;RAG routers&rdquo; under customer service — exactly the routing architecture from the last session, now one component inside an agent.
{{% /note %}}

***

<!-- 12 — Use case: intelligent customer support -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide12.png" >}}
<h1></h1>

{{% note %}}
- One sentence from a customer: &ldquo;I need a refund for my last order.&rdquo; Four things have to happen: verify identity, retrieve purchase history, check the business rule, execute the refund.
- The line at the bottom is the whole session compressed: **a standard chatbot can explain the policy; an agent applies it.**
- Notice the business rule is a threshold — under $\$100$. Someone chose that number. That choice is the actual autonomy decision, and it is usually made in a configuration file by whoever is building the system.
- Ask: who in your organisation signs off on that threshold today for a human agent? Whoever it is, they should sign off on this one.
{{% /note %}}

***

<!-- 13 — Under the hood: the refund logic -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide13.png" >}}
<h1></h1>

{{% note %}}
- The same transaction as a trace. Input, LLM classifies intent and plans, CRM tool, billing tool, a deterministic logic check on the 30-day window, the refund call, a write to memory, and a response.
- Two colours, two kinds of step. The **red diamonds are model judgement**; the **green boxes are deterministic calls**. Good agent design pushes as much as possible into green.
- Point at the &ldquo;within 30 days?&rdquo; check specifically: that is a business rule evaluated in code, not by the model. If that check were phrased as a prompt instruction, it would hold most of the time — and most of the time is not a policy.
- This trace is also the audit record. If your team cannot produce a picture like this for a real transaction after the fact, the system is not ready for production.
{{% /note %}}

***

<!-- Where the refund agent breaks -->
{{< slide class="fs55" >}}

# Where that refund agent breaks

<div class="cols2">
<div>
<div class="card warn"><span class="hd">Misread intent</span>&ldquo;I'd like to know about refunds&rdquo; is classified as a refund request. The model acts on an enquiry.</div>
<div class="card warn"><span class="hd">Stale or wrong data</span>The CRM lookup returns the wrong order. Every downstream step is correct and the outcome is wrong.</div>
<div class="card warn"><span class="hd">Partial failure</span>The refund API succeeds; the memory write fails. The system does not know what it did.</div>
</div>
<div>
<div class="card warn"><span class="hd">Loops and cost</span>The goal is never judged &ldquo;met,&rdquo; so the agent re-plans indefinitely. The bill and the latency grow together.</div>
<div class="card warn"><span class="hd">Prompt injection</span>The customer writes text designed to be read as an instruction. The attack surface is the input field.</div>
<div class="card warn"><span class="hd">Threshold drift</span>The $\$100$ ceiling lives in a prompt, not in the payment wrapper, and quietly stops binding.</div>
</div>
</div>

{{% note %}}
- None of these are exotic. Every one has been observed in deployed systems.
- **Partial failure** is the one that surprises executives: unlike a database transaction, an agent's sequence of tool calls has no automatic rollback. If money moved and the log did not, you have a reconciliation problem and no record of the cause.
- **Prompt injection** deserves its own sentence: the user's text and the system's instructions travel in the same channel, so anything a user can write is potentially an instruction. This is why a tool that can move money must never trust the model's judgement alone.
- The mitigations are unglamorous and effective: step limits, budget caps, idempotent tool calls, deterministic rule checks, and human approval above a threshold.
{{% /note %}}

***

<!-- ===== SECTION 4 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Agents vs. Agentic AI

<p>The unit and the system</p>

{{% note %}}
Part four: a distinction vendors blur, and one you should be able to hold firmly.
{{% /note %}}

***

<!-- 14 — AI agents vs agentic AI -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide14.png" >}}
<h1></h1>

{{% note %}}
- **AI agents are the building blocks; Agentic AI is the system-level paradigm.** An agent answers a question or processes a file. Agentic AI manages a supply chain.
- The autonomy row is the one to interrogate. &ldquo;Reactive&rdquo; means it operates within predefined constraints and usually waits to be asked. &ldquo;Proactive&rdquo; means it **formulates its own goals**.
- Be direct with the room: the right-hand column is mostly aspiration today. Very few production systems self-formulate goals, and the ones that do are narrowly bounded. When a vendor sells the right-hand column, ask which specific goals the system sets for itself and what stops it setting one you would not approve.
- The useful takeaway is not the taxonomy — it is that autonomy is a dial, and someone has to decide where it is set.
{{% /note %}}

***

<!-- 15 — Core concepts of agentic AI -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide15.png" >}}
<h1></h1>

{{% note %}}
- The four foundational patterns, which we will see again in detail: **reflection**, **planning**, **tool use**, **multi-agent collaboration**.
- These are composable, not alternatives. A serious system uses all four.
- Flag the cost structure now: reflection means generating output more than once, planning means extra model calls before any work happens, and multi-agent means several models in conversation. Each pattern buys quality with tokens and latency. There is no free reliability.
{{% /note %}}

***

<!-- 16 — Advanced agentic AI principles -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide16.png" >}}
<h1></h1>

{{% note %}}
- Four higher-order principles. **Governed autonomy** is first, and deliberately so: independent operation *within strict guardrails*, with human approval checkpoints for critical actions.
- **System-level orchestration** is the organisational claim — coordination across functions, breaking silos between production, logistics and sales. Note what that implies: the agent inherits every data-sharing and access question those silos were partly there to manage.
- **Proactive goal formulation** — &ldquo;from reactive executor to proactive partner&rdquo; — is the frontier claim. Treat it as a direction of travel, not a current capability.
- The leadership read: principles one and two are buildable today and are mostly governance work. Principles three and four are where the research is.
{{% /note %}}

***

<!-- ===== SECTION 5 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Multi-Agent Systems

<p>From decomposing steps to decomposing roles</p>

{{% note %}}
Part five: what happens when one agent is not enough — and when it is.
{{% /note %}}

***

<!-- 17 — Beyond the individual -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide17.png" >}}
<h1></h1>

{{% note %}}
- On the left, one agent with everything pointed at it — inputs, data, tasks, and a lot of question marks. On the right, three agents with roles.
- **The shift: from decomposing steps to decomposing roles.** That is an organisational design idea, not a technical one, and it is why this material feels familiar to anyone who has structured a team.
- Two justifications given: **specialisation** (each agent optimised for a sub-domain, with its own instructions and tools) and **complexity management** (preventing context window overflow).
- The second is the more honest engineering reason. A single agent holding an entire complex task runs out of room and starts losing the thread — the &ldquo;lost in the middle&rdquo; problem from the last session, now applied to a plan rather than a document.
{{% /note %}}

***

<!-- 18 — The multi-agent architecture -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide18.png" >}}
<h1></h1>

{{% note %}}
- Two structural pieces: the **orchestrator** — the manager that controls flow, routes outputs, and decides when the goal is met — and the **shared state or blackboard**, the common workspace all agents read from and write to.
- The blackboard is an old idea from classical AI and it is the right one. It means agents do not need to talk to each other directly; they publish to a shared board.
- Two questions to ask about any multi-agent design: **who decides the goal is met**, and **what happens when two agents write contradictory things to the blackboard?** Teams often have no answer to the second.
- Organisational analogy, and a warning with it: a manager, a shared document, and three specialists. Multi-agent systems inherit the failure modes of human teams too — deadlock, duplicated work, and diffusion of responsibility.
{{% /note %}}

***

<!-- 19 — Modes of coordination -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide19.png" >}}
<h1></h1>

{{% note %}}
- Two coordination modes. **Linear — the relay race:** a fixed sequence, best for predictable workflows. **Adaptive — the basketball team:** dynamic routing where the orchestrator picks the next agent based on context.
- The trade-off is exactly the one from earlier: the relay race is testable, auditable and cheap; the basketball team handles novelty and cannot be exhaustively tested.
- Strong practical advice for the room: start with the relay race. Most processes that get proposed for adaptive coordination turn out to be predictable enough for a fixed sequence, and the fixed sequence can be explained to an auditor.
- Escalate to adaptive coordination only where you can point to real variation that the fixed path handles badly.
{{% /note %}}

***

<!-- 20 — Use case: contract analysis -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide20.png" >}}
<h1></h1>

{{% note %}}
- A second worked example with genuinely different shape: raw PDF in, OCR required, legal tone and compliance constraints, risk compared against internal playbooks, and new clauses drafted and synced to the contract management system.
- &ldquo;**Too complex for a single prompt. Requires a team.**&rdquo; — note the specific reason. It is not that the task is hard; it is that the task has four different *kinds* of work, each needing different instructions, different tools, and different quality bars.
- The risk step is a RAG call against policy playbooks. Again, retrieval as a component.
- Worth flagging: the output is a **redline draft**, not a decision. That is a well-designed autonomy boundary and a good template — the system does the labour, a lawyer keeps the judgement.
{{% /note %}}

***

<!-- 21 — The negotiation team -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide21.png" >}}
<h1></h1>

{{% note %}}
- The team: an **intake agent** that configures the workflow, a **classifier** doing OCR and extraction, a **risk analyst** running the RAG policy check, and a **drafter** generating redlines — all coordinating through the shared blackboard holding the parsed contract, the risk list and the draft edits.
- Note the blackboard contents are *structured artifacts*, not conversation. That is what makes the system reviewable: a human can inspect the risk list without reading the agents' chatter.
- This is also the natural place to insert human review — between the risk list and the draft edits. Pause the workflow, show a person the risks, let them approve before anything is drafted.
{{% /note %}}

***

<!-- 22 — The design challenge -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide22.png" >}}
<h1></h1>

{{% note %}}
- The progression, and the exercise: take a RAG project you already have, redesign it as a single agent loop, then scale it to a multi-agent team with specialised roles.
- Use this as a live exercise if there is time. Most people in the room have a RAG project in flight or in the budget.
- The useful discipline in doing it: at each step, name what new capability you gained and what new failure mode you accepted. The arrow is not free in either direction.
{{% /note %}}

***

<!-- When not to go multi-agent -->
{{< slide class="fs55" >}}

# When *not* to build a team

<div class="cols2">
<div>
<p class="sub">Multi-agent earns its cost when</p>
<p>The work has genuinely different kinds of task, each needing different tools, instructions or quality bars.</p>
<p>A single agent's context or instruction set has become unmanageable.</p>
<p>You want independent review &mdash; one agent checking another's work.</p>
</div>
<div>
<p class="sub">It is usually the wrong answer when</p>
<p>The process is a fixed sequence. That is a workflow, and a workflow engine will be cheaper, faster and testable.</p>
<p>Nobody can say which agent is accountable for the final output.</p>
<p>The team is reaching for it because the single agent is unreliable &mdash; more agents multiply an unreliable step rather than fixing it.</p>
</div>
</div>

<p class="refs">Each additional agent adds model calls, latency, and a new place for the handoff to go wrong. Complexity is a cost you pay every single transaction.</p>

{{% note %}}
- The last item on the right is the common failure. Multi-agent architectures are often adopted as a remedy for a step that simply does not work well. It rarely helps, and it makes the failure harder to locate.
- The &ldquo;this is really a workflow&rdquo; point is worth pressing. A large share of proposed agentic systems are deterministic business processes with one uncertain step. Build the deterministic part deterministically and use a model only where judgement is genuinely needed.
- Debuggability is the hidden cost: with one agent you ask why it did that. With six, you first have to work out which one did it.
{{% /note %}}

***

<!-- ===== SECTION 6 ===== -->
{{< slide background-color="#003478" class="section" >}}

# The Design Patterns

<p>Reflection, tool use, planning, and multi-agent</p>

{{% note %}}
Part six: the four patterns in detail. These are the vocabulary your engineers already use.
{{% /note %}}

***

<!-- 23 — Four patterns overview -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide23.png" >}}
<h1></h1>

{{% note %}}
- All four on one page. **Reflection** — generate, critique, iterate. **Tool use** — prompt out to tools, results back. **Planning** — plan, generate tasks, execute, re-plan. **Multi-agent** — specialised roles in conversation.
- Note the loop symbol in three of the four. Iteration is the common thread, and iteration is what separates these from a single prompt.
- Each of the next five slides takes one of these apart.
{{% /note %}}

***

<!-- 24 — Reflection pattern -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide24.png" >}}
<h1></h1>

{{% note %}}
- **Reflection**: the system reviews its own output the way a human reviewer would, identifies errors, and revises. The self-critique loop can run several times.
- The worked example is **Self-RAG**, which applies reflection to the retrieval pipeline: instead of always retrieving a fixed number of documents, the model decides *whether* retrieval is needed, then critiques the segments it generated for relevance and support.
- The business translation: reflection buys accuracy with tokens. A useful rule is to reserve it for outputs that are expensive to get wrong — a contract redline, a customer-facing commitment, code that will be deployed.
- It is also the cheapest quality intervention available in most pipelines. If a team has never tried &ldquo;generate, then critique, then revise,&rdquo; that is the first experiment to run.
{{% /note %}}

***

<!-- 25 — Self-RAG vs RAG -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide25.png" >}}
<h1></h1>

{{% note %}}
- The comparison in detail. Standard RAG on the left: retrieve *k* documents, prompt with all of them, generate. The result contains a contradiction and a passage with no supporting information — the FP4 failure from the last session.
- Self-RAG on the right: retrieve on demand, generate segments in parallel, then **critique and select** — each segment tagged relevant, irrelevant, supported or partially supported, and the best combination assembled.
- The bottom row is the elegant part. &ldquo;Write an essay about your best summer vacation&rdquo; triggers **no retrieval at all**, because the model judges that no external knowledge is needed. Standard RAG retrieves regardless, wasting cost and adding noise.
- Leadership version: the system decides whether it needs to look something up, and grades its own evidence. That is a meaningful reliability gain, and it costs more per query.
{{% /note %}}

***

<!-- 26 — Tool use pattern -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide26.png" >}}
<h1></h1>

{{% note %}}
- **Tool use** in its general form: databases, web search, code execution, image generation, spreadsheet manipulation.
- The phrase to take away is &ldquo;from static knowledge banks into dynamic agents that interact with external systems.&rdquo;
- Code execution deserves a specific flag. An agent that can run code is extraordinarily capable and is also arbitrary code execution inside your environment. It belongs in a sandbox with no network access and no credentials, every time, without exception.
{{% /note %}}

***

<!-- 27 — Planning pattern -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide27.png" >}}
<h1></h1>

{{% note %}}
- **Planning**: build a roadmap of subtasks before executing, rather than working linearly.
- Two named approaches your engineers will mention. **ReAct** — reasoning and acting interleaved, so the agent thinks, acts, observes the result, and thinks again. **ReWOO** — reasoning decoupled from observation, so the plan is formed up front and executed with fewer model calls.
- The practical distinction for a budget conversation: ReAct is adaptive and expensive because every step involves the model; ReWOO is cheaper and less able to recover when reality departs from the plan.
- The figure glosses ReWOO as &ldquo;Reasoning With Open Ontology&rdquo; in one place and &ldquo;Reasoning WithOut Observation&rdquo; in another. The second is the correct expansion — worth knowing before someone in the room checks.
{{% /note %}}

***

<!-- 28 — Multi-agent pattern -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide28.png" >}}
<h1></h1>

{{% note %}}
- **Multi-agent**, with the three organisational shapes named explicitly on the right: **collaborative** (peers sharing progress), **supervised** (a supervisor coordinating and verifying), and **hierarchical** (decisions cascading through levels).
- These are the three shapes human organisations use, for the same reasons. The supervised pattern is the one most enterprises should start with, because it creates a single place where quality is verified and a single answer to &ldquo;who is accountable.&rdquo;
- The analogy to project management is in the source text, and it is fair. Just note that it inherits the failure modes too: unclear ownership, handoff loss, and meetings that produce nothing.
{{% /note %}}

***

<!-- ===== SECTION 7 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Architectures &amp; Frameworks

<p>What the reference designs look like, and what you will be sold</p>

{{% note %}}
Part seven: the reference architectures and the tooling landscape.
{{% /note %}}

***

<!-- 29 — Agentic architectures -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide29.png" >}}
<h1></h1>

{{% note %}}
- A catalogue rather than a diagram to read line by line. Single versus multi-agent at the top; the coordination patterns in the middle — **parallel, sequential, loop, router, aggregator, network, hierarchical**; six worked examples on the right.
- Point at two specifically. **Router** is the architecture from the end of the last session — classify the request, send it to the right handler. **Human-in-the-loop** (example 2) is the one that should appear in most enterprise designs and frequently does not.
- The value of a catalogue like this in a design review is that it turns &ldquo;we're building an agent&rdquo; into &ldquo;we're building a supervised hierarchical system with a router in front,&rdquo; which is a sentence you can actually interrogate.
{{% /note %}}

***

<!-- 30 — Classic agent types -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide30.png" >}}
<h1></h1>

{{% note %}}
- The classical taxonomy, from the Russell and Norvig textbook, and it is genuinely clarifying: **simple reflex** (condition-action rules), **model-based reflex** (keeps an internal model of a partially observable world), **goal-based** (searches and plans toward a goal), **utility-based** (optimises a utility function under uncertainty), and **learning** agents (a critic and a learning element that improve performance over time).
- Most LLM agents shipping today are goal-based. Utility-based agents are rarer and more consequential, because a utility function is an explicit statement of what the organisation values — and anything not in it gets traded away.
- That is the slide's real lesson for leaders: if you let a system optimise, you have to be able to write down what &ldquo;better&rdquo; means. Most organisations discover they cannot.
- Note also that &ldquo;learning agent&rdquo; means the system changes after deployment. Anything that changes itself needs monitoring, not just testing.
{{% /note %}}

***

<!-- 31 — Agentic search -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide31.png" >}}
<h1></h1>

{{% note %}}
- A real production-shaped architecture, numbered one to nine. Query in, system prompt and query parsing, a switch between a general language model and a dedicated **reasoning** model, a retrieval agent that fans out to a vector database, a semantic database and external search engines, short- and long-term memory, then a compiled output.
- Two details worth pointing at. First, the **switch** between model types: routing cheap questions to a cheap model and hard ones to an expensive reasoning model is one of the main levers on unit economics. Second, retrieval agents A and B running against *different* sources — internal knowledge and the public web — which is an obvious place for a data-leakage control.
- This is roughly what a serious internal &ldquo;ask anything&rdquo; system looks like. Note how little of it is the model.
{{% /note %}}

***

<!-- 32 — Architecture of AI agents -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide32.png" >}}
<h1></h1>

{{% note %}}
- The layered enterprise reference architecture: input layer, orchestration layer, the agents themselves, a data storage and retrieval layer, then output and service layers.
- The band across the bottom is the one to dwell on: **safety and control, ethics and responsible AI, regulatory and compliance, interoperability, versioning and evaluation, human-AI collaboration.** Drawn as a foundation under everything, which is the correct picture and rarely the correct project plan.
- Note &ldquo;monitoring and observability&rdquo; sitting inside the orchestration layer — the same lesson as the RAG session. If you cannot see what the system did, you cannot improve it or defend it.
- Also note the data layer holds vector stores *and* knowledge graphs *and* structured data. The interesting enterprise systems are not purely vector-based.
{{% /note %}}

***

<!-- 33 — Framework comparison -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide33.png" >}}
<h1></h1>

{{% note %}}
- The tooling landscape: LangChain, LangGraph, CrewAI, Microsoft Semantic Kernel, AutoGen, Smolagents, AutoGPT — with a comparison table adding LlamaIndex, Swarm and PydanticAI.
- Do not memorise it; this layer moves faster than any slide can track. Read the *shape* instead: some are general application frameworks, some are graph-based orchestration, some are role-based team frameworks, and some enforce structured output.
- The weakness column is the honest one. &ldquo;Debugging is hard&rdquo; against the most popular framework is a real finding, and it connects straight back to observability.
- The leadership point: a framework is a convenience layer, not an architecture. The decisions that matter — which tools, what autonomy, what gets logged, who approves — are the same in all of them.
{{% /note %}}

***

<!-- Framework choice -->
{{< slide class="fs55" >}}

# Don't let the framework be the architecture

<div class="card"><span class="hd">What a framework gives you</span>Plumbing: tool calling, state passing, retries, streaming, traces. Genuinely useful, and increasingly commoditised.</div>
<div class="card"><span class="hd">What it does not give you</span>The autonomy boundary, the approval thresholds, the audit record, the evaluation set, and the answer to who is accountable for an action.</div>
<div class="card warn"><span class="hd">The question to ask</span>&ldquo;If we replaced this framework next year, what would we have to rebuild?&rdquo; If the answer includes your guardrails or your audit trail, they are in the wrong place.</div>

<p class="refs">This layer is young and consolidating. Design so that the framework is replaceable, because it may well be replaced.</p>

{{% note %}}
- Teams choose a framework in week one and inherit its assumptions for the life of the system. Worth one deliberate conversation rather than a default.
- The portability test is the practical one. Guardrails, logging and approval logic should live in your own service layer, in front of the tools, not inside framework callbacks.
- If someone presents a framework choice as the architecture decision, the architecture decision has not been made yet.
{{% /note %}}

***

<!-- ===== SECTION 8 ===== -->
{{< slide background-color="#003478" class="section" >}}

# In the Business

<p>Where this is actually running, and where it is heading</p>

{{% note %}}
Part eight: the industry picture, read with appropriate scepticism.
{{% /note %}}

***

<!-- 34 — CS and healthcare -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide34.png" >}}
<h1></h1>

{{% note %}}
- Customer service and clinical operations. Salesforce Agentforce handling interactions end to end; Microsoft Copilot agents across Microsoft 365; clinical workflow orchestration across triage, bed management and lab scheduling, exchanging data over HL7 FHIR.
- Two things to point out rather than read. First, &ldquo;maintains zero-data-retention for privacy compliance&rdquo; — a **vendor claim**, and exactly the kind of claim to put in a contract rather than a slide. Second, &ldquo;maintains human-in-the-loop oversight for safety&rdquo; in the pharmaceutical column: note that the highest-stakes domain on the slide is the one that keeps a human in the loop.
- General caution: these are largely announcements and vendor case studies. Treat them as evidence that the category is real, not as evidence that any specific number is.
{{% /note %}}

***

<!-- 35 — Energy, manufacturing and finance -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide35.png" >}}
<h1></h1>

{{% note %}}
- Capital-intensive industries: agents across oilfields interacting with digital twins, a multi-agent framework for industrial processes at BMW, natural-language queries over IoT sensor data with failure prediction, and autonomous finance reconciling statements and running compliance checks.
- The pattern across all four: the agent sits on top of systems that *already* had good structured data and clear rules. That is not a coincidence, and it is the most useful thing on the slide.
- Say it plainly: the organisations getting value from agents are the ones that did their data and process work first. If your master data is a mess, an agent will make expensive decisions from it faster.
- The finance row is the one closest to most of this room — reconciliation and compliance checking, high-volume rule-following work with a clear right answer.
{{% /note %}}

***

<!-- 36 — Evolution and future -->
{{< slide content-image="/imgs/slide-30-agentic-systems/Slide36.png" >}}
<h1></h1>

{{% note %}}
- The progression: traditional AI reacting to inputs, AI agents with perception-action loops, agentic AI as proactive self-improving systems. And the transformation: from automating single tasks to managing operations.
- The three challenges listed are the right three, and they are governance problems rather than model problems: **interpretability**, **safety**, and **accountability** — &ldquo;establishing responsibility frameworks.&rdquo;
- That last one is where this room comes in. There is no technical solution to the question of who is responsible when an autonomous system acts. It is an organisational decision that has to be made before deployment, not after an incident.
- &ldquo;Integration with legacy enterprise infrastructure&rdquo; under strategic outlook is the unglamorous truth: most of the work ahead is plumbing into systems built decades ago.
{{% /note %}}

***

<!-- Autonomy levels -->
{{< slide class="fs55" >}}

# The autonomy dial

<table class="plain">
<tr><th>Level</th><th>The system&hellip;</th><th>Appropriate when</th><th>What must exist</th></tr>
<tr><td class="lv">1 &middot; Advise</td><td>Drafts or recommends; a human does everything</td><td>Judgement-heavy, high-stakes, or novel work</td><td>Nothing beyond normal review</td></tr>
<tr><td class="lv">2 &middot; Act on approval</td><td>Prepares the action; a human clicks</td><td>Reversible but material actions</td><td>A reviewer who has time to actually look</td></tr>
<tr><td class="lv">3 &middot; Act and notify</td><td>Acts within limits; a human is told after</td><td>High-volume, low-value, easily reversed</td><td>Hard ceilings in code, alerting, and an undo</td></tr>
<tr><td class="lv">4 &middot; Act silently</td><td>Acts; only exceptions surface</td><td>Well-understood, measured, low-variance work</td><td>Monitoring, sampling, and a named owner</td></tr>
</table>

<p class="refs">The level is set <strong>per tool</strong>, not per system. The same agent can read at level 4, draft at level 1, and refund at level 2.</p>

{{% note %}}
- This is the slide to photograph, and the one to bring to your own governance conversation.
- The critical design insight is the footnote: autonomy is set per action, not per system. Most disagreements about &ldquo;how autonomous should this be&rdquo; dissolve once you break it into individual tools.
- Level 2 has a specific failure mode worth naming — **rubber-stamping**. An approval step where the reviewer approves 200 items an hour is a level 3 system with extra paperwork and a person to blame. If you rely on approval, measure the rejection rate.
- Level 3 is where most enterprise value sits today, and it is only safe with ceilings enforced in code and a working undo.
{{% /note %}}

***

<!-- ===== DISCUSSION ===== -->
{{< slide background-color="#003478" class="section" >}}

# Class Discussion

{{% note %}}
Five questions. Small groups, then report back.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 1
# Setting the Dial

Your service organisation wants an agent that can issue refunds, update shipping addresses, apply account credits, and cancel subscriptions.

<p class="q">Assign an autonomy level to each of those four actions and justify the differences. Which one would you refuse to automate at all, and what would change your mind?</p>

{{% note %}}
- Looking for per-tool reasoning: address updates are low-stakes and reversible; refunds are material but bounded; account credits create liability; cancellations may be irreversible and have retention consequences.
- Push on reversibility as the organising criterion, and on the *ceiling* — a refund agent at level 3 up to $\$50$ and level 2 above it is a perfectly good answer.
- "What would change your mind" is the real question: usually measured error rates from a period at a lower level.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 2
# Workflow or Agent?

A team proposes a multi-agent system to handle supplier onboarding: collect documents, verify registration, check sanctions lists, score risk, and create the vendor record.

<p class="q">How much of that is genuinely agentic, and how much is a workflow with one uncertain step? What would you approve, and what would you send back?</p>

{{% note %}}
- Most of it is a deterministic workflow. Sanctions screening in particular must be a deterministic check against an authoritative list — never a model's judgement.
- The genuinely uncertain steps are document extraction from heterogeneous formats and perhaps risk scoring on unstructured inputs.
- The answer to look for: build the workflow, use models only at the uncertain steps, and do not let a model decide whether a sanctions hit is a match.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 3
# The Tool List

You are shown an agent design. Its tool list includes `search_knowledge_base`, `send_email_to_customer`, `update_crm_record`, `issue_refund`, and `execute_sql`.

<p class="q">Which of these worry you, and why? What controls would you require before any of them ships &mdash; and which would you strike from the list?</p>

{{% note %}}
- `execute_sql` is the one to strike, or confine to a read-only replica with a fixed schema. Arbitrary query execution driven by natural language is both a data-exfiltration and a data-integrity risk.
- `send_email_to_customer` is underrated: it is irreversible, it is external, and it speaks in the company's voice.
- Controls to look for: per-tool authorisation, hard ceilings in the wrapper rather than the prompt, idempotency, full audit logging, and a rollback path.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 4
# Who Is Accountable?

An agent in your firm takes a defensible-looking action that turns out to be wrong and costs a client money. The trace shows the model chose a reasonable path from the information it had; the information was stale.

<p class="q">Who is accountable &mdash; and how would you have had to structure the project beforehand for that answer to be clear?</p>

{{% note %}}
- The answer is never "the model." Candidates: the process owner who set the autonomy level, the data owner whose feed was stale, the engineering owner who did not check freshness.
- What has to exist beforehand: a named owner per tool, an agreed autonomy level, data freshness requirements written down, and a trace you can reconstruct.
- Connect to the Responsible AI session — this is the accountability gap that framework material addresses directly.
{{% /note %}}

***

{{< slide class="dq fs60" >}}

### Discussion Question 5
# Synthesis

Take the RAG project from the last session &mdash; the knowledge assistant over policies and handbooks. Your CEO now asks why it can only answer questions when &ldquo;everyone says agents can actually do things.&rdquo;

<p class="q">Redesign it as an agent. What tools would you give it, at what autonomy level, with what guardrails? What does the phase-one scope look like, and what would you tell the CEO you are deliberately *not* doing yet?</p>

{{% note %}}
- Strong answers start at level 1 and level 2 tools: draft a response, raise a ticket, schedule a meeting, prefill a form. Nothing irreversible in phase one.
- The deliberate omissions are the interesting part: no writes to systems of record, no external communication, no financial actions.
- Best answers note that the evaluation harness from the RAG session must be extended — you are now measuring actions taken, not just answers given, and "was the answer right" becomes "was the action correct, authorised, and reversible."
{{% /note %}}

***

<!-- ===== TAKEAWAYS ===== -->
{{< slide class="fs60" >}}

# Takeaways

<div class="card"><span class="hd">RAG is a pattern; an agent is a process</span>The retrieval system becomes a tool the agent chooses to use. Everything you built last session survives &mdash; as a component.</div>
<div class="card"><span class="hd">Every tool is a permission</span>A one-line function signature is a standing grant of authority to a probabilistic system. Review it as such.</div>
<div class="card"><span class="hd">Set the autonomy dial per action, not per system</span>Read at level 4, draft at level 1, spend money at level 2. Ceilings belong in code, not in prompts.</div>
<div class="card"><span class="hd">Most &ldquo;agentic&rdquo; proposals are workflows with one uncertain step</span>Build the deterministic part deterministically. Reach for a team of agents only when the work has genuinely different kinds of task.</div>

{{% note %}}
- If one sentence survives the session: **the question is not what the system can do, it is what it is allowed to do without asking.**
- The through-line across all three sessions: the model is not the system, the system is not one system, and now — the system does not only speak, it acts. Each step adds capability and subtracts the ability to test exhaustively.
{{% /note %}}

***

<!-- ===== CREDITS ===== -->
{{< slide class="fs55" >}}

# Sources &amp; Figure Credits

<div class="card"><span class="hd">Agent foundations and the classical taxonomy</span>
Stuart Russell &amp; Peter Norvig, <em>Artificial Intelligence: A Modern Approach</em> &mdash; the sensor/actuator definition and the five classic agent types (simple reflex, model-based, goal-based, utility-based, learning).</div>

<div class="card"><span class="hd">The four agentic design patterns</span>
Yugank Aman, &ldquo;Top Agentic AI Design Patterns for Architecting AI Systems,&rdquo; <em>Medium</em> &mdash; credited on the figures themselves. The Self-RAG comparison originates with Asai et al., <em>Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection</em> (2023).</div>

<div class="card"><span class="hd">Architecture diagrams</span>
The agentic search architecture is credited on the figure to <em>@rakeshgohel01</em>. Framework comparisons reflect a fast-moving landscape and will date quickly.</div>

<div class="card warn"><span class="hd">About these figures</span>
Several diagrams in this deck were generated with <strong>NotebookLM</strong>; the industry slides report <strong>vendor and press claims</strong> that have not been independently verified. Useful as a map of the category &mdash; not as evidence for any specific number.</div>

{{% note %}}
- Worth saying the last card out loud. In a session about delegating action to machines, being explicit about which claims are verified and which are marketing is part of the lesson.
- If anyone wants to go deeper: Russell and Norvig for the foundations, and the Self-RAG paper for a concrete, readable example of reflection applied to retrieval.
{{% /note %}}
