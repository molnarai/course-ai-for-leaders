+++
title = "Business Solutions"
description = "Agents in ten slides, then six agentic business solutions read the same way — the job, the team, the value hypothesis, and the evidence"
weight = 35
outputs = ["Reveal"]
math = true
thumbnail = "/imgs/slides/agentic-ai-enterprise-workflows.png"

[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"
+++

<!--
    Slide deck: Business Solutions.

    Outline:
      0. Opening            — title, outline
      1. Agents in ten slides — condensed from slide-30-agentic-systems, which
                               was not shown in class. Its figures are redrawn
                               here as native HTML and inline SVG (class "dg").
      2. Six solutions, and how to read them — selection, template, evidence types
      3. Knowledge work     — enterprise knowledge and research; software engineering
      4. Operations         — IT service and incident ops; supply chain and procurement
      5. Revenue & customer — customer-service resolution; sales and marketing
      6. Across the six     — industry matrix, shared foundation, design boundary
      7. Discussion, takeaways, sources

    Each solution uses the same four slides: the job, the team, the value
    hypothesis, the evidence. Source material is in slide-business-solutions/
    (SIX_BUSINESS_SOLUTIONS.md, INDUSTRIES.md, REFERENCES.md).

    The tool lists and autonomy levels on the "team" slides are illustrative
    teaching material, not taken from the cited references.

    Every content slide carries speaker notes in a note block.
-->

<style>
/* Helper classes for this deck. Palette follows reveal-robinson.css —
   GSU Blue #003478, GSU Crimson #CC0000. Kept in sync with slide-30-agentic-systems. */

/* reveal-robinson.css pads sections by 50px with box-sizing: content-box, which
   makes every section 1060px wide on a 960px stage and clips text off the right
   edge. Scoped correction so the native slides fit. */
.reveal .slides section { box-sizing: border-box; }

.reveal .slides section.fs66 { font-size: 0.66em; }
.reveal .slides section.fs60 { font-size: 0.60em; }
.reveal .slides section.fs55 { font-size: 0.55em; }
.reveal .slides section.fs50 { font-size: 0.50em; }
.reveal .slides section.fs45 { font-size: 0.45em; }
.reveal .slides section[class*="fs"] h1 { font-size: 52px; margin-bottom: 0.4em; }

.reveal .cols2 { display: grid; grid-template-columns: 1fr 1fr; gap: 0 1.8em; align-items: start; }
.reveal .cols3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0 1.4em; align-items: start; }
/* Four cards in one row, stretched to equal height. */
.reveal .cols4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 0 1em; align-items: stretch; }
/* Sub-boxes nested inside a card: white, equal size, no bottom margin. */
.reveal .cols4.sub4 { gap: 0 0.7em; margin-top: 0.45em; }
.reveal .cols4.sub4 .card { background: #fff; margin: 0; }
.reveal .cols2 p, .reveal .cols3 p { margin: 0.35em 0; }

.reveal .sub { color: #CC0000; font-weight: 700; margin: 0.8em 0 0.25em 0; }
.reveal .cols2 > div > .sub:first-child,
.reveal .cols3 > div > .sub:first-child { margin-top: 0; }

.reveal .card { background: #f4f6f9; border-left: 4px solid #003478;
                border-radius: 6px; padding: 0.5em 0.9em; margin: 0 0 0.55em 0; }
.reveal .card .hd { color: #003478; font-weight: 700; display: block; margin-bottom: 0.3em; }
.reveal .card.warn { border-left-color: #CC0000; }
.reveal .card.warn .hd { color: #CC0000; }

.reveal .term { color: #CC0000; font-weight: 700; }
.reveal .lead { font-style: italic; color: #555; margin-bottom: 0.8em; }
.reveal .refs { font-size: 0.62em; color: #777; margin-top: 0.9em; }
.reveal .refs a { color: #777; }

/* Kicker above a solution slide title: which solution, which of the four slides. */
.reveal .kicker { color: #CC0000; font-weight: 700; font-size: 0.8em;
                  text-transform: uppercase; letter-spacing: 0.04em; margin: 0 0 0.2em 0; }

/* The theme shrinks tables to 0.75em. Give every table in this deck one fixed
   size (0.6 of the base), whatever fs class its slide uses. */
.reveal table.plain { width: 100%; border-collapse: collapse;
                      font-size: calc(var(--r-main-font-size) * 0.6); }
.reveal table.plain th { color: #003478; text-align: left; border-bottom: 2px solid #003478;
                         padding: 0.3em 0.5em; }
.reveal table.plain td { border-bottom: 1px solid #ddd; padding: 0.3em 0.5em; vertical-align: top; }
.reveal table.plain td.lv { color: #CC0000; font-weight: 700; white-space: nowrap; }
.reveal table.plain td.c, .reveal table.plain th.c { text-align: center; }

/* Inline SVG diagrams. Drawn at the slide's content width (860px) so the
   font sizes below are true pixel sizes on the 960px stage. */
.reveal svg.dg { display: block; width: 100%; height: auto; margin: 0 auto; overflow: visible; }
.reveal svg.dg text { font-size: 19px; fill: #222; }
.reveal svg.dg .t-c { text-anchor: middle; }
.reveal svg.dg .t-b { font-weight: 700; }
.reveal svg.dg .t-m { font-size: 16px; }
.reveal svg.dg .t-s { font-size: 14px; fill: #666; }
.reveal svg.dg .t-w { fill: #fff; }
.reveal svg.dg .t-blue { fill: #003478; }
.reveal svg.dg .t-red { fill: #CC0000; }
.reveal svg.dg .bx { fill: #f4f6f9; stroke: #003478; stroke-width: 2; }
.reveal svg.dg .bx-b { fill: #003478; stroke: #003478; stroke-width: 2; }
.reveal svg.dg .bx-r { fill: #fdf0f0; stroke: #CC0000; stroke-width: 2; }
.reveal svg.dg .bx-rf { fill: #CC0000; stroke: #CC0000; stroke-width: 2; }
.reveal svg.dg .bx-g { fill: #f2f2f2; stroke: #999; stroke-width: 2; }
.reveal svg.dg .bx-p { fill: #f4f6f9; stroke: none; }
.reveal svg.dg .ln { fill: none; stroke: #003478; stroke-width: 2.5; }
.reveal svg.dg .ln-g { fill: none; stroke: #999; stroke-width: 2.5; }
.reveal svg.dg .ln-d { stroke-dasharray: 3 6; stroke-linecap: round; }

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

<!-- ===== TITLE ===== -->
{{< slide background-color="#003478" class="section" >}}

# Agentic AI<br>Business Solutions

<p>EMBA 8160 &mdash; AI for Leaders</p>

{{% note %}}
- Two halves today. First, what an agent actually is, in ten slides. Then six business solutions you are likely to be pitched, each read the same way.
- Everything so far in the course has been about systems that *answer*. Today is about systems that *act* — and about deciding which of them deserve your budget.
{{% /note %}}

***

<!-- ===== OUTLINE ===== -->
{{< slide class="fs60" >}}

# Outline

<p class="lead">Hold one question throughout: which of these would you fund, and what evidence would you need first?</p>

<div class="cols2">
<div>
<p><span class="term">1.</span> Agents in ten slides</p>
<p><span class="term">2.</span> Six solutions, and how to read them</p>
<p><span class="term">3.</span> Knowledge work</p>
<p><span class="term">4.</span> Operations</p>
</div>
<div>
<p><span class="term">5.</span> Revenue and customer</p>
<p><span class="term">6.</span> Across the six</p>
<p><span class="term">7.</span> Discussion</p>
</div>
</div>

{{% note %}}
- Part 1 is the vocabulary: the loop, tools, multi-agent teams, and the autonomy dial. It is deliberately short.
- Parts 3 to 5 walk through six solutions in three pairs. The pairs are ordered by where the action lands — inside the firm's knowledge, inside its systems, then in front of customers — so the stakes rise as we go.
- Part 6 steps back: what the evidence does and does not show across all six.
{{% /note %}}

***

<!-- ===== SECTION 1 — PRIMER ===== -->
{{< slide background-color="#003478" class="section" >}}

# Agents

<p>From a pattern that answers to a process that acts</p>

{{% note %}}
Part one: the minimum vocabulary needed to read a vendor pitch or an internal proposal.
{{% /note %}}

***

<!-- Primer 1 — What is an AI agent? -->
{{< slide class="fs55" >}}

# What is an AI agent?

<p class="lead">An autonomous system capable of <strong>perceiving its environment</strong>, reasoning over information, <strong>planning courses of action</strong>, and <strong>executing tasks</strong> on behalf of a user.</p>

<div class="cols4">
<div class="card"><span class="hd">Foundational definition</span>&ldquo;Anything perceiving its environment through sensors and acting upon it through actuators&rdquo; (Russell &amp; Norvig). Fundamentally distinct from a static model.</div>
<div class="card"><span class="hd">Perception-action loop</span>Continuous observation and decision-making. Moves beyond a single prompt and response, and adapts across multiple steps.</div>
<div class="card"><span class="hd">Cognitive backbone</span>Powered by a large language model, augmented by memory modules, with planning and tool-integration layers.</div>
<div class="card warn"><span class="hd">Beyond chatbots</span>Decomposes complex problems into subtasks, maintains context over long horizons, and integrates external tools to extend what it can do.</div>
</div>

{{% note %}}
- The working definition: a system that **perceives** its environment, **reasons** over what it finds, **plans** a course of action, and **executes** on behalf of a user.
- The idea is decades older than ChatGPT — Russell and Norvig's &ldquo;anything perceiving its environment through sensors and acting upon it through actuators.&rdquo; The language model is a new engine in an old architecture.
- The commercial distinction: a **perception-action loop** rather than one prompt and one response. A chatbot's output is text. An agent's output is a *changed system*.
{{% /note %}}

***

<!-- Primer 2 — The agent: a process that controls patterns -->
{{< slide class="fs55" >}}

# A process that controls patterns

<svg class="dg" viewBox="0 0 860 390" role="img" aria-label="RAG as a fixed pattern of query, retrieve, generate, answer, compared with an agent loop of goal, plan, decide, act, evaluate, where RAG, APIs and a code interpreter are tools the agent chooses between">
<defs>
<marker id="pp-b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#003478"/></marker>
<marker id="pp-g" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#999"/></marker>
</defs>
<text x="0" y="30" class="t-b" style="fill:#777">The pattern: RAG</text>
<rect class="bx-g" x="200" y="6" width="110" height="38" rx="6"/><text class="t-c" x="255" y="31">Query</text>
<rect class="bx-g" x="350" y="6" width="110" height="38" rx="6"/><text class="t-c" x="405" y="31">Retrieve</text>
<rect class="bx-g" x="500" y="6" width="110" height="38" rx="6"/><text class="t-c" x="555" y="31">Generate</text>
<rect class="bx-g" x="650" y="6" width="110" height="38" rx="6"/><text class="t-c" x="705" y="31">Answer</text>
<path class="ln-g" d="M310 25H348" marker-end="url(#pp-g)"/>
<path class="ln-g" d="M460 25H498" marker-end="url(#pp-g)"/>
<path class="ln-g" d="M610 25H648" marker-end="url(#pp-g)"/>
<text x="200" y="68" class="t-s">Fixed control flow: a pre-determined path with no branching.</text>
<path d="M0 88H860" stroke="#ddd" stroke-width="1"/>
<text x="0" y="122" class="t-b t-blue">The process: an agent</text>
<rect class="bx-b" x="0" y="218" width="90" height="44" rx="6"/><text class="t-c t-b t-w" x="45" y="246">Goal</text>
<rect class="bx" x="125" y="218" width="90" height="44" rx="6"/><text class="t-c" x="170" y="246">Plan</text>
<rect class="bx-rf" x="250" y="218" width="110" height="44" rx="6"/><text class="t-c t-b t-w" x="305" y="246">Decide</text>
<rect class="bx" x="420" y="150" width="170" height="44" rx="6"/><text class="t-c" x="505" y="178">RAG</text>
<rect class="bx" x="420" y="218" width="170" height="44" rx="6"/><text class="t-c" x="505" y="246">APIs</text>
<rect class="bx" x="420" y="286" width="170" height="44" rx="6"/><text class="t-c" x="505" y="314">Code interpreter</text>
<rect class="bx" x="650" y="218" width="90" height="44" rx="6"/><text class="t-c" x="695" y="246">Act</text>
<rect class="bx" x="770" y="218" width="90" height="44" rx="6"/><text class="t-c" x="815" y="246">Evaluate</text>
<path class="ln" d="M90 240H123" marker-end="url(#pp-b)"/>
<path class="ln" d="M215 240H248" marker-end="url(#pp-b)"/>
<path class="ln" d="M360 230L418 174" marker-end="url(#pp-b)"/>
<path class="ln" d="M360 240H418" marker-end="url(#pp-b)"/>
<path class="ln" d="M360 250L418 306" marker-end="url(#pp-b)"/>
<path class="ln" d="M590 174L648 230" marker-end="url(#pp-b)"/>
<path class="ln" d="M590 240H648" marker-end="url(#pp-b)"/>
<path class="ln" d="M590 306L648 250" marker-end="url(#pp-b)"/>
<path class="ln" d="M740 240H768" marker-end="url(#pp-b)"/>
<path class="ln" d="M815 262V372H170V265" marker-end="url(#pp-b)"/>
<text class="t-c t-s" x="492" y="364">Goal not met: plan again</text>
</svg>

<p class="refs"><strong>RAG becomes a tool the agent chooses to use</strong>, not the architecture of the system.</p>

{{% note %}}
- The RAG systems from earlier sessions are a straight line: query, retrieve, generate, answer. Fixed path, one static goal, no action.
- Here that line becomes one option inside a loop: goal, plan, **decide**, act, evaluate — and back to plan if the goal is not met.
- Look at what sits behind &ldquo;decide&rdquo;: RAG, APIs, a code interpreter. **RAG becomes a tool the agent chooses to use**, not the architecture of the system.
- The governance consequence arrives with the word &ldquo;decide.&rdquo; A fixed path can be tested exhaustively. A system that chooses its own path cannot — you test the *policy*, not the path.
{{% /note %}}

***

<!-- Primer 3 — The agentic loop -->
{{< slide class="fs55" >}}

# The agentic loop

<svg class="dg" viewBox="0 0 860 390" role="img" aria-label="A four-step cycle: perceive, decide, act, remember, repeating until the goal is met">
<defs>
<marker id="lp-b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#003478"/></marker>
</defs>
<rect class="bx-g" x="185" y="35" width="130" height="50" rx="8"/><text class="t-c t-b" x="250" y="67">Perceive</text>
<rect class="bx-rf" x="355" y="175" width="130" height="50" rx="8"/><text class="t-c t-b t-w" x="420" y="207">Decide</text>
<rect class="bx-b" x="185" y="315" width="130" height="50" rx="8"/><text class="t-c t-b t-w" x="250" y="347">Act</text>
<rect class="bx" x="15" y="175" width="130" height="50" rx="8"/><text class="t-c t-b" x="80" y="207">Remember</text>
<path class="ln" d="M315 60Q420 60 420 172" marker-end="url(#lp-b)"/>
<path class="ln" d="M420 225Q420 340 318 340" marker-end="url(#lp-b)"/>
<path class="ln" d="M185 340Q80 340 80 228" marker-end="url(#lp-b)"/>
<path class="ln" d="M80 175Q80 60 182 60" marker-end="url(#lp-b)"/>
<text class="t-c t-s" x="250" y="196">repeat until</text>
<text class="t-c t-s" x="250" y="216">the goal is met</text>
<text x="560" y="70" class="t-b">1. Perceive</text><text x="560" y="94" class="t-m">Input handling</text>
<text x="560" y="150" class="t-b t-red">2. Decide</text><text x="560" y="174" class="t-m">Planning and reasoning</text>
<text x="560" y="230" class="t-b t-blue">3. Act</text><text x="560" y="254" class="t-m">Tool usage and interaction</text>
<text x="560" y="310" class="t-b">4. Remember</text><text x="560" y="334" class="t-m">Storing state and history</text>
</svg>

{{% note %}}
- The loop in four words: **perceive, decide, act, remember**.
- **Decide** is the model: it decomposes the goal into steps and chooses which tool to use next.
- **Remember** is the one people skip. Without state an agent repeats itself and cannot explain what it did. The structured state — not the chat history — is the record you replay in a dispute.
- Because it is a loop, it can also fail to stop. Step limits and budget caps are part of the design, not an afterthought.
{{% /note %}}

***

<!-- Primer 4 — Tools and environment interfaces -->
{{< slide class="fs55" >}}

# Tools and environment interfaces

<div class="cols2">
<div>
<svg class="dg" viewBox="0 0 412 300" role="img" aria-label="The act step connects to three kinds of tool: a RAG retriever, SaaS APIs such as a CRM, and transactional systems">
<rect class="bx-b" x="0" y="125" width="100" height="50" rx="8"/><text class="t-c t-b t-w" x="50" y="157">Act</text>
<path class="ln" d="M100 150L170 50"/>
<path class="ln" d="M100 150H170"/>
<path class="ln" d="M100 150L170 250"/>
<rect class="bx" x="170" y="20" width="240" height="60" rx="8"/><text class="t-b" x="186" y="46">RAG retriever</text><text class="t-s" x="186" y="67">reads documents</text>
<rect class="bx" x="170" y="120" width="240" height="60" rx="8"/><text class="t-b" x="186" y="146">SaaS APIs</text><text class="t-s" x="186" y="167">updates the CRM</text>
<rect class="bx-r" x="170" y="220" width="240" height="60" rx="8"/><text class="t-b" x="186" y="246">Transactional systems</text><text class="t-s" x="186" y="267">moves money</text>
</svg>
</div>
<div>
<p class="sub">Action capabilities</p>
<p>Connectors that allow the agent to affect the world, not just speak about it.</p>
<div class="card" style="margin-top:0.8em"><code>tools = [<br>&nbsp;&nbsp;client.search_docs(),<br>&nbsp;&nbsp;crm.update_record(),<br>&nbsp;&nbsp;payment.issue_refund()<br>]</code></div>
</div>
</div>

{{% note %}}
- The **act** quadrant, and where the risk conversation begins: connectors that let the agent affect the world, not just speak about it.
- Look at the tool list in the code box: `search_docs`, `update_record`, `issue_refund`. Three lines, and the third one moves money.
- Engineers see a list of functions. The business should see a **list of permissions granted to a non-deterministic system**. It is the same list.
{{% /note %}}

***

<!-- Primer 5 — Tools are permissions -->
{{< slide class="fs55" >}}

# Every tool is a permission

<div class="cols2">
<div>
<p class="sub">What the team sees</p>
<div class="card"><span class="hd">A function signature</span><code>payment.issue_refund(order_id, amount)</code><br>Two parameters, one line of configuration.</div>
<p>Adding a tool is a ten-minute task. That is what makes agents powerful.</p>
</div>
<div>
<p class="sub">What you are approving</p>
<div class="card warn"><span class="hd">A standing authority</span>A probabilistic system may move money, on its own judgement, at a rate limited only by how often people ask.</div>
<p>The same ten minutes, from the other side of the table.</p>
</div>
</div>

<p class="refs">Ask for four things per tool: <strong>who authorised it</strong>, <strong>what the blast radius is</strong>, <strong>what the ceiling is</strong>, and <strong>how it gets reversed</strong>.</p>

{{% note %}}
- The gap between how cheap it is to add a tool and how consequential the tool is, is the central governance problem of agentic systems.
- A limit written in a prompt is a *request*. A limit enforced in the tool wrapper is a **control**. Auditors care about the second kind.
- We will read every one of the six solutions through its tool list.
{{% /note %}}

***

<!-- Primer 6 — Under the hood: the refund logic -->
{{< slide class="fs55" >}}

# Under the hood: the refund logic

<svg class="dg" viewBox="0 0 860 402" role="img" aria-label="A refund request traced step by step: user input, the model classifies and plans, a CRM lookup, a billing lookup, a coded check that the order is within 30 days, the refund call, a log to memory, and the reply">
<defs>
<marker id="rf-g" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#999"/></marker>
</defs>
<rect class="bx-g" x="150" y="1" width="300" height="36" rx="6"/><text class="t-c" x="300" y="26"><tspan class="t-b">User input:</tspan> &#8220;Refund please&#8221;</text>
<rect class="bx-r" x="150" y="53" width="300" height="36" rx="6"/><text class="t-c" x="300" y="78"><tspan class="t-b">LLM:</tspan> classify and plan</text>
<text class="t-s" x="462" y="77">Intent: refund</text>
<rect class="bx" x="150" y="105" width="300" height="36" rx="6"/><text class="t-c" x="300" y="130"><tspan class="t-b">Tool:</tspan> CRM API (get profile)</text>
<rect class="bx" x="150" y="157" width="300" height="36" rx="6"/><text class="t-c" x="300" y="182"><tspan class="t-b">Tool:</tspan> Billing API (check date)</text>
<path class="bx" d="M130 227L160 207H440L470 227L440 247H160Z"/><text class="t-c" x="300" y="234"><tspan class="t-b">Logic check:</tspan> within 30 days?</text>
<rect class="bx" x="150" y="261" width="300" height="36" rx="6"/><text class="t-c" x="300" y="286"><tspan class="t-b">Tool:</tspan> execute_refund()</text>
<rect class="bx" x="150" y="313" width="300" height="36" rx="6"/><text class="t-c" x="300" y="338"><tspan class="t-b">Memory:</tspan> log to history</text>
<rect class="bx-g" x="150" y="365" width="300" height="36" rx="6"/><text class="t-c" x="300" y="390"><tspan class="t-b">Output:</tspan> &#8220;Refund processed.&#8221;</text>
<path class="ln-g" d="M300 37V51" marker-end="url(#rf-g)"/>
<path class="ln-g" d="M300 89V103" marker-end="url(#rf-g)"/>
<path class="ln-g" d="M300 141V155" marker-end="url(#rf-g)"/>
<path class="ln-g" d="M300 193V205" marker-end="url(#rf-g)"/>
<path class="ln-g" d="M300 247V259" marker-end="url(#rf-g)"/>
<path class="ln-g" d="M300 297V311" marker-end="url(#rf-g)"/>
<path class="ln-g" d="M300 349V363" marker-end="url(#rf-g)"/>
<text class="t-s" x="312" y="258">Yes</text>
<path class="ln-g" d="M470 227H588" marker-end="url(#rf-g)"/><text class="t-s" x="520" y="219">No</text>
<rect class="bx-g" x="590" y="209" width="200" height="36" rx="6"/><text class="t-c" x="690" y="234">Hand to a person</text>
<rect class="bx-r" x="590" y="20" width="26" height="20" rx="4"/><text class="t-m" x="626" y="36">Model judgement</text>
<rect class="bx" x="590" y="52" width="26" height="20" rx="4"/><text class="t-m" x="626" y="68">Deterministic call or rule</text>
<rect class="bx-g" x="590" y="84" width="26" height="20" rx="4"/><text class="t-m" x="626" y="100">Input, output, hand-off</text>
</svg>

{{% note %}}
- One concrete transaction. A customer writes &ldquo;I need a refund for my last order.&rdquo; Four things must happen: verify identity, retrieve the purchase, check the business rule, execute the refund. A chatbot can explain the policy; an agent applies it.
- Two colours, two kinds of step. The **red step is model judgement**; the **blue steps are deterministic calls and rules**. Good design pushes as much as possible into blue.
- The &ldquo;within 30 days?&rdquo; check is a business rule evaluated in code, not by the model. Phrased as a prompt instruction it would hold most of the time — and most of the time is not a policy.
- This trace is also the audit record. If a team cannot produce a picture like this for a real transaction, the system is not ready for production.
{{% /note %}}

***

<!-- Primer 7 — The multi-agent architecture -->
{{< slide class="fs55" >}}

# The multi-agent architecture

<div style="display:grid; grid-template-columns:2.6fr 1fr; gap:0 1.6em; align-items:center">
<div>
<svg class="dg" viewBox="0 0 600 362" role="img" aria-label="An orchestrator routes work to three specialised agents, a planner, an executor and a quality checker, which all read from and write to a shared blackboard">
<defs>
<marker id="ma-b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto-start-reverse"><path d="M0 0L10 5L0 10z" fill="#003478"/></marker>
</defs>
<rect class="bx-b" x="200" y="2" width="200" height="60" rx="8"/><text class="t-c t-b t-w" x="300" y="39">The orchestrator</text>
<path class="ln" d="M245 64L100 148" marker-start="url(#ma-b)" marker-end="url(#ma-b)"/>
<path class="ln" d="M300 64V148" marker-start="url(#ma-b)" marker-end="url(#ma-b)"/>
<path class="ln" d="M355 64L500 148" marker-start="url(#ma-b)" marker-end="url(#ma-b)"/>
<rect class="bx" x="0" y="150" width="180" height="60" rx="8"/><text class="t-c t-b" x="90" y="176">Agent A</text><text class="t-c t-s" x="90" y="197">Planner</text>
<rect class="bx" x="210" y="150" width="180" height="60" rx="8"/><text class="t-c t-b" x="300" y="176">Agent B</text><text class="t-c t-s" x="300" y="197">Executor</text>
<rect class="bx" x="420" y="150" width="180" height="60" rx="8"/><text class="t-c t-b" x="510" y="176">Agent C</text><text class="t-c t-s" x="510" y="197">Quality check</text>
<path class="ln ln-d" d="M90 212V298"/>
<path class="ln ln-d" d="M300 212V298"/>
<path class="ln ln-d" d="M510 212V298"/>
<text class="t-s" x="312" y="260">read and write</text>
<rect class="bx" x="0" y="300" width="600" height="60" rx="8" style="fill:#dbe6f4"/><text class="t-c t-b" x="300" y="326">Shared state / blackboard</text><text class="t-c t-s" x="300" y="347">the plan, intermediate results, drafts</text>
</svg>
</div>
<div>
<div class="card"><span class="hd">The manager</span>The orchestrator controls flow, routes outputs, and decides when the goal is met.</div>
<div class="card"><span class="hd">The workspace</span>Agents do not talk to each other directly. They publish to a shared board.</div>
</div>
</div>

{{% note %}}
- When one agent is not enough, the work is split by **role** rather than by step: each agent gets its own instructions and its own tools.
- Two structural pieces: the **orchestrator**, which routes work and decides when the goal is met, and the **shared state or blackboard**, the common workspace all agents read from and write to.
- Every solution in the second half is drawn as a small team like this. Two questions to carry forward: **who decides the goal is met**, and **which agent is accountable for the final output?**
{{% /note %}}

***

<!-- How an LLM plans and reasons -->
{{< slide class="fs50" >}}

# How an LLM plans and reasons

<div style="display:grid; grid-template-columns:1.45fr 1fr; gap:0 1.6em; align-items:center">
<div>
<svg class="dg" viewBox="0 0 520 352" role="img" aria-label="A ReAct trace for a refund: the model alternates thoughts and actions, the system returns observations, until the model gives an answer">
<defs>
<marker id="ra-b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#003478"/></marker>
</defs>
<rect class="bx-g" x="0" y="4" width="118" height="34" rx="17"/><text class="t-c t-b t-m " x="59" y="27">Goal</text><text class="t-m" x="134" y="27">Customer asks for a refund on order 1182</text>
<rect class="bx-rf" x="0" y="48" width="118" height="34" rx="17"/><text class="t-c t-b t-m t-w" x="59" y="71">Thought</text><text class="t-m" x="134" y="71">I need the order date and amount first.</text>
<rect class="bx-rf" x="0" y="92" width="118" height="34" rx="17"/><text class="t-c t-b t-m t-w" x="59" y="115">Action</text><text class="t-m" x="134" y="115" style="font-family:monospace">lookup_order(1182)</text>
<rect class="bx-b" x="0" y="136" width="118" height="34" rx="17"/><text class="t-c t-b t-m t-w" x="59" y="159">Observation</text><text class="t-m" x="134" y="159" style="font-family:monospace">date: 2 Sep, amount: 45.00</text>
<rect class="bx-rf" x="0" y="180" width="118" height="34" rx="17"/><text class="t-c t-b t-m t-w" x="59" y="203">Thought</text><text class="t-m" x="134" y="203">Within 30 days and under the ceiling.</text>
<rect class="bx-rf" x="0" y="224" width="118" height="34" rx="17"/><text class="t-c t-b t-m t-w" x="59" y="247">Action</text><text class="t-m" x="134" y="247" style="font-family:monospace">issue_refund(1182, 45.00)</text>
<rect class="bx-b" x="0" y="268" width="118" height="34" rx="17"/><text class="t-c t-b t-m t-w" x="59" y="291">Observation</text><text class="t-m" x="134" y="291" style="font-family:monospace">status: refunded</text>
<rect class="bx-g" x="0" y="312" width="118" height="34" rx="17"/><text class="t-c t-b t-m " x="59" y="335">Answer</text><text class="t-m" x="134" y="335">&#8220;Your refund of 45.00 is on its way.&#8221;</text>
<path class="ln" d="M508 301H516V65H510" marker-end="url(#ra-b)"/>
</svg>
</div>
<div>
<div class="card"><span class="hd">1 &middot; Instructions</span>A system prompt states the goal, the role, the rules and the tools available. Examples of good behaviour help.</div>
<div class="card"><span class="hd">2 &middot; Think before acting</span>The model is asked to plan first, or is a <em>reasoning model</em> trained to work through a problem before it answers.</div>
<div class="card"><span class="hd">3 &middot; A loop around it</span>Software feeds each result back into the conversation and asks again, until the model answers or a step limit is hit.</div>
</div>
</div>

<p class="refs">This pattern is called <strong>ReAct</strong>: reason, act, observe, repeat. The plan lives in the conversation; it is text the model wrote, not a separate planner.</p>

{{% note %}}
- An LLM still only predicts the next token. Planning and reasoning are not a separate engine; they are text the model is prompted, or trained, to write before it acts.
- Three ingredients. Instructions in a system prompt. A habit of thinking first: either we ask for a plan, or we use a reasoning model, which has been trained to produce a long internal working-out before answering. And a loop: ordinary software that runs the model, executes what it asks for, feeds the result back, and asks again.
- Walk the trace on the left. Red rows are written by the model. Blue rows come from your systems. The model never sees the database; it sees what the lookup returned.
- The arrow on the right is the loop. It is also the cost and the risk: every turn is another model call, and a model that never decides it is done will keep going. That is why step limits exist.
- Reminder from earlier: the thoughts are useful for debugging, but they are generated text, not a faithful record of how the model reached its answer. The actions and observations are the audit trail.
{{% /note %}}

***

<!-- How a tool is described to the model -->
{{< slide class="fs50" >}}

# How the model learns a tool exists

<div class="cols2">
<div>
<div class="card" style="font-size:1.05em"><code>{<br>
&nbsp;&nbsp;"name": "issue_refund",<br>
&nbsp;&nbsp;"description": "Refund a customer's<br>
&nbsp;&nbsp;&nbsp;&nbsp;order. Use only after the order is<br>
&nbsp;&nbsp;&nbsp;&nbsp;verified and placed within 30 days.",<br>
&nbsp;&nbsp;"parameters": {<br>
&nbsp;&nbsp;&nbsp;&nbsp;"order_id": "string",<br>
&nbsp;&nbsp;&nbsp;&nbsp;"amount": "number"<br>
&nbsp;&nbsp;}<br>
}</code></div>
<p class="refs" style="margin-top:0.3em">A tool definition, simplified. It is sent to the model with every request.</p>
</div>
<div>
<div class="card"><span class="hd">Name and parameters</span>What your code will run, and the exact shape of a valid request. Anything else can be rejected before it runs.</div>
<div class="card"><span class="hd">Description</span>Plain English the model reads to decide <em>when</em> to use the tool. It reads like policy, and someone in the business should review it.</div>
<div class="card warn"><span class="hd">But a description is a request</span>&ldquo;Use only within 30 days&rdquo; will be followed most of the time. The 30-day rule still has to be checked in code.</div>
</div>
</div>

{{% note %}}
- This is the whole interface between a model and a tool: a name, a description, and the parameters it takes. Every major model provider uses this same shape.
- The model has never seen your refund system. It learns the tool exists from this definition, which is sent along with every request.
- The description is the interesting part for this room. It is written in plain English, it decides when the model reaches for the tool, and in most organisations it is written by a developer and reviewed by nobody. Treat it as a policy document.
- And then the caveat, the same one as the refund trace: instructions in a description shape behaviour; they do not enforce it. The ceiling and the 30-day window belong in the code that runs the tool.
{{% /note %}}

***

<!-- The tool-call round trip -->
{{< slide class="fs50" >}}

# How the model calls a tool

<svg class="dg" viewBox="0 0 860 372" role="img" aria-label="A sequence diagram. The user asks the agent runtime for a refund. The runtime sends the message and tool definitions to the model. The model replies with a structured tool-call request. The runtime checks it against permissions and limits, executes it against the payments system, returns the result to the model, and passes the model's answer to the user">
<defs>
<marker id="tc-b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#003478"/></marker>
<marker id="tc-r" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#CC0000"/></marker>
</defs>
<rect class="bx-g" x="20" y="0" width="140" height="40" rx="6"/><text class="t-c t-b t-m" x="90" y="26">User</text>
<rect class="bx-b" x="250" y="0" width="160" height="40" rx="6"/><text class="t-c t-b t-m t-w" x="330" y="26">Your code</text>
<rect class="bx-rf" x="510" y="0" width="160" height="40" rx="6"/><text class="t-c t-b t-m t-w" x="590" y="26">LLM</text>
<rect class="bx" x="720" y="0" width="140" height="40" rx="6"/><text class="t-c t-b t-m" x="790" y="26">Payments</text>
<path d="M90 40V368M330 40V368M590 40V368M790 40V368" stroke="#bbb" stroke-width="1.5" stroke-dasharray="4 5"/>
<text class="t-c t-s" x="210" y="70">1 &middot; &#8220;Refund order 1182&#8221;</text><path class="ln" d="M90 78H328" marker-end="url(#tc-b)"/>
<text class="t-c t-s" x="460" y="106">2 &middot; message + tool definitions</text><path class="ln" d="M330 114H588" marker-end="url(#tc-b)"/>
<text class="t-c t-s" x="460" y="142" style="fill:#CC0000">3 &middot; tool call: issue_refund(1182, 45.00)</text><path class="ln" d="M590 150H332" style="stroke:#CC0000" marker-end="url(#tc-r)"/>
<rect class="bx-r" x="232" y="166" width="196" height="54" rx="6"/><text class="t-c t-b t-m" x="330" y="189">4 &middot; Check</text><text class="t-c t-s" x="330" y="209">allowed? under limit? log it</text>
<text class="t-c t-s" x="560" y="238">5 &middot; execute</text><path class="ln" d="M330 246H788" marker-end="url(#tc-b)"/>
<text class="t-c t-s" x="560" y="274">6 &middot; result: refunded</text><path class="ln" d="M790 282H332" marker-end="url(#tc-b)"/>
<text class="t-c t-s" x="460" y="310">7 &middot; result, as text</text><path class="ln" d="M330 318H588" marker-end="url(#tc-b)"/>
<text class="t-c t-s" x="210" y="346">8 &middot; &#8220;Your refund is on its way&#8221;</text><path class="ln" d="M330 354H92" marker-end="url(#tc-b)"/>
</svg>

<p class="refs" style="font-size:0.8em">The model only ever <strong>writes a request</strong> (step 3). Your code decides whether it runs (step 4). That gap is where permissions, ceilings and the audit log belong.</p>

{{% note %}}
- The most important fact about tool use, and the most commonly misunderstood: the model does not call anything. It cannot. It writes a structured request, in red at step 3, and stops.
- Your code, the agent runtime, receives that request. Step 4 is the control point. Is this tool allowed for this user? Is the amount under the ceiling? Is the order inside the window? Log it either way.
- Only then does anything touch the payments system. The result comes back to your code, goes to the model as text, and the model writes the reply.
- Map this onto the earlier slides. &ldquo;Every tool is a permission&rdquo; is enforced at step 4. &ldquo;A limit in the prompt is a request; a limit in the wrapper is a control&rdquo; is the difference between the description on the last slide and step 4 on this one.
- Frameworks and MCP automate steps 2 to 7. They do not decide what step 4 checks. That is a business decision.
{{% /note %}}

***

<!-- Orchestrator: generate or decide (LLM vs. Jev) -->
{{< slide class="fs50" >}}

# The orchestrator: LLM or Jev<sup>*</sup>?

<svg class="dg" viewBox="0 0 860 296" role="img" aria-label="Two ways to make a routing decision. A language model generates a sentence token by token, which code must then parse before routing. A decision model such as Jev scores a fixed list of options and returns the choice with a probability, which code can route on directly">
<defs>
<marker id="jv-g" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto"><path d="M0 0L10 5L0 10z" fill="#999"/></marker>
</defs>
<text x="0" y="18" class="t-b t-red">LLM orchestrator: generates text</text>
<rect class="bx-g" x="0" y="34" width="110" height="50" rx="6"/><text class="t-c" x="55" y="65">State</text>
<rect class="bx-rf" x="150" y="34" width="110" height="50" rx="6"/><text class="t-c t-b t-w" x="205" y="65">LLM</text>
<rect class="bx-r" x="300" y="34" width="310" height="50" rx="6"/><text class="t-c t-m" x="455" y="56" style="font-style:italic">&#8220;Next, hand this to the Executor,</text><text class="t-c t-m" x="455" y="75" style="font-style:italic">because the plan is complete&#8230;&#8221;</text>
<rect class="bx" x="650" y="34" width="90" height="50" rx="6"/><text class="t-c" x="695" y="65">Parse</text>
<rect class="bx-g" x="770" y="34" width="90" height="50" rx="6"/><text class="t-c" x="815" y="65">Route</text>
<path class="ln-g" d="M110 59H148" marker-end="url(#jv-g)"/>
<path class="ln-g" d="M260 59H298" marker-end="url(#jv-g)"/>
<path class="ln-g" d="M610 59H648" marker-end="url(#jv-g)"/>
<path class="ln-g" d="M740 59H768" marker-end="url(#jv-g)"/>
<text class="t-c t-s" x="455" y="102">one token at a time</text>
<path d="M0 124H860" stroke="#ddd" stroke-width="1"/>
<text x="0" y="156" class="t-b t-blue">Decision model (Jev): scores your options</text>
<rect class="bx-g" x="0" y="196" width="110" height="60" rx="6"/><text class="t-c" x="55" y="222">State +</text><text class="t-c" x="55" y="244">options</text>
<rect class="bx-b" x="150" y="201" width="110" height="50" rx="6"/><text class="t-c t-b t-w" x="205" y="232">Jev</text>
<rect class="bx" x="300" y="172" width="310" height="108" rx="6"/>
<text class="t-m" x="314" y="196">Planner</text><rect x="430" y="185" width="8" height="13" fill="#9db3d1"/><text class="t-m" x="560" y="196">0.06</text>
<text class="t-m t-b" x="314" y="220">Executor</text><rect x="430" y="209" width="105" height="13" fill="#003478"/><text class="t-m t-b" x="560" y="220">0.81</text>
<text class="t-m" x="314" y="244">Quality check</text><rect x="430" y="233" width="12" height="13" fill="#9db3d1"/><text class="t-m" x="560" y="244">0.09</text>
<text class="t-m" x="314" y="268">Done</text><rect x="430" y="257" width="5" height="13" fill="#9db3d1"/><text class="t-m" x="560" y="268">0.04</text>
<rect class="bx-g" x="770" y="201" width="90" height="50" rx="6"/><text class="t-c" x="815" y="232">Route</text>
<path class="ln-g" d="M110 226H148" marker-end="url(#jv-g)"/>
<path class="ln-g" d="M260 226H298" marker-end="url(#jv-g)"/>
<path class="ln-g" d="M610 226H768" marker-end="url(#jv-g)"/>
<text class="t-c t-s" x="690" y="217">a typed choice</text>
</svg>

<div class="cols3" style="margin-top:0.7em">
<div>
<div class="card warn"><span class="hd">An LLM generates</span>Open-ended text: it can plan, explain and cope with the unexpected. Slower, priced per output token, and its answer has to be parsed.</div>
</div>
<div>
<div class="card"><span class="hd">Jev decides</span>It picks from a list your code supplies and puts a probability on each option. No text to parse, and nothing outside the list can come back.</div>
</div>
<div>
<div class="card"><span class="hd">Still a judgement</span>A scored choice can be the wrong choice. The probability gives your code a threshold: below it, hand the case to a person.</div>
</div>
</div>

<p class="refs">Jev: TypeSafe AI, early access since September 2026. The vendor reports responses in 70&ndash;500 ms and large cost savings on its own workflows; those figures are a type P claim. <a href="https://typesafe.ai/blog/introducing-system-one-models-and-jev">TypeSafe AI, Introducing System One Models &amp; Jev</a><br><sup>*</sup> Named after the <strong>Jevons paradox</strong> of William Stanley Jevons, a British economist (<em>The Coal Question</em>, 1865): when efficiency makes a resource cheaper, total use of it tends to rise, not fall.</p>

{{% note %}}
- Look at what the orchestrator on the last slide actually does: it picks the next agent from a short list. That is a decision with a finite set of answers.
- A language model answers it the only way it can, by predicting text one token at a time. We then write code to read the sentence and work out which agent it meant. We are paying for prose when we wanted a choice.
- Jev is a new kind of model that TypeSafe AI calls a &ldquo;System One&rdquo; model, after fast intuitive thinking. It does not generate text. Your code supplies the options and it returns a score for each. It offers three question types: choose one of a list, rate on a scale, or yes/no with a probability.
- Where this fits: routing, choosing a tool, a risk check before a tool runs, triage of results. Where it does not: writing the plan, drafting the reply, anything open-ended. A realistic design uses both.
- Connect to the refund trace: this moves a red step closer to blue. It is still model judgement, but the output is constrained and comes with a number your code can act on.
- The name is a deliberate signal. Jevons observed that more efficient steam engines raised England's coal consumption, because cheaper energy unlocked new uses. TypeSafe's bet is the same for decisions: make each one cheap enough and firms will automate far more of them. Worth asking the room whether that is good news for their compute budget.
- Be straightforward about maturity. The model was released weeks ago, the speed and cost figures are the vendor's own, and no independent accuracy results exist yet. Cheap routing is worthless if cases go to the wrong place.
{{% /note %}}

***

<!-- MCP, tools and skills -->
{{< slide class="fs50" >}}

# MCP, tools and skills

<svg class="dg" viewBox="0 0 860 246" role="img" aria-label="An agent in the centre. On the left, skills such as a refund procedure are loaded when needed. On the right, MCP servers for the CRM, payments and documents each expose tools the agent can call">
<text x="0" y="18" class="t-b t-blue">Skills: know-how</text>
<text x="630" y="18" class="t-b t-blue">MCP servers: connections</text>
<rect class="bx" x="0" y="32" width="230" height="54" rx="6"/><text class="t-b t-m" x="14" y="55">Refund procedure</text><text class="t-s" x="14" y="75">steps, limits, who approves</text>
<rect class="bx" x="0" y="110" width="230" height="54" rx="6"/><text class="t-b t-m" x="14" y="133">Month-end close</text><text class="t-s" x="14" y="153">checklist and templates</text>
<rect class="bx" x="0" y="188" width="230" height="54" rx="6"/><text class="t-b t-m" x="14" y="211">Brand voice</text><text class="t-s" x="14" y="231">how we write to customers</text>
<path class="ln ln-d" d="M230 59L340 130"/>
<path class="ln ln-d" d="M230 137H340"/>
<path class="ln ln-d" d="M230 215L340 144"/>
<text class="t-c t-s" x="285" y="128">loaded</text>
<rect class="bx-b" x="340" y="107" width="180" height="60" rx="8"/><text class="t-c t-b t-w" x="430" y="144">Agent</text>
<path class="ln" d="M520 130L630 59"/>
<path class="ln" d="M520 137H630"/>
<path class="ln" d="M520 144L630 215"/>
<text class="t-c t-s" x="575" y="128">MCP</text>
<rect class="bx" x="630" y="32" width="230" height="54" rx="6"/><text class="t-b t-m" x="644" y="55">CRM</text><text class="t-s" x="644" y="75">lookup_order, update_record</text>
<rect class="bx-r" x="630" y="110" width="230" height="54" rx="6"/><text class="t-b t-m" x="644" y="133">Payments</text><text class="t-s" x="644" y="153">issue_refund</text>
<rect class="bx" x="630" y="188" width="230" height="54" rx="6"/><text class="t-b t-m" x="644" y="211">Documents</text><text class="t-s" x="644" y="231">search_docs</text>
</svg>

<div class="cols3" style="margin-top:0.8em">
<div>
<div class="card"><span class="hd">Tool: what it can do</span>One callable function, such as <code>issue_refund</code>. Each one is a permission.</div>
<p><strong>Ask:</strong> what may it do, and up to what limit?</p>
</div>
<div>
<div class="card"><span class="hd">MCP: how tools are plugged in</span>The Model Context Protocol is an open standard connector. A system publishes its tools once, as an MCP server, and any compatible agent can use them.</div>
<p><strong>Ask:</strong> which servers is it connected to, and who runs them?</p>
</div>
<div>
<div class="card"><span class="hd">Skill: how the work is done here</span>A packaged procedure, written instructions plus any scripts, that the agent loads when a task calls for it.</div>
<p><strong>Ask:</strong> whose procedure is it, and who keeps it current?</p>
</div>
</div>

{{% note %}}
- Three words you will hear in every agent proposal, and they answer three different questions: what can it do, how is it connected, and how does it know our way of doing things.
- **Tools** we have covered: one function, one permission.
- **MCP**, the Model Context Protocol, was introduced by Anthropic in late 2024 and is now supported across the major vendors. Think of it as a standard plug. Before it, every agent needed a custom connector to every system; now a system publishes one MCP server and any compatible agent can use it.
- The governance point about MCP: connecting a server grants every tool that server exposes. Adding a server is not one permission, it is a bundle. Review the tool list inside it, and be careful with servers run by third parties.
- **Skills** are the newer idea. A skill is a folder of instructions, and sometimes scripts, describing how to do a task: the refund procedure, the month-end checklist, the house style. The agent reads only a short description of each and loads the full skill when the task calls for it.
- The useful way to hold the three together: tools and MCP give the agent hands; skills give it your firm's operating procedures. Most of the difference between a generic agent and one that works in your business is in the skills, and those are documents your own people can write and maintain.
- A skill is not a control. It tells the agent what to do; it does not stop it doing something else. Limits still belong in the tool.
{{% /note %}}

***

<!-- Primer 8 — When not to go multi-agent -->
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
<p>The single agent is unreliable &mdash; more agents multiply an unreliable step rather than fixing it.</p>
</div>
</div>

<p class="refs">Most &ldquo;agentic&rdquo; proposals are workflows with one uncertain step. Build the deterministic part deterministically.</p>

{{% note %}}
- Keep this slide in mind for the rest of the session. Each solution lists four or five agent roles; that is an illustration of the kinds of work involved, not a requirement to deploy four models.
- Each additional agent adds model calls, latency, and a new place for a handoff to go wrong.
- Debuggability is the hidden cost: with one agent you ask why it did that. With six, you first have to work out which one did it.
{{% /note %}}

***

<!-- Primer 9 — Four patterns overview -->
{{< slide class="fs55" >}}

# Four design patterns

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="Four agentic design patterns: reflection, tool use, planning, and multi-agent">
<defs>
<marker id="fp-b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="5" markerHeight="5" orient="auto-start-reverse"><path d="M0 0L10 5L0 10z" fill="#003478"/></marker>
</defs>
<g>
<rect class="bx-p" x="0" y="0" width="420" height="200" rx="8"/>
<text class="t-b t-blue" x="16" y="32">Reflection</text>
<rect class="bx" x="50" y="70" width="120" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="110" y="97">Generate</text>
<rect class="bx" x="250" y="70" width="120" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="310" y="97">Critique</text>
<path class="ln" d="M170 83H248" marker-end="url(#fp-b)"/><text class="t-c t-s" x="210" y="74">draft</text>
<path class="ln" d="M250 101H172" marker-end="url(#fp-b)"/><text class="t-c t-s" x="210" y="122">feedback</text>
<text class="t-s" x="16" y="182">Generate, critique, revise.</text>
</g>
<g transform="translate(440 0)">
<rect class="bx-p" x="0" y="0" width="420" height="200" rx="8"/>
<text class="t-b t-blue" x="16" y="32">Tool use</text>
<rect class="bx" x="40" y="76" width="110" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="95" y="103">Model</text>
<rect class="bx" x="250" y="48" width="130" height="30" rx="6" style="fill:#fff"/><text class="t-c t-m" x="315" y="68">Search</text>
<rect class="bx" x="250" y="83" width="130" height="30" rx="6" style="fill:#fff"/><text class="t-c t-m" x="315" y="103">APIs</text>
<rect class="bx" x="250" y="118" width="130" height="30" rx="6" style="fill:#fff"/><text class="t-c t-m" x="315" y="138">Code</text>
<path class="ln" d="M152 90L248 64" marker-start="url(#fp-b)" marker-end="url(#fp-b)"/>
<path class="ln" d="M152 98H248" marker-start="url(#fp-b)" marker-end="url(#fp-b)"/>
<path class="ln" d="M152 106L248 132" marker-start="url(#fp-b)" marker-end="url(#fp-b)"/>
<text class="t-s" x="16" y="182">Call out to systems; use the results.</text>
</g>
<g transform="translate(0 220)">
<rect class="bx-p" x="0" y="0" width="420" height="200" rx="8"/>
<text class="t-b t-blue" x="16" y="32">Planning</text>
<rect class="bx" x="20" y="60" width="100" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="70" y="87">Plan</text>
<rect class="bx" x="160" y="60" width="100" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="210" y="87">Execute</text>
<rect class="bx" x="300" y="60" width="100" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="350" y="87">Re-plan</text>
<path class="ln" d="M120 82H158" marker-end="url(#fp-b)"/>
<path class="ln" d="M260 82H298" marker-end="url(#fp-b)"/>
<path class="ln" d="M350 104V134H210V107" marker-end="url(#fp-b)"/><text class="t-c t-s" x="280" y="152">iterate</text>
<text class="t-s" x="16" y="182">Lay out subtasks before executing.</text>
</g>
<g transform="translate(440 220)">
<rect class="bx-p" x="0" y="0" width="420" height="200" rx="8"/>
<text class="t-b t-blue" x="16" y="32">Multi-agent</text>
<rect class="bx" x="20" y="60" width="100" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="70" y="87">Planner</text>
<rect class="bx" x="160" y="60" width="100" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="210" y="87">Executor</text>
<rect class="bx" x="300" y="60" width="100" height="44" rx="6" style="fill:#fff"/><text class="t-c t-m" x="350" y="87">Reviewer</text>
<path class="ln" d="M122 82H158" marker-start="url(#fp-b)" marker-end="url(#fp-b)"/>
<path class="ln" d="M262 82H298" marker-start="url(#fp-b)" marker-end="url(#fp-b)"/>
<path class="ln" d="M70 107Q210 170 350 107" marker-start="url(#fp-b)" marker-end="url(#fp-b)"/>
<text class="t-s" x="16" y="182">Specialised roles working together.</text>
</g>
</svg>

{{% note %}}
- The four design patterns your engineers will name. **Reflection** — generate, critique, revise. **Tool use** — call out to systems and use the results. **Planning** — lay out subtasks before executing. **Multi-agent** — specialised roles working together.
- They are composable, not alternatives. A serious system uses several.
- The cost structure matters for a budget conversation: each pattern buys quality with extra model calls and latency. There is no free reliability.
{{% /note %}}

***

<!-- Primer 10 — Autonomy levels -->
{{< slide class="fs60" >}}

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
- This is the slide to photograph. Every solution in the second half carries a tool list with one of these four levels against each tool.
- Autonomy is set per action, not per system. Most disagreements about &ldquo;how autonomous should this be&rdquo; dissolve once you break the system into individual tools.
- Level 2 has a specific failure mode — **rubber-stamping**. A reviewer approving 200 items an hour is a level 3 system with a person to blame. If you rely on approval, measure the rejection rate.
{{% /note %}}

***

<!-- ===== SECTION 2 — HOW TO READ ===== -->
{{< slide background-color="#003478" class="section" >}}

# Agentic Business Solutions

<p>What was chosen, and how to read each one</p>

{{% note %}}
Part two: the frame. Five slides, then we use it six times.
{{% /note %}}

***

{{< slide class="fs55" >}}

# Why these six

<div class="card"><span class="hd">Common patterns, not a ranked top six</span>These are solution patterns that are widely deployed or frequently proposed. Nothing here says they are the six most valuable, or the six most adopted.</div>
<div class="card"><span class="hd">Where scaling is reported</span>McKinsey's 2026 survey reports agent scaling most often in <strong>IT</strong>, <strong>knowledge management</strong> and <strong>software engineering</strong>, with <strong>marketing and sales</strong> and <strong>supply chain</strong> prominent in particular industries.</div>
<div class="card"><span class="hd">Plus one established application</span><strong>Customer support</strong> is added as a long-standing use of conversational systems that is now being extended from answering to acting.</div>

<p class="refs">McKinsey, <em>The state of AI in 2026: On the road to ROI</em> (2026). Used as general context for where adoption is reported, not as a ranking.</p>

{{% note %}}
- Be explicit about the selection. A list of six in a slide deck reads like a league table, and this is not one.
- The survey finding is about where organisations *report* scaling. Self-reported adoption is a signal of where attention and budget are going; it is not evidence of return.
{{% /note %}}

***

{{< slide class="fs55" >}}

# What makes a solution &ldquo;agentic&rdquo;

<div class="cols2">
<div>
<p class="sub">Answers</p>
<div class="card"><span class="hd">A prompt and a response</span>Explains the refund policy. Summarises the incident. Suggests a supplier.</div>
<p>The human still does the work.</p>
</div>
<div>
<p class="sub">Acts</p>
<div class="card warn"><span class="hd">Plans and executes multistep work</span>Uses tools and organisational data to issue the refund, run the runbook step, or raise the purchase order.</div>
<p>The human supervises, approves, or handles exceptions.</p>
</div>
</div>

<p class="refs">A test for any pitch: name the tool the system calls that changes something outside the conversation. If there is none, it is a chatbot.</p>

{{% note %}}
- The definition from the first half, restated for a buyer: an agentic solution plans and executes multistep work using tools and organisational data, rather than merely answering a prompt.
- The test in the footer is the practical one. Much of what is sold as agentic today is the left-hand column with a new label.
{{% /note %}}

***

{{< slide class="fs55" >}}

# The six on one page

<table class="plain">
<tr><th>Group</th><th>Solution</th><th>What it does</th></tr>
<tr><td class="lv" rowspan="2">Knowledge work</td><td><strong>Enterprise knowledge and research</strong></td><td>Searches internal material, synthesises evidence, drafts briefings</td></tr>
<tr><td><strong>Software engineering and modernisation</strong></td><td>Turns requirements into code changes, tests and documentation</td></tr>
<tr><td class="lv" rowspan="2">Operations</td><td><strong>IT service and incident operations</strong></td><td>Handles help requests, diagnoses alerts, runs runbook steps</td></tr>
<tr><td><strong>Supply chain and procurement</strong></td><td>Monitors inventory and suppliers, recommends and raises orders</td></tr>
<tr><td class="lv" rowspan="2">Revenue and customer</td><td><strong>Customer-service resolution</strong></td><td>Triages requests, performs permitted fixes, escalates exceptions</td></tr>
<tr><td><strong>Sales and marketing execution</strong></td><td>Qualifies leads, drafts outreach, updates CRM, tests campaigns</td></tr>
</table>

<p class="refs">Ordered by where the action lands: inside the firm's knowledge, inside its systems, then in front of customers and suppliers.</p>

{{% note %}}
- Three pairs. The grouping is ours, chosen so the stakes rise through the session.
- Knowledge work is mostly read-only or sandboxed, with a human gate before anything ships. Operations writes to internal systems and commits spend. Revenue and customer speaks to outsiders in the company's voice and moves money.
- Ask the room which of the six is already in their budget or on a vendor's slide.
{{% /note %}}

***

{{< slide class="fs55" >}}

# Four slides per solution

<div class="cols2">
<div>
<div class="card"><span class="hd">1 &middot; The job</span>What it does, and the workflow it replaces. If you cannot describe today's workflow, you cannot measure the change.</div>
<div class="card"><span class="hd">2 &middot; The team</span>The agent roles, the resources they need, and the tool list with an autonomy level against each tool.</div>
</div>
<div>
<div class="card"><span class="hd">3 &middot; The value hypothesis</span>The expected benefit, the metric that would show it, and the baseline you need before you start.</div>
<div class="card warn"><span class="hd">4 &middot; The evidence</span>The vendor reference and the best independent study, what type each is, and what it does not prove.</div>
</div>
</div>

<p class="refs">The same four questions work on any proposal that reaches your desk.</p>

{{% note %}}
- This template is the reusable part of the session. The six solutions will date; the four questions will not.
- Slide 2 of each solution is illustrative. The agent roles come from the source material; the tool lists and autonomy levels are a reasonable starting point for discussion, not a description of any vendor's product.
{{% /note %}}

***

{{< slide class="fs55" >}}

# Reading the evidence

<table class="plain">
<tr><th>Code</th><th>Evidence type</th><th>What it shows</th><th>What it does not show</th></tr>
<tr><td class="lv">P</td><td>Product documentation, announcement or advertisement</td><td>The vendor says the product can do this</td><td>That anyone has deployed it, or that it works at scale</td></tr>
<tr><td class="lv">C</td><td>Vendor-published customer story</td><td>A named organisation uses the product</td><td>Independently verified results; what did not work</td></tr>
<tr><td class="lv">A</td><td>An AI-assistance story plus separate agent documentation</td><td>The industry uses assistive AI, and an agent product exists</td><td>That the named customer runs the autonomous agent</td></tr>
<tr><td class="lv">I</td><td>Research with a stated method: experiment, benchmark, or tribunal record</td><td>A measured effect, or a documented failure</td><td>That it transfers to your firm; most measure assistance, not autonomy</td></tr>
</table>

<div class="card warn" style="margin-top:0.8em"><span class="hd">Three different claims</span><strong>Capability</strong> is not <strong>deployment</strong>, and deployment is not <strong>return</strong>. Most public material on agentic AI is the first kind.</div>

{{% note %}}
- Every reference in this deck is labelled P, C, A or I. The first three are published by vendors. The fourth is research with a method you can inspect.
- An I is not automatically stronger for your decision. Most of the rigorous studies measure a person working with an AI assistant, not an autonomous agent, and some are written by researchers at the firm being studied.
- The &ldquo;A&rdquo; category is the subtle one, and we will see a real example of it in the software-engineering section.
{{% /note %}}

***

<!-- ===== SECTION 3 — KNOWLEDGE WORK ===== -->
{{< slide background-color="#003478" class="section" >}}

# Knowledge Work

<p>Enterprise knowledge and research &middot; Software engineering</p>

{{% note %}}
Part three: the two solutions where the action stays closest to home. Mostly read-only or sandboxed, with a human gate before anything ships.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Enterprise knowledge and research &middot; 1 of 4</p>

# The job

<div class="cols2">
<div>
<p class="sub">What it does</p>
<div class="card">Searches internal material across systems.</div>
<div class="card">Synthesises the evidence it finds and drafts a briefing.</div>
<div class="card">Routes questions it cannot resolve to a subject-matter expert.</div>
</div>
<div>
<p class="sub">What it replaces</p>
<div class="card warn">An employee searching the intranet, three shared drives and a ticketing system, then asking a colleague who has been there longest.</div>
<p>The work is real and almost never measured, which makes the baseline the hard part.</p>
</div>
</div>

{{% note %}}
- This is the RAG project from earlier sessions, promoted to an agent. The difference is the loop: it plans a multi-step search, decides whether what it found is enough, and looks again if not.
- The third card is the agentic step that matters most in practice — knowing when to stop and hand the question to a person.
{{% /note %}}

***

{{< slide class="fs50" >}}

<p class="kicker">Enterprise knowledge and research &middot; 2 of 4</p>

# The team

<div class="cols2">
<div>
<p class="sub">Agents</p>
<div class="card"><span class="hd">Query planner</span>Breaks the question into searches.</div>
<div class="card"><span class="hd">Retrieval / research</span>Runs the searches across sources.</div>
<div class="card"><span class="hd">Synthesis</span>Drafts the answer or briefing.</div>
<div class="card"><span class="hd">Citation / verification</span>Checks each claim against its source.</div>
<p class="sub">Resources</p>
<p>Permission-aware document index or graph, search and RAG, intranet and file connectors, access controls, expert review.</p>
</div>
<div>
<p class="sub">Tools and the dial</p>
<table class="plain">
<tr><th>Tool</th><th>Level</th></tr>
<tr><td><code>search_index</code></td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>read_document</code></td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>draft_briefing</code></td><td class="lv">1 &middot; Advise</td></tr>
<tr><td><code>route_to_expert</code></td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>publish_to_wiki</code></td><td class="lv">Not granted</td></tr>
</table>
<div class="card warn" style="margin-top:0.7em"><span class="hd">The control that matters</span>Permission-aware retrieval. The agent must see only what the person asking is allowed to see.</div>
</div>
</div>

{{% note %}}
- The tool list is almost entirely read-only. That is why this is the usual first agentic project: the worst single call is a wrong answer, not a changed record.
- The risk is in the reading. An index that ignores document permissions turns a helpful assistant into the fastest way to find the salary spreadsheet.
- Tool names and levels here are illustrative.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Enterprise knowledge and research &middot; 3 of 4</p>

# The value hypothesis

<div class="card"><span class="hd">Expected value</span>Less employee search time, faster decisions, and reuse of institutional knowledge.</div>
<div class="card"><span class="hd">Measure</span><strong>Answer accuracy</strong> against a set of questions with known answers, and <strong>time saved</strong> per question.</div>
<div class="card warn"><span class="hd">Baseline first</span>How long does a typical question take today, and how often is the answer wrong or out of date? Without those two numbers, &ldquo;time saved&rdquo; is a survey of how people feel.</div>

<p class="refs">The evaluation set from the RAG sessions is the measurement instrument. It carries over unchanged.</p>

{{% note %}}
- Time saved is the metric every vendor quotes and the hardest to verify, because nobody timed the search before.
- Accuracy is the one you can actually measure, using the evaluation approach from the RAG sessions.
- A fast wrong answer is worse than a slow search. Report the two metrics together.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Enterprise knowledge and research &middot; 4 of 4</p>

# The evidence

<div class="card"><span class="hd">McCarthy Holdings / Glean &mdash; construction &middot; type C</span>A vendor-published customer story: search across company knowledge, and agents for policy, project and operational questions.</div>
<div class="card"><span class="hd">Dell'Acqua et al., <em>Organization Science</em> (2026) &mdash; consulting &middot; type I</span>A pre-registered experiment with 758 BCG consultants using GPT-4 as an assistant. On tasks within the model's capability they completed 12.2% more tasks at higher rated quality; on a task chosen to lie outside it, they did worse than the control group.</div>
<div class="card warn"><span class="hd">What the evidence does not prove</span>Neither source tests an agent searching a firm's own documents. The customer story is the vendor's claim; the experiment gave consultants a general-purpose assistant. Together they suggest a real benefit with a catch: on work outside the model's reach, people relying on it did worse.</div>
<div class="card"><span class="hd">Ask</span>How was accuracy measured, on which questions, and by whom? What share of questions still went to a person?</div>

<p class="refs"><a href="https://www.glean.com/resources/customer-stories/mccarthy-holdings-inc">Glean, McCarthy Holdings, Inc. customer story</a> &middot; <a href="https://pubsonline.informs.org/doi/full/10.1287/orsc.2025.21838">Dell'Acqua et al., Navigating the Jagged Technological Frontier</a></p>

{{% note %}}
- This is the only vendor reference in today's deck that names a customer actually using an agentic product. Note that, and note that it is still published by the vendor.
- The independent study is about knowledge work with an assistant, not an agent searching company documents. Its lesson transfers anyway: the same tool helps on some tasks and hurts on others that look similar, and users cannot easily tell which is which.
- Construction is an interesting industry for it: project knowledge is scattered across sites, contracts and people, which is exactly where search across silos pays.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Software engineering and modernisation &middot; 1 of 4</p>

# The job

<div class="cols2">
<div>
<p class="sub">What it does</p>
<div class="card">Turns a requirement or an issue into a code change.</div>
<div class="card">Writes tests and documentation, and reviews changes.</div>
<div class="card">Assists with legacy migration, under developer supervision.</div>
</div>
<div>
<p class="sub">What it replaces</p>
<div class="card warn">A developer picking a ticket from the backlog, writing the change and its tests, and waiting for a colleague to review it.</div>
<p>Of the six, this is the workflow with the best existing instrumentation.</p>
</div>
</div>

{{% note %}}
- Software engineering is where agents are most mature, for a structural reason: the work already lives in version control, has automated tests, and has a review gate. The guardrails existed before the agent did.
- &ldquo;Under developer supervision&rdquo; is doing real work in that third card. Legacy migration is where the value is large and the tests are thinnest.
{{% /note %}}

***

{{< slide class="fs50" >}}

<p class="kicker">Software engineering and modernisation &middot; 2 of 4</p>

# The team

<div class="cols2">
<div>
<p class="sub">Agents</p>
<div class="card"><span class="hd">Planner</span>Breaks the issue into changes.</div>
<div class="card"><span class="hd">Coding</span>Writes the change.</div>
<div class="card"><span class="hd">Test</span>Writes and runs tests.</div>
<div class="card"><span class="hd">Review / security</span>Checks the change before a human sees it.</div>
<p class="sub">Resources</p>
<p>Git repositories, issue tracker, CI/CD, test runners, sandbox, code-search index, developer approvals.</p>
</div>
<div>
<p class="sub">Tools and the dial</p>
<table class="plain">
<tr><th>Tool</th><th>Level</th></tr>
<tr><td><code>read_repository</code></td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>run_tests</code> (sandbox)</td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>open_pull_request</code></td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>merge_to_main</code></td><td class="lv">2 &middot; Approval</td></tr>
<tr><td><code>deploy_to_production</code></td><td class="lv">Not granted</td></tr>
</table>
<div class="card warn" style="margin-top:0.7em"><span class="hd">The control that matters</span>The pull request. The agent proposes; a developer approves the merge.</div>
</div>
</div>

{{% note %}}
- An agent that runs code is arbitrary code execution inside your environment. The sandbox — no production credentials, restricted network — is not optional.
- The pull request is a ready-made level 2 gate. It is also where rubber-stamping shows up: a reviewer facing ten agent-written changes a day reviews them differently from one written by a colleague.
- Tool names and levels here are illustrative.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Software engineering and modernisation &middot; 3 of 4</p>

# The value hypothesis

<div class="card"><span class="hd">Expected value</span>Shorter delivery cycles, reduced maintenance effort, and potentially more freedom in build-versus-buy decisions.</div>
<div class="card"><span class="hd">Measure</span><strong>Accepted changes</strong>, <strong>defects</strong>, and <strong>lead time</strong> from request to release.</div>
<div class="card warn"><span class="hd">Baseline first</span>All three are already in your engineering tools. Take the last two quarters before the pilot starts.</div>

<p class="refs">Lines of code written is not on this list. It measures output, not delivery.</p>

{{% note %}}
- Accepted changes is the honest metric: how much of what the agent proposed did a developer actually merge?
- Watch defects alongside lead time. Faster delivery that raises the defect rate has moved the cost downstream, not removed it.
- The build-versus-buy point is strategic: if custom software gets cheaper to build and maintain, some packaged-software decisions change. Treat it as a hypothesis.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Software engineering and modernisation &middot; 4 of 4</p>

# The evidence

<div class="cols2">
<div>
<div class="card"><span class="hd">Saxo Bank / Microsoft &mdash; banking</span>A vendor-published customer story about AI-<em>assisted</em> coding with GitHub Copilot.</div>
</div>
<div>
<div class="card"><span class="hd">GitHub Copilot cloud agent</span>Product documentation for an agent that takes an issue and prepares a pull request.</div>
</div>
</div>

<div class="cols2">
<div>
<div class="card"><span class="hd">Cui et al., <em>Management Science</em> &middot; type I</span>Three randomised trials at Microsoft, Accenture and a Fortune 100 firm, 4,867 developers: 26% more completed tasks with an AI coding assistant, with larger gains for less experienced developers.</div>
</div>
<div>
<div class="card"><span class="hd">METR (2025) &middot; type I</span>A randomised trial with 16 experienced open-source developers on 246 tasks in their own projects: allowing AI tools made them 19% slower, while they believed they had been 20% faster.</div>
</div>
</div>

<div class="card warn"><span class="hd">What the evidence does not prove</span>Do not join the dots: no source shows Saxo Bank, or any bank, running the autonomous agent. The trials measure developers with an assistant, and they disagree: 26% more tasks across large firms, 19% slower for experts in code they know well.</div>

<p class="refs"><a href="https://www.microsoft.com/en/customers/story/24389-saxo-bank-github-copilot">Microsoft, GitHub Copilot accelerates coding at Saxo Bank</a> (2025) &middot; <a href="https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent">GitHub Docs, About GitHub Copilot cloud agent</a> &middot; <a href="https://pubsonline.informs.org/doi/10.1287/mnsc.2025.00535">Cui et al., The Effects of Generative AI on High-Skilled Work</a> &middot; <a href="https://arxiv.org/abs/2507.09089">Becker et al. (METR), Measuring the Impact of Early-2025 AI</a></p>

{{% note %}}
- This is the evidence-literacy slide of the session. Two true statements, placed side by side, invite a third that neither supports.
- It is a common shape in vendor decks: a recognisable logo next to a capability the logo's owner may not be using.
- The question to ask: is the customer using the feature you are being sold, or an earlier one?
- The two independent studies point in opposite directions, and both are sound. The large trials measured tasks completed by developers across a company; the small one measured time taken by experts in codebases they knew deeply. Who the developer is and what the task is matter more than the tool.
- The METR result has a second lesson: the developers' own estimate of the benefit was wrong in sign. Self-reported time savings are not evidence.
{{% /note %}}

***

<!-- ===== SECTION 4 — OPERATIONS ===== -->
{{< slide background-color="#003478" class="section" >}}

# Operations

<p>IT service and incident operations &middot; Supply chain and procurement</p>

{{% note %}}
Part four: the agent now writes to internal systems and, in procurement, commits spend.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">IT service and incident operations &middot; 1 of 4</p>

# The job

<div class="cols2">
<div>
<p class="sub">What it does</p>
<div class="card">Handles employee help requests.</div>
<div class="card">Diagnoses alerts from logs, metrics and traces.</div>
<div class="card">Proposes or executes runbook steps, and escalates risky incidents.</div>
</div>
<div>
<p class="sub">What it replaces</p>
<div class="card warn">A service-desk queue of repetitive tickets, and an on-call engineer woken to follow a documented procedure.</div>
<p>The runbook already exists. The agent's job is to follow it, not to invent it.</p>
</div>
</div>

{{% note %}}
- The phrase to notice is &ldquo;proposes or executes.&rdquo; That &ldquo;or&rdquo; is the autonomy decision, and it should be made per runbook step.
- IT is where scaling is most often reported, and the reason is the same as for software engineering: the procedures are written down and the systems have APIs.
{{% /note %}}

***

{{< slide class="fs50" >}}

<p class="kicker">IT service and incident operations &middot; 2 of 4</p>

# The team

<div class="cols2">
<div>
<p class="sub">Agents</p>
<div class="card"><span class="hd">Triage</span>Classifies and prioritises the request or alert.</div>
<div class="card"><span class="hd">Diagnostic</span>Reads logs, metrics and traces.</div>
<div class="card"><span class="hd">Runbook executor</span>Runs approved steps.</div>
<div class="card"><span class="hd">Communications / escalation</span>Keeps people informed; pages on-call.</div>
<p class="sub">Resources</p>
<p>Service desk, logs / metrics / traces, CMDB, IAM, approved scripts and infrastructure APIs, on-call staff.</p>
</div>
<div>
<p class="sub">Tools and the dial</p>
<table class="plain">
<tr><th>Tool</th><th>Level</th></tr>
<tr><td><code>read_logs_and_metrics</code></td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>unlock_account</code></td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>restart_service</code> (production)</td><td class="lv">2 &middot; Approval</td></tr>
<tr><td><code>page_on_call</code></td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>change_access_rights</code></td><td class="lv">Not granted</td></tr>
</table>
<div class="card warn" style="margin-top:0.7em"><span class="hd">The control that matters</span>An approved list of scripts. The agent picks from the runbook; it does not write new commands.</div>
</div>
</div>

{{% note %}}
- This agent holds infrastructure credentials. Least privilege is the whole game: read widely, act narrowly.
- &ldquo;Approved scripts&rdquo; is the green-box principle from the refund trace. The model decides *which* step; the step itself is deterministic.
- An agent that can change access rights can change its own. That one stays off the list.
- Tool names and levels here are illustrative.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">IT service and incident operations &middot; 3 of 4</p>

# The value hypothesis

<div class="card"><span class="hd">Expected value</span>Lower mean time to resolve incidents, fewer repetitive tickets, and less downtime.</div>
<div class="card"><span class="hd">Measure</span><strong>Resolution time</strong>, and the <strong>safe automation rate</strong> &mdash; the share of automated actions that needed no correction.</div>
<div class="card warn"><span class="hd">Baseline first</span>Resolution time by ticket category, from the service desk you already run. Automation helps the repetitive categories and may do nothing for the rest.</div>

<p class="refs">The word &ldquo;safe&rdquo; matters. An automation rate that counts actions later reversed by a human is measuring activity.</p>

{{% note %}}
- Mean time to resolve is a well-established operations metric, which makes this one of the easier business cases to test.
- The safe automation rate is the counterweight. Ask how many agent actions were rolled back, and how long that took.
- An agent that causes one outage can erase a year of saved tickets. The downside is not symmetric.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">IT service and incident operations &middot; 4 of 4</p>

# The evidence

<div class="card"><span class="hd">ServiceNow network-incident workflow &mdash; telecommunications &middot; type P</span>Product documentation for an agentic workflow that analyses and coordinates telecommunications network incidents.</div>
<div class="card"><span class="hd">Roy et al., FSE 2024 &mdash; cloud services &middot; type I</span>Microsoft researchers tested a tool-using agent on root-cause analysis of real production incidents at Microsoft. It performed competitively with strong baselines and with higher factual accuracy. The study covers diagnosis, not executing a fix.</div>
<div class="card warn"><span class="hd">What the evidence does not prove</span>Neither shows the risky step. The product page has no customer and no result; the study is Microsoft reporting on its own incidents, and it stops at diagnosis. Nothing here shows an agent safely executing a runbook in production.</div>
<div class="card"><span class="hd">Ask</span>Which steps does the workflow execute, and which does it only recommend? Who has it running in production?</div>

<p class="refs"><a href="https://www.servicenow.com/docs/r/zurich/telecom-media-technology/now-assist-for-telecom-media-and-technology/network-incident-analysis-usecase.html">ServiceNow, Analyze network incidents agentic workflow</a> (2025) &middot; <a href="https://arxiv.org/abs/2403.04123">Roy et al., Exploring LLM-based Agents for Root Cause Analysis</a></p>

{{% note %}}
- Product documentation is more useful than a press release for one thing: it tells you what the workflow actually does, step by step.
- It is silent on whether anyone uses it. Both of those are worth knowing.
- The research paper is peer-reviewed and uses real incidents, but it is written by the firm's own researchers and it stops at diagnosis. The step that carries the risk, running the runbook, is the one with no published evidence.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Supply chain and procurement &middot; 1 of 4</p>

# The job

<div class="cols2">
<div>
<p class="sub">What it does</p>
<div class="card">Monitors inventory and supplier signals, and forecasts exceptions.</div>
<div class="card">Recommends replenishment or sourcing actions.</div>
<div class="card">Coordinates approvals and purchase orders.</div>
</div>
<div>
<p class="sub">What it replaces</p>
<div class="card warn">A planner watching exception reports, a buyer chasing supplier updates by email, and a purchase order waiting in an approval queue.</div>
<p>Much of the work is coordination between people and systems, not analysis.</p>
</div>
</div>

{{% note %}}
- This is the first solution in the deck where the agent commits the firm's money to an outside party.
- Notice how much of the replaced work is coordination — chasing, routing, waiting. That is where near-term value from agents tends to sit.
{{% /note %}}

***

{{< slide class="fs50" >}}

<p class="kicker">Supply chain and procurement &middot; 2 of 4</p>

# The team

<div class="cols2">
<div>
<p class="sub">Agents</p>
<div class="card"><span class="hd">Demand / inventory monitor</span>Watches stock and forecasts.</div>
<div class="card"><span class="hd">Supplier-risk researcher</span>Tracks supplier signals.</div>
<div class="card"><span class="hd">Sourcing optimiser</span>Recommends what to buy, and from whom.</div>
<div class="card"><span class="hd">Purchase-order executor</span>Raises and routes orders.</div>
<p class="sub">Resources</p>
<p>ERP, inventory and supplier records, contracts, demand forecasts, purchasing APIs, spending limits, buyer approval.</p>
</div>
<div>
<p class="sub">Tools and the dial</p>
<table class="plain">
<tr><th>Tool</th><th>Level</th></tr>
<tr><td><code>read_inventory</code></td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>recommend_replenishment</code></td><td class="lv">1 &middot; Advise</td></tr>
<tr><td><code>create_po</code> (contracted supplier, under limit)</td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>create_po</code> (above limit, or new supplier)</td><td class="lv">2 &middot; Approval</td></tr>
<tr><td><code>edit_supplier_master_data</code></td><td class="lv">Not granted</td></tr>
</table>
<div class="card warn" style="margin-top:0.7em"><span class="hd">The control that matters</span>Spending limits enforced in the purchasing system, not in the prompt.</div>
</div>
</div>

{{% note %}}
- The same tool appears twice at two levels. That is the per-tool dial in practice: the level depends on the amount and the counterparty, not on the function name.
- Supplier master data — bank details in particular — stays off the list. It is the classic payment-fraud target, and an agent that reads supplier emails is exposed to prompt injection.
- The existing delegation-of-authority policy for human buyers is the starting point for these limits.
- Tool names and levels here are illustrative.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Supply chain and procurement &middot; 3 of 4</p>

# The value hypothesis

<div class="card"><span class="hd">Expected value</span>Fewer stockouts and expediting costs, lower working capital, and shorter sourcing cycles.</div>
<div class="card"><span class="hd">Measure</span><strong>Service level</strong>, <strong>inventory turns</strong>, and <strong>purchase-cycle time</strong>.</div>
<div class="card warn"><span class="hd">Baseline first</span>These metrics move with demand, season and supplier performance. Compare against a control group of products or sites, not against last year.</div>

<p class="refs">An agent acting on poor master data makes expensive decisions faster. The data work comes first.</p>

{{% note %}}
- Attribution is the hard part here. Inventory turns improve for many reasons, and an agent launched during a calm quarter will look brilliant.
- The footer is the most practical line on the slide. Organisations getting value from operational agents are generally the ones that already had clean data and clear rules.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Supply chain and procurement &middot; 4 of 4</p>

# The evidence

<div class="card"><span class="hd">Blue Yonder AI agents &mdash; retail, manufacturing, logistics &middot; type P</span>A vendor product page describing supply-chain agents for planning, warehouse, transportation and retail workflows.</div>
<div class="card"><span class="hd">Yin et al. (2025 preprint) &mdash; e-commerce retail &middot; type I</span>An agentic planning framework deployed in JD.com's operations. The authors report about 22% better planning accuracy and a 2% higher in-stock rate. Not yet peer-reviewed, and the results are reported by the team that built it.</div>
<div class="card warn"><span class="hd">What the evidence does not prove</span>Planning, not purchasing. The vendor page reports no customer results, and the JD.com figures are a self-reported preprint about planning. Nothing here shows an agent placing purchase orders or committing spend.</div>
<div class="card"><span class="hd">Ask</span>Which of these agents place orders, and which only recommend? What limits are built in?</div>

<p class="refs"><a href="https://blueyonder.com/why-blue-yonder/ai-and-machine-learning/ai-agents">Blue Yonder, AI agents for supply chain software</a> &middot; <a href="https://arxiv.org/abs/2509.03811">Yin et al., Rethinking Supply Chain Planning: A Generative Paradigm</a> &middot; Background: <a href="https://www.deloitte.com/us/en/services/consulting/blogs/business-operations-room/multi-agent-ai-sourcing-procurement.html">Deloitte, Multi-agentic AI for sourcing and procurement</a></p>

{{% note %}}
- One product page supports three industries in our matrix, because the vendor sells to all three. That is breadth of marketing, not breadth of evidence.
- The solution title says &ldquo;supply chain and procurement&rdquo;; the reference mostly covers the first half. Worth saying out loud.
- The JD.com paper is the weakest of the I references: a preprint, about planning rather than purchasing, with numbers from the deploying team. It is here because it is the closest thing to a production result that could be found, which tells you how thin this row is.
{{% /note %}}

***

<!-- ===== SECTION 5 — REVENUE AND CUSTOMER ===== -->
{{< slide background-color="#003478" class="section" >}}

# Revenue and Customer

<p>Customer-service resolution &middot; Sales and marketing execution</p>

{{% note %}}
Part five: the agent now speaks to people outside the firm, in the firm's voice.
{{% /note %}}

***

{{< slide class="fs50" >}}

<p class="kicker">Customer-service resolution &middot; 1 of 3</p>

# The job and the team

<div class="cols2">
<div>
<p class="sub">What it does</p>
<p>Triages incoming requests, retrieves account and order context, answers questions, performs permitted fixes such as a replacement or refund, and escalates exceptions.</p>
<p class="sub">Agents</p>
<div class="card"><span class="hd">Intake / intent</span>Works out what the customer wants.</div>
<div class="card"><span class="hd">Knowledge and policy</span>Finds the rule that applies.</div>
<div class="card"><span class="hd">Action / fulfilment</span>Performs the permitted fix.</div>
<div class="card"><span class="hd">Escalation / quality</span>Hands over to a person.</div>
</div>
<div>
<p class="sub">Tools and the dial</p>
<table class="plain">
<tr><th>Tool</th><th>Level</th></tr>
<tr><td><code>lookup_order</code></td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>answer_policy_question</code></td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>issue_refund</code> (under ceiling)</td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>issue_refund</code> (above ceiling)</td><td class="lv">2 &middot; Approval</td></tr>
<tr><td><code>close_account</code></td><td class="lv">Not granted</td></tr>
</table>
<p class="sub">Resources</p>
<p>Chat, voice and email channels, CRM and ticketing APIs, order and billing systems, approved knowledge base, refund limits, human service team.</p>
</div>
</div>

{{% note %}}
- This is the refund trace from the first half, now drawn as a team. We already walked through the mechanics, so this solution gets three slides instead of four.
- The refund ceiling is the autonomy decision. Someone signs off on that number for human agents today; the same person should sign off on this one.
- Three failure modes to name: a misread intent, where an enquiry is treated as a request; prompt injection through the customer's own message; and a ceiling that lives in the prompt rather than the payment wrapper.
- Tool names and levels here are illustrative.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Customer-service resolution &middot; 2 of 3</p>

# The value hypothesis

<div class="card"><span class="hd">Expected value</span>Faster resolution and 24/7 coverage; lower cost per contact and improved customer retention &mdash; <em>subject to quality controls</em>.</div>
<div class="card"><span class="hd">Measure</span><strong>Resolution time</strong>, <strong>cost per contact</strong>, <strong>retention</strong>, and the share of contacts resolved without a person.</div>
<div class="card warn"><span class="hd">Baseline first</span>Cost per contact is easy to cut by making it hard to reach a person. Measure repeat contacts and retention alongside it.</div>

<p class="refs">A contact the agent closed that the customer reopened the next day is not a resolution.</p>

{{% note %}}
- This is the business case most likely to be approved on cost alone, and the one where cost alone is most misleading.
- &ldquo;Deflection&rdquo; and &ldquo;containment&rdquo; are the vendor words for a customer who did not reach a human. Ask whether the customer's problem was solved.
- Retention is the slow metric and the one that matters. It takes quarters, not weeks, to show up.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Customer-service resolution &middot; 3 of 3</p>

# The evidence

<div class="card"><span class="hd">Salesforce Agentforce for Financial Services &mdash; banking, insurance &middot; type P</span>A product announcement describing agents for lost-card reports, fee reversals, insurance coverage questions, and escalation.</div>
<div class="cols2">
<div>
<div class="card"><span class="hd">Brynjolfsson, Li &amp; Raymond, <em>QJE</em> (2025) &middot; type I</span>5,172 support agents given an AI assistant resolved 15% more issues per hour on average, with the largest gains for less experienced agents.</div>
</div>
<div>
<div class="card warn"><span class="hd"><em>Moffatt v. Air Canada</em> (2024) &middot; type I</span>A tribunal held the airline liable for negligent misrepresentation after its website chatbot gave a customer wrong information about bereavement fares.</div>
</div>
</div>
<div class="card warn"><span class="hd">What the evidence does not prove</span>Assistance and liability, not autonomous resolution. The announcement names no deployment; the QJE study measured people using a reply-suggesting assistant; the tribunal shows the firm answers for what its bot says. No source shows an agent issuing refunds on its own, with outcomes.</div>
<div class="card"><span class="hd">Ask</span>In a regulated industry: who is accountable for what the agent tells a customer about their coverage?</div>

<p class="refs"><a href="https://www.salesforce.com/news/stories/agentforce-for-financial-services-announcement/">Salesforce, Salesforce introduces Agentforce for Financial Services</a> (2025) &middot; <a href="https://academic.oup.com/qje/article/140/2/889/7990658">Brynjolfsson, Li &amp; Raymond, Generative AI at Work</a> &middot; <a href="https://www.americanbar.org/groups/business_law/resources/business-law-today/2024-february/bc-tribunal-confirms-companies-remain-liable-information-provided-ai-chatbot/">Moffatt v. Air Canada, 2024 BCCRT 149</a></p>

{{% note %}}
- Look at the examples the vendor chose: a fee reversal moves money; a coverage answer can be relied on by a customer in a claim. These are consequential actions in regulated industries.
- That is a reason for care, not a reason to dismiss it. It is where the autonomy dial and the audit trail earn their keep.
- The QJE study is the best-known field evidence on generative AI at work. Note what it measured: human agents with an assistant suggesting replies, not an agent resolving cases alone.
- The Air Canada case answers the accountability question directly. The airline argued the chatbot was responsible for its own words; the tribunal disagreed. What your agent tells a customer, you told the customer.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Sales and marketing execution &middot; 1 of 4</p>

# The job

<div class="cols2">
<div>
<p class="sub">What it does</p>
<div class="card">Qualifies leads and researches accounts.</div>
<div class="card">Drafts personalised outreach and updates the CRM.</div>
<div class="card">Tests campaign variants, with approval gates.</div>
</div>
<div>
<p class="sub">What it replaces</p>
<div class="card warn">A seller spending the morning on account research and CRM entry, and a marketer building each segment and variant by hand.</div>
<p>The pitch is seller capacity: more time in front of customers.</p>
</div>
</div>

{{% note %}}
- The source material itself says &ldquo;with approval gates.&rdquo; Hold on to that; it is the control this solution depends on.
- The capacity argument is real — administrative work does consume a large share of a seller's week — but freed time only becomes revenue if it is spent selling.
{{% /note %}}

***

{{< slide class="fs50" >}}

<p class="kicker">Sales and marketing execution &middot; 2 of 4</p>

# The team

<div class="cols2">
<div>
<p class="sub">Agents</p>
<div class="card"><span class="hd">Prospect research</span>Builds the account picture.</div>
<div class="card"><span class="hd">Lead scoring</span>Ranks who to contact.</div>
<div class="card"><span class="hd">Content / campaign</span>Drafts outreach and variants.</div>
<div class="card"><span class="hd">CRM follow-up</span>Logs activity and next steps.</div>
<div class="card"><span class="hd">Compliance review</span>Checks consent and brand rules.</div>
</div>
<div>
<p class="sub">Tools and the dial</p>
<table class="plain">
<tr><th>Tool</th><th>Level</th></tr>
<tr><td><code>research_account</code></td><td class="lv">4 &middot; Silent</td></tr>
<tr><td><code>update_crm_record</code></td><td class="lv">3 &middot; Notify</td></tr>
<tr><td><code>draft_outreach</code></td><td class="lv">1 &middot; Advise</td></tr>
<tr><td><code>send_email_to_prospect</code></td><td class="lv">2 &middot; Approval</td></tr>
<tr><td><code>offer_discount</code></td><td class="lv">Not granted</td></tr>
</table>
<p class="sub">Resources</p>
<p>CRM, product and pricing catalogue, consent records, campaign platform, customer data, brand guidelines, sales approvals.</p>
</div>
</div>

{{% note %}}
- Sending an email is the underrated tool. It is irreversible, it is external, and it speaks in the company's voice.
- Consent records are a resource, not a detail. An agent that emails people who opted out creates a regulatory problem at machine speed.
- Compliance review as a separate agent is the independent-review case for multi-agent design — one agent checking another's work.
- Tool names and levels here are illustrative.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Sales and marketing execution &middot; 3 of 4</p>

# The value hypothesis

<div class="card"><span class="hd">Expected value</span>Higher seller capacity, improved conversion and campaign effectiveness, and potential revenue growth.</div>
<div class="card"><span class="hd">Measure</span><strong>Qualified pipeline</strong> and <strong>incremental conversion</strong>.</div>
<div class="card warn"><span class="hd">Baseline first</span>&ldquo;Incremental&rdquo; needs a holdout group that did not get the agent. Without one you are measuring the sales cycle, not the system.</div>

<p class="refs">Emails sent and leads touched are activity measures. Volume is what agents produce most easily and what buyers value least.</p>

{{% note %}}
- Marketing already knows how to run a holdout test. Insist on one.
- The risk on the other side of the ledger is volume. If every firm's agent sends more personalised outreach, response rates fall for everyone, and the brand pays for it.
{{% /note %}}

***

{{< slide class="fs55" >}}

<p class="kicker">Sales and marketing execution &middot; 4 of 4</p>

# The evidence

<div class="card"><span class="hd">Salesforce retail Agentforce presentation &mdash; retail &middot; type P</span>A vendor presentation describing campaign and content agents and segmented retail campaigns.</div>
<div class="card"><span class="hd">Fang et al. (2025 preprint) &mdash; online retail &middot; type I</span>Randomised field experiments on a large cross-border retail platform, across seven generative-AI workflows in customer service, product matching, advertising and seller services. Sales effects ranged from none detectable to 16.3%, and were positive in four of the seven.</div>
<div class="card warn"><span class="hd">What the evidence does not prove</span>Brand mentions are not deployments, and the experiments test one retail platform's automated workflows, not an agent selling. Three of the seven workflows showed no positive sales effect: expect uneven results, and test each workflow separately.</div>
<div class="card"><span class="hd">Ask</span>Which named customer runs which agent, in production, and what was the holdout result?</div>

<p class="refs"><a href="https://www.salesforce.com/plus/experience/connections_2026/series/connections_2026_highlights/episode/episode-s1e32">Salesforce, Retail's AI moment: Inside Agentforce adoption</a> (2026) &middot; <a href="https://arxiv.org/abs/2510.12049">Fang et al., Generative AI and Sales Productivity: Field Experiments in Online Retail</a></p>

{{% note %}}
- A conference presentation is the weakest evidence type in the deck, and the most persuasive in the room. Logos on a slide are not deployments.
- Same pattern as the Saxo example: a recognisable name placed near a capability.
- The retail experiments are the holdout test this section asked for, run at scale. The useful number is not the 16.3%; it is &ldquo;four of seven.&rdquo; Three workflows showed no positive sales effect, and nobody could have said in advance which three.
{{% /note %}}

***

<!-- ===== SECTION 6 — ACROSS THE SIX ===== -->
{{< slide background-color="#003478" class="section" >}}

# Across the Six

<p>What the evidence shows, and what all six have in common</p>

{{% note %}}
Part six: step back from the individual solutions.
{{% /note %}}

***

{{< slide class="fs45" >}}

# Solution &times; industry evidence map

<!-- Eight industry columns: this table and the research sources table are the two exceptions to the deck-wide table size. -->
<table class="plain" style="font-size:calc(var(--r-main-font-size) * 0.5)">
<tr><th style="width:27%">Business solution</th><th class="c">Banking</th><th class="c">Insurance</th><th class="c">Construction</th><th class="c">Telecom</th><th class="c">Retail</th><th class="c">Manufacturing</th><th class="c">Logistics</th><th class="c">Tech and services</th></tr>
<tr><td>Enterprise knowledge and research</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">C</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">I</td></tr>
<tr><td>Software engineering and modernisation</td><td class="c lv">A</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">I</td></tr>
<tr><td>IT service and incident operations</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">P</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">I</td></tr>
<tr><td>Supply chain and procurement</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">P &middot; I</td><td class="c lv">P</td><td class="c lv">P</td><td class="c">&mdash;</td></tr>
<tr><td>Customer-service resolution</td><td class="c lv">P</td><td class="c lv">P</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">I</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">I</td></tr>
<tr><td>Sales and marketing execution</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c lv">P &middot; I</td><td class="c">&mdash;</td><td class="c">&mdash;</td><td class="c">&mdash;</td></tr>
</table>

<p class="refs" style="font-size:0.8em"><strong>P</strong> product documentation or advertisement &middot; <strong>C</strong> vendor-published customer story &middot; <strong>A</strong> assistance story plus separate agent documentation &middot; <strong>I</strong> research with a stated method &middot; <strong>&mdash;</strong> no direct evidence in the references used here. A filled cell is an illustrative fit, not adoption prevalence or proven return.</p>

{{% note %}}
- Read this as a map of the references we used today, not as a survey of industries.
- A blank cell means &ldquo;not evidenced by these references,&rdquo; not &ldquo;impossible.&rdquo; Customer service in telecom or retail is entirely plausible; we simply did not cite it.
- The rows follow the order of the session.
- The last column was added for the independent studies, because most of them were run at software, cloud and consulting firms rather than in the seven industries the vendors target.
{{% /note %}}

***

{{< slide class="fs55" >}}

# What the map tells you

<div class="cols3">
<div>
<div class="card"><span class="hd">Nine vendor cells</span>Seven P, one C and one A: almost all of it a vendor describing its own product.</div>
</div>
<div>
<div class="card"><span class="hd">Seven research cells</span>Every solution now has at least one study with a method you can inspect.</div>
</div>
<div>
<div class="card warn"><span class="hd">Mostly assistance, mostly tech</span>The strongest studies measure people working with an assistant, at software and services firms.</div>
</div>
</div>

<div class="card warn" style="margin-top:0.6em"><span class="hd">What to conclude</span>AI assistance has measured, uneven benefits. Evidence that an <em>autonomous</em> agent pays back, in a firm like yours, is something you will still have to generate yourself.</div>

{{% note %}}
- Count the cells with the room: nine vendor entries, seven research entries.
- Look at where the two kinds sit. Vendor claims are spread across the industries vendors sell to. Research clusters in the last column and in retail, where firms had the data and the scale to run experiments.
- The research is also uneven in result: developers sped up in one trial and slowed down in another; four of seven retail workflows raised sales and three did not.
- This is not an argument against investing. It is an argument for a pilot with a baseline, a metric, and a stopping rule — because nobody else's numbers will substitute for your own.
{{% /note %}}

***

{{< slide class="fs55" >}}

# Can an agent do the work alone?

<div class="cols2">
<div>
<div class="card"><span class="hd">TheAgentCompany &middot; type I</span>A benchmark that simulates a small software company, with tasks in engineering, project management and finance. The most competitive agent tested completed <strong>30%</strong> of tasks autonomously.</div>
</div>
<div>
<div class="card"><span class="hd">&tau;-bench &middot; type I</span>Customer-service tasks with tools and policy rules to follow. The leading agents of 2024 succeeded on <strong>under 50%</strong> of tasks, and on under 25% of retail tasks when the same task had to succeed eight times running.</div>
</div>
</div>

<div class="card warn"><span class="hd">Read the second number</span>A business process runs the same task thousands of times. An agent that is right most of the time, but not the same way twice, fails the consistency test before it fails the capability test.</div>

<p class="refs"><a href="https://arxiv.org/abs/2412.14161">Xu et al., TheAgentCompany: Benchmarking LLM Agents on Consequential Real World Tasks</a> &middot; <a href="https://arxiv.org/abs/2406.12045">Yao et al., &tau;-bench: A Benchmark for Tool-Agent-User Interaction in Real-World Domains</a>. Benchmark scores date quickly; these are the figures the papers report.</p>

{{% note %}}
- The field studies mostly measure assistance. Benchmarks are where autonomy is actually tested, on simulated work with a known right answer.
- Both results say the same thing: simple tasks are within reach, long multistep ones are not yet reliable.
- Be straightforward about the dates. Models improve quickly and newer ones score higher. The durable point is the method: ask a vendor for task-completion and repeat-consistency figures, not a demo.
- This connects to the dial. A tool earns level 3 or 4 on measured reliability, and these are the kinds of measurement to ask for.
{{% /note %}}

***

{{< slide class="fs55" >}}

# What all six need underneath

<div class="cols2">
<div>
<div class="card"><span class="hd">Model and orchestration layer</span>The engine and the thing that routes work.</div>
<div class="card"><span class="hd">Governed data access</span>The agent sees what the requester may see.</div>
<div class="card"><span class="hd">Least-privilege tool permissions</span>Each tool granted separately, with a ceiling.</div>
</div>
<div>
<div class="card"><span class="hd">Audit logs</span>A reconstructable record of what was done and why.</div>
<div class="card"><span class="hd">Evaluation and monitoring</span>Before launch, and continuously after.</div>
<div class="card warn"><span class="hd">Human approval for consequential actions</span>Level 2 on the dial, with a reviewer who has time to look.</div>
</div>
</div>

<p class="refs">This foundation is shared. Built once, it carries the second and third solution at a fraction of the cost of the first.</p>

{{% note %}}
- Six solutions, one foundation. That is the portfolio argument: the first agentic project is expensive mostly because it pays for this layer.
- It also argues for sequencing. Start with a read-mostly solution — knowledge and research — build the foundation there, and reuse it when the tools start to write.
- None of these six items is a model capability. They are all engineering and governance.
{{% /note %}}

***

{{< slide class="fs55" >}}

# Two cautions before you fund one

<div class="cols2">
<div>
<p class="sub">Four roles is not four models</p>
<div class="card">The agent roles on each &ldquo;team&rdquo; slide are <strong>illustrative architectures</strong>. One agent with several tools may be enough.</div>
<p>Ask why the design needs more than one agent, and which one is accountable for the output.</p>
</div>
<div>
<p class="sub">Value is a hypothesis</p>
<div class="card warn">Expected value is something to <strong>validate against a workflow baseline</strong>, not a guaranteed return.</div>
<p>Ask for the baseline, the metric, the comparison group, and the date on which you will decide to stop.</p>
</div>
</div>

{{% note %}}
- The left column is the &ldquo;when not to build a team&rdquo; slide from the first half, applied. Vendor diagrams with many agents look sophisticated; many are a workflow with one uncertain step.
- The right column is the discipline. A pilot without a stopping rule is not a pilot.
{{% /note %}}

***

{{< slide class="fs55" >}}

# The riskiest tool in each solution

<table class="plain">
<tr><th>Solution</th><th>Riskiest tool</th><th>Why</th><th>Start at</th></tr>
<tr><td>Enterprise knowledge and research</td><td>Reading across silos</td><td>Exposes documents the requester should not see</td><td class="lv">4, permission-aware</td></tr>
<tr><td>Software engineering</td><td>Merging to the main branch</td><td>Unreviewed code reaches production</td><td class="lv">2 &middot; Approval</td></tr>
<tr><td>IT service and incident ops</td><td>Executing a production runbook step</td><td>An outage caused at machine speed</td><td class="lv">2 &middot; Approval</td></tr>
<tr><td>Supply chain and procurement</td><td>Creating a purchase order</td><td>Commits spend to an outside party</td><td class="lv">2, then 3 under a limit</td></tr>
<tr><td>Customer-service resolution</td><td>Issuing a refund</td><td>Moves money on a customer's say-so</td><td class="lv">2, then 3 under a ceiling</td></tr>
<tr><td>Sales and marketing</td><td>Sending external email</td><td>Irreversible, in the company's voice</td><td class="lv">2 &middot; Approval</td></tr>
</table>

<p class="refs">Move a tool up the dial only on measured error rates from a period at the level below.</p>

{{% note %}}
- One line per solution. If you remember nothing else about each one, remember its riskiest tool.
- The pattern: every solution has a large read-only surface that can run at level 4, and one or two tools that deserve a human.
- Moving up the dial is earned with data, tool by tool.
{{% /note %}}

***

<!-- ===== TAKEAWAYS ===== -->
{{< slide class="fs60" >}}

# Takeaways

<div class="card"><span class="hd">An agent is a process that acts</span>It plans, calls tools and changes systems. The question is not what it can do; it is what it is allowed to do without asking.</div>
<div class="card"><span class="hd">Read every solution the same way</span>The job, the team, the value hypothesis, the evidence. The four questions outlast any product.</div>
<div class="card"><span class="hd">Every tool is a permission, set per tool</span>Each solution has a wide read-only surface and one or two tools that deserve a human. Ceilings belong in code.</div>
<div class="card warn"><span class="hd">Capability is not deployment, and deployment is not return</span>Vendors describe products; research mostly measures assistance, with uneven results. The proof for your firm comes from your own baseline.</div>

{{% note %}}
- If one sentence survives the session: **fund the workflow you can measure, grant the tools you can reverse, and trust the evidence you generated yourself.**
- The shared foundation is the quiet strategic point. The first solution pays for the layer the next ones reuse.
{{% /note %}}

***

<!-- ===== SOURCES ===== -->
{{< slide class="fs50" >}}

# Sources: vendor evidence

<table class="plain">
<tr><th>Solution</th><th>Reference</th><th>Type</th></tr>
<tr><td>Enterprise knowledge and research</td><td><a href="https://www.glean.com/resources/customer-stories/mccarthy-holdings-inc">Glean, McCarthy Holdings, Inc. customer story</a></td><td class="lv">C</td></tr>
<tr><td rowspan="2">Software engineering</td><td><a href="https://www.microsoft.com/en/customers/story/24389-saxo-bank-github-copilot">Microsoft, GitHub Copilot accelerates coding at Saxo Bank</a> (2025)</td><td class="lv" rowspan="2">A</td></tr>
<tr><td><a href="https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent">GitHub Docs, About GitHub Copilot cloud agent</a></td></tr>
<tr><td>IT service and incident ops</td><td><a href="https://www.servicenow.com/docs/r/zurich/telecom-media-technology/now-assist-for-telecom-media-and-technology/network-incident-analysis-usecase.html">ServiceNow, Analyze network incidents agentic workflow</a> (2025)</td><td class="lv">P</td></tr>
<tr><td>Supply chain and procurement</td><td><a href="https://blueyonder.com/why-blue-yonder/ai-and-machine-learning/ai-agents">Blue Yonder, AI agents for supply chain software</a></td><td class="lv">P</td></tr>
<tr><td>Customer-service resolution</td><td><a href="https://www.salesforce.com/news/stories/agentforce-for-financial-services-announcement/">Salesforce, Agentforce for Financial Services</a> (2025)</td><td class="lv">P</td></tr>
<tr><td>Sales and marketing</td><td><a href="https://www.salesforce.com/plus/experience/connections_2026/series/connections_2026_highlights/episode/episode-s1e32">Salesforce, Retail's AI moment: Inside Agentforce adoption</a> (2026)</td><td class="lv">P</td></tr>
</table>

<p class="refs" style="font-size:0.85em"><strong>Background:</strong> McKinsey, <a href="https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai">The state of AI in 2026</a>; <a href="https://www.mckinsey.com/featured-insights/mckinsey-explainers/what-is-an-ai-agent">What is an AI agent?</a>; <a href="https://www.mckinsey.com/capabilities/mckinsey-technology/our-insights/building-the-foundations-for-agentic-ai-at-scale">Building the foundations for agentic AI at scale</a>; <a href="https://www.mckinsey.com/capabilities/quantumblack/our-insights/seizing-the-agentic-ai-advantage">Seizing the agentic AI advantage</a>. Deloitte, <a href="https://www.deloitte.com/us/en/services/consulting/blogs/business-operations-room/multi-agent-ai-sourcing-procurement.html">Multi-agentic AI for sourcing and procurement</a>. Russell &amp; Norvig, <em>Artificial Intelligence: A Modern Approach</em>. <strong>Figures:</strong> the diagrams in the first section are redrawn from the Agentic Systems deck; the four design patterns follow Yugank Aman, &ldquo;Top Agentic AI Design Patterns for Architecting AI Systems,&rdquo; <em>Medium</em>. Tool lists and autonomy levels on the &ldquo;team&rdquo; slides are illustrative.</p>

{{% note %}}
- Worth saying out loud: every reference in this table is published by a vendor. In a session about reading evidence, labelling our own sources is part of the lesson.
- For anyone who wants more depth on the first half, the full Agentic Systems deck is on the course site.
{{% /note %}}

***

{{< slide class="fs50" >}}

# Sources: research evidence

<table class="plain" style="font-size:calc(var(--r-main-font-size) * 0.5)">
<tr><th>Solution</th><th>Reference (all type I)</th><th>Method</th></tr>
<tr><td>Enterprise knowledge and research</td><td><a href="https://pubsonline.informs.org/doi/full/10.1287/orsc.2025.21838">Dell'Acqua et al., Navigating the Jagged Technological Frontier</a>, <em>Organization Science</em> 37(2), 2026</td><td>Field experiment</td></tr>
<tr><td rowspan="2">Software engineering</td><td><a href="https://pubsonline.informs.org/doi/10.1287/mnsc.2025.00535">Cui et al., The Effects of Generative AI on High-Skilled Work</a>, <em>Management Science</em></td><td>Three field experiments</td></tr>
<tr><td><a href="https://arxiv.org/abs/2507.09089">Becker et al. (METR), Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity</a>, 2025</td><td>Randomised trial</td></tr>
<tr><td>IT service and incident ops</td><td><a href="https://arxiv.org/abs/2403.04123">Roy et al., Exploring LLM-based Agents for Root Cause Analysis</a>, FSE 2024</td><td>Evaluation on real incidents</td></tr>
<tr><td>Supply chain and procurement</td><td><a href="https://arxiv.org/abs/2509.03811">Yin et al., Rethinking Supply Chain Planning: A Generative Paradigm</a>, preprint 2025</td><td>Deployment report</td></tr>
<tr><td rowspan="2">Customer-service resolution</td><td><a href="https://academic.oup.com/qje/article/140/2/889/7990658">Brynjolfsson, Li &amp; Raymond, Generative AI at Work</a>, <em>QJE</em> 140(2), 2025</td><td>Staggered rollout study</td></tr>
<tr><td><a href="https://www.americanbar.org/groups/business_law/resources/business-law-today/2024-february/bc-tribunal-confirms-companies-remain-liable-information-provided-ai-chatbot/">Moffatt v. Air Canada, 2024 BCCRT 149</a></td><td>Tribunal decision</td></tr>
<tr><td>Sales and marketing</td><td><a href="https://arxiv.org/abs/2510.12049">Fang et al., Generative AI and Sales Productivity: Field Experiments in Online Retail</a>, preprint 2025</td><td>Seven field experiments</td></tr>
<tr><td rowspan="2">Across the six</td><td><a href="https://arxiv.org/abs/2412.14161">Xu et al., TheAgentCompany</a>, 2024</td><td>Benchmark</td></tr>
<tr><td><a href="https://arxiv.org/abs/2406.12045">Yao et al., &tau;-bench</a>, 2024</td><td>Benchmark</td></tr>
</table>

{{% note %}}
- Three of these are published in leading journals, one at a peer-reviewed software engineering conference, and the rest are preprints or benchmarks. One is a legal decision.
- Independent of the vendor is not the same as independent of the firm: the incident-analysis and supply-chain papers report on the authors' own systems.
{{% /note %}}

***

<!-- ===== ACTIVITY ===== -->
{{< slide background-color="#003478" class="section" >}}

# Group Activity

{{% note %}}
Five questions. Small groups, then report back.
{{% /note %}}

***

{{< slide class="dq fs50" >}}

### Group Activity
# Propose an agentic solution

<div class="card"><span class="hd">1 &middot; The job</span>Identify a concrete business problem that an agentic solution could solve. Draw on your own work if you can, but leave out anything confidential or proprietary; alternatively, choose a fictional organisation facing a significant problem. Describe the workflow the solution would replace.</div>
<div class="card"><span class="hd">2 &middot; The team</span>Design the agents and their tools. For each agent, describe its role and the tools it uses.</div>
<div class="card"><span class="hd">3 &middot; The case for it</span>
<div class="cols4 sub4">
<div class="card"><span class="hd">Value hypothesis</span>Name the baseline metric you would measure before the project starts, and who owns that number today.</div>
<div class="card"><span class="hd">Evidence</span>Find evidence that supports your proposal, and label each source P, C, A or I.</div>
<div class="card"><span class="hd">Autonomy dial</span>Set a level, 1 to 4, for each tool. Which tool would you not grant at all, and which existing policy should set the limits?</div>
<div class="card"><span class="hd">Readiness</span>What must be true of your data, your processes and your regulation for the solution to work? What would you fix first?</div>
</div>
</div>
<div class="card warn"><span class="hd">4 &middot; Deliverable</span>Prepare a slide deck for a 7-minute class presentation, with references, further thoughts and comments in the speaker notes. Submit it to iCollege as a group assignment.</div>


***

{{< slide state="jitter" background-image="/imgs/slides/Philips_PM5544.svg" >}}
<div class="background-box">
    <h1 contenteditable="true" style="color:white; text-shadow: 2px 2px 4px rgba(0,0,0,0.7);" >Group Activity</h1>
    <p contenteditable="true" style="color:white; text-shadow: 2px 2px 4px rgba(0,0,0,0.7);" >Please be back by 5:00 PM</p>
</div>


