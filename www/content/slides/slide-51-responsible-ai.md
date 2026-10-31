+++
title = "Responsible AI"
description = "How to govern Agentic AI systems — from values to principles, risk tiers, governance and accountability, told through one running case"
weight = 51
outputs = ["Reveal"]
math = true
thumbnail = "/imgs/slides/responsible_ai_3.png"

[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"

+++

<!--
    Slide deck: Responsible AI.

    Spine: Opening -> Ethics -> Principles -> Risk -> Governance -> Accountability -> Close.
    Each layer turns the one before it into practice. Governance is before the
    fact (who approves, what is reviewed); Accountability is after the fact
    (who answers, recourse, audit trail, incident response).

    One running case threads every section: the Replit agent that deleted
    SaaStr's production database (July 2025), and SaaStr's follow-up (Oct 2026).
    Each section ends with a "Case lens" slide.

    Two kinds of slides are used here:
      1. Diagram slides — redrawn as inline SVG / HTML from the NotebookLM
         export (originals: static/imgs/Engineering_Agentic_Governance_NN.png).
      2. Native slides — section dividers, framing, case and exercise slides,
         using the helper classes below (same set as slide-30-agentic-systems).
    Keep blank lines out of <svg> blocks: Markdown ends an HTML block at one.
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
.reveal .slides section[class*="fs"] h1 { font-size: 52px; margin-bottom: 0.4em; }
.reveal .slides section[class*="fs"] h3 { color: #CC0000; font-size: 26px; margin-bottom: 0.1em; }

.reveal .cols2 { display: grid; grid-template-columns: 1fr 1fr; gap: 0 1.8em; align-items: start; }
.reveal .cols3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0 1.4em; align-items: start; }
.reveal .cols2 p, .reveal .cols3 p { margin: 0.35em 0; }

.reveal .sub { color: #CC0000; font-weight: 700; margin: 0.8em 0 0.25em 0; }
.reveal .cols2 > div > .sub:first-child,
.reveal .cols3 > div > .sub:first-child { margin-top: 0; }

.reveal .card { background: #f4f6f9; border-left: 4px solid #003478;
                border-radius: 6px; padding: 0.5em 0.9em; margin: 0 0 0.55em 0; text-align: left; }
.reveal .card .hd { color: #003478; font-weight: 700; display: block; margin-bottom: 0.1em; }
.reveal .card.warn { border-left-color: #CC0000; }
.reveal .card.warn .hd { color: #CC0000; }

.reveal .term { color: #CC0000; font-weight: 700; }
.reveal .lead { font-style: italic; color: #555; margin-bottom: 0.8em; }
.reveal .refs { font-size: 0.62em; color: #777; margin-top: 0.9em; }
.reveal .refs a { color: #777; }
.reveal .punch { color: #003478; font-weight: 700; margin-top: 0.8em; }

.reveal table.plain { width: 100%; border-collapse: collapse; border: none; font-size: 1.1em; }
.reveal table.plain th { color: #003478; text-align: left; border-bottom: 2px solid #003478;
                         background: none; border-top: none; border-left: none; border-right: none;
                         padding: 0.3em 0.5em; }
.reveal table.plain td { border: none; border-bottom: 1px solid #ddd; padding: 0.3em 0.5em; vertical-align: top; }
.reveal table.plain tbody tr:nth-child(even) { background: none; }
.reveal table.plain td.lv { color: #CC0000; font-weight: 700; white-space: nowrap; }

/* Redrawn diagrams (inline SVG) and their layouts. */
.reveal svg.dg { width: 100%; height: auto; display: block; margin: 0.3em 0 0.6em 0; }
.reveal svg.dg text { font-family: inherit; }
.reveal .g23 { display: grid; grid-template-columns: 2fr 3fr; gap: 0 1.6em; align-items: center; }
.reveal .g32 { display: grid; grid-template-columns: 3fr 2fr; gap: 0 1.6em; align-items: center; }
.reveal .pipe { display: grid; grid-template-columns: 1fr auto 1fr auto 1fr auto 1fr; gap: 0 0.4em; align-items: stretch; }
.reveal .pipe .card { margin: 0; }
.reveal .pipe .arr { align-self: center; color: #003478; }
.reveal .card .gate { display: block; margin-top: 0.5em; font-size: 0.85em; color: #777; font-style: italic; }
.reveal .card p.chk { margin: 0.3em 0; }
.reveal .tier { border-radius: 6px; padding: 0.5em 0.9em; text-align: left; }
.reveal .tier .hd { font-weight: 700; display: block; }
.reveal .tier.t1 { background: #003478; color: #fff; }
.reveal .tier.t2 { background: #3a5f99; color: #fff; }
.reveal .tier.t3 { background: #dce6f3; color: #003478; }
.reveal .up { text-align: center; color: #7f9cc6; line-height: 1.2; }
.reveal .card.co p { margin: 0.3em 0; }
.reveal .card ul { margin: 0.2em 0 0 1.1em; }
.reveal .card li { margin: 0.25em 0; }
.reveal .cols2.eq, .reveal .cols3.eq { align-items: stretch; }
.reveal .co-hd { display: flex; align-items: center; gap: 0.5em; margin-bottom: 0.2em; }
.reveal .co-hd img { width: 34px; height: 34px; margin: 0; border: none; box-shadow: none; background: none; }
.reveal .co-hd span { font-size: 1.3em; font-weight: 700; color: #003478; }
.reveal table.plain td.hl { background: #eef3fa; color: #003478; font-weight: 600; }

/* Section dividers — flat GSU Blue panel. */
.reveal .slides section.section { text-align: center; }
.reveal .slides section.section h1 { color: #fff; font-size: 2.3em; margin: 0; }
.reveal .slides section.section p { color: #c9d6e8; font-size: 0.66em; margin-top: 0.7em; }

/* The theme's footer branding and slide number are dark, drawn for white
   slides. Reverse them to white while a dark divider is on screen. */
.reveal:has(.slides section.section.present) .slide-footer img { filter: brightness(0) invert(1); }
.reveal:has(.slides section.section.present) .slide-number { color: #EDEEEF; }
</style>

<!-- ===== TITLE ===== -->
{{< slide background-image="/imgs/slides/responsible_ai_3.png" >}}
<div style="min-height: 15em;"></div>
<div style="margin:0; padding: 50; background-color: rgba(0,0,0,0.5); min-hight:100%; min-width:100%" >
    <h1 style="color:white; text-shadow: 2px 2px 4px rgba(0,0,0,0.7);" >Responsible AI</h1>
    <p style="color:white; text-shadow: 2px 2px 4px rgba(0,0,0,0.7);" > EMBA 8160 — Session 5</p>
</div>

{{% note %}}
- Last session we built agents. Today: how a leader makes sure they behave, and who answers when they don't.
- One story runs through the whole session. Keep it in your head; we will come back to it at the end of every section.
{{% /note %}}

***

<!-- 00 — Engineering the objective function -->
{{< slide class="fs55" >}}

### Blueprint
# Engineering the objective function

<p class="lead">A structural blueprint for ethics, governance and liability in agentic AI systems.</p>

<svg class="dg" viewBox="0 0 860 300" role="img" aria-label="An agent's proposed actions pass through a governance gate. Approved actions continue; others are blocked.">
<defs><marker id="a00b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<polygon points="180,150 145,89 75,89 40,150 75,211 145,211" fill="#dce6f3" stroke="#003478" stroke-width="3"/>
<text x="110" y="146" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">Agent</text>
<text x="110" y="168" text-anchor="middle" font-size="13" fill="#555">objective function</text>
<g stroke="#003478" stroke-width="3" fill="none">
<line x1="180" y1="150" x2="462" y2="60" marker-end="url(#a00b)"/>
<line x1="180" y1="150" x2="462" y2="150" marker-end="url(#a00b)"/>
<line x1="180" y1="150" x2="462" y2="240" marker-end="url(#a00b)"/>
</g>
<g stroke="#CC0000" stroke-width="3" fill="none" stroke-dasharray="6 4">
<line x1="180" y1="150" x2="440" y2="105"/>
<line x1="180" y1="150" x2="440" y2="195"/>
</g>
<text x="452" y="111" text-anchor="middle" font-size="22" font-weight="700" fill="#CC0000">&#10005;</text>
<text x="452" y="201" text-anchor="middle" font-size="22" font-weight="700" fill="#CC0000">&#10005;</text>
<rect x="468" y="30" width="56" height="240" rx="6" fill="#003478"/>
<text x="496" y="18" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Governance gate</text>
<text x="496" y="292" text-anchor="middle" font-size="13" fill="#555">permissions &#183; review &#183; logs</text>
<g stroke="#003478" stroke-width="3" fill="none">
<line x1="524" y1="60" x2="692" y2="60" marker-end="url(#a00b)"/>
<line x1="524" y1="150" x2="692" y2="150" marker-end="url(#a00b)"/>
<line x1="524" y1="240" x2="692" y2="240" marker-end="url(#a00b)"/>
</g>
<rect x="700" y="30" width="155" height="240" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<text x="777" y="140" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">Approved</text>
<text x="777" y="162" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">actions</text>
</svg>

<p class="refs">For: technical leads &#183; product managers &#183; enterprise executives</p>

{{% note %}}
- The subtitle is the agenda: ethics, governance, liability. The image is engineering-flavoured; the decisions in it are yours.
{{% /note %}}

***

<!-- ===== OUTLINE ===== -->
{{< slide class="fs55" >}}

# Outline

<p class="lead">From what we value to who answers for it &mdash; each step turns the one before it into practice.</p>

<table class="plain">
<thead><tr><th>Section</th><th>Question</th><th>What we cover</th></tr></thead>
<tbody>
<tr><td class="lv">Opening</td><td>Why does this matter?</td><td>The agent that deleted a production database</td></tr>
<tr><td class="lv">Ethics</td><td>What do we value?</td><td>Values, trade-offs, ethics vs. legal compliance</td></tr>
<tr><td class="lv">Principles</td><td>What do we commit to?</td><td>Common principles, and why companies publish them but rarely put them into practice</td></tr>
<tr><td class="lv">Risk</td><td>Where does it matter most?</td><td>Sorting use cases by stakes, autonomy and who is affected</td></tr>
<tr><td class="lv">Governance</td><td>How do we make it routine?</td><td>Roles, an inventory of AI systems, review checkpoints, reference frameworks</td></tr>
<tr><td class="lv">Accountability</td><td>Who answers?</td><td>Named owners, human oversight, recourse, incident response</td></tr>
<tr><td class="lv">Close</td><td>What do I do Monday?</td><td>Team breakouts, a leader&rsquo;s checklist, and your own Study Buddy</td></tr>
</tbody>
</table>

{{% note %}}
- The spine is abstract to concrete: why we care, what we commit to, where it matters most, how we make it routine, who answers for it.
- Executives personally own the last row. That is why we end there, not with the regulation.
- Every section closes with a &ldquo;case lens&rdquo; slide on the same running case.
{{% /note %}}

***

<!-- From values to answerability -->
{{< slide class="fs55" >}}

### The framework
# From values to answerability

<div class="card"><span class="hd">Ethics &mdash; what do we value?</span>The values the organization will defend, and the trade-offs between them when they collide. Judgment, not a checklist.</div>
<div class="card"><span class="hd">Principles &mdash; what do we commit to?</span>Values written down as commitments, and translated into product, process and business decisions.</div>
<div class="card"><span class="hd">Risk &mdash; where does it matter most?</span>Not every use case deserves the same scrutiny. Tier each one by stakes, autonomy and who is affected.</div>
<div class="card"><span class="hd">Governance &mdash; before the fact</span>Who approves, what gets reviewed, which risk tier gets which checkpoint across the lifecycle.</div>
<div class="card warn"><span class="hd">Accountability &mdash; after the fact</span>Who answers when harm happens, how affected people get recourse, the audit trail, incident response.</div>

{{% note %}}
- Values mean little without structures and owners. Each layer exists to make the one above it real.
- The split worth stressing: **governance is before the fact, accountability is after the fact.** Students tend to blur the two. Governance asks &ldquo;may we ship this?&rdquo;; accountability asks &ldquo;something went wrong &mdash; now what, and whose name is on it?&rdquo;
- Risk sits in the middle because it decides how much of the governance machinery a given system needs.
{{% /note %}}

***

<!-- ===== SECTION: OPENING ===== -->
{{< slide background-color="#003478" class="section" >}}

# Why Does This Matter?

<p>One agent, one written order, one deleted database</p>

{{% note %}}
About five minutes for the story. Tell it; do not read it.
{{% /note %}}

***

<!-- The two companies in the running case -->
{{< slide class="fs50" >}}

### Running case
# Meet the two companies

<div class="cols2 eq">
<div class="card co">
<div class="co-hd"><img src="/imgs/slide-51-responsible-ai/saastr-logo.png" alt="SaaStr logo"><span>SaaStr</span></div>
<p class="sub">The customer &mdash; the deployer</p>
<p>The largest community for business-software (B2B and SaaS) founders and executives. Founded in 2012 by <strong>Jason Lemkin</strong>, who earlier co-founded EchoSign (now Adobe Acrobat Sign).</p>
<p><strong>What it does:</strong> runs the SaaStr Annual conference and other events, publishes a widely read blog and podcast, and invests in early-stage startups through the SaaStr Fund.</p>
<p><strong>Why it matters here:</strong> its business runs on relationships, so its database of executives and companies is a core asset. Today it runs with a handful of people and more than 20 AI agents.</p>
</div>
<div class="card co">
<div class="co-hd"><img src="/imgs/slide-51-responsible-ai/replit-logo.png" alt="Replit logo"><span>Replit</span></div>
<p class="sub">The vendor &mdash; the agent&rsquo;s maker</p>
<p>A browser-based platform for writing, running and publishing software, used by millions of people. Founded in 2016 by <strong>Amjad Masad</strong> and co-founders; based in the San Francisco Bay Area.</p>
<p><strong>What it does:</strong> <em>Replit Agent</em> builds complete apps from plain-English instructions &mdash; &ldquo;vibe coding&rdquo; &mdash; and Replit hosts the result, including its database.</p>
<p><strong>Why it matters here:</strong> it markets the agent to non-programmers, so the user often cannot check what the agent did. In September 2025 it raised &#36;250 million.</p>
</div>
</div>

{{% note %}}
- One minute. The point is the roles, not the companies: SaaStr is the **deployer** (the customer using an agent on its own data); Replit is the **vendor** (the company that built and sells the agent). Most of the room will be in SaaStr&rsquo;s position.
- Lemkin is not a novice. He built and sold a software company and has spent a decade advising SaaS founders. If this can happen to him, it can happen to anyone in the room.
- Replit&rsquo;s pitch is that you do not need to read code. That is exactly why its agent&rsquo;s own account of what it did matters so much: the customer has no other way to check.
{{% /note %}}

***

<!-- Case: the Replit agent -->
{{< slide class="fs55" >}}

### Running case
# The agent that deleted the database

<div class="cols2">
<div>
<div class="card"><span class="hd">The setup &mdash; July 2025</span>SaaStr founder Jason Lemkin runs a public 12-day experiment, building an app with Replit&rsquo;s AI agent on real data. The agent makes changes he did not ask for and makes up data.</div>
<div class="card"><span class="hd">The written order</span>Lemkin tells the agent in writing to make no changes without his permission. The project is in a declared &ldquo;code and action freeze.&rdquo;</div>
<div class="card warn"><span class="hd">The deletion &mdash; day nine</span>The agent deletes the production database: records on 1,206 executives and more than 1,196 companies.</div>
</div>
<div>
<div class="card warn"><span class="hd">The false account</span>The agent says the data cannot be recovered. That is wrong &mdash; Lemkin restores it himself.</div>
<div class="card"><span class="hd">Replit&rsquo;s response</span>The CEO calls it unacceptable and offers a refund. Replit separates live data from the agent&rsquo;s working environment.</div>
<div class="card"><span class="hd">Two months later</span>Replit raises &#36;250 million and launches an agent it describes as ten times more autonomous.</div>
</div>
</div>

<p class="refs">Sources: <a href="https://fortune.com/2025/07/23/ai-coding-tool-replit-wiped-database-called-it-a-catastrophic-failure/">Fortune</a>, <a href="https://www.cio.com/article/4230232/the-replit-case-an-agent-a-written-order-and-a-deleted-database.html">CIO</a>, <a href="https://www.saastr.com/replits-new-release-address-most-of-the-challenges-we-hit-vibe-coding-but-is-prosumer-vibe-coding-really-ready-for-commercial-apps-yet/">SaaStr</a>, <a href="https://www.theregister.com/software/2025/07/21/vibe-coding-service-replit-deleted-production-database/719783">The Register</a></p>

{{% note %}}
- Well documented and easy to follow without technical background &mdash; and it maps onto all four lenses we use today.
- Dwell on the **written order**. Everyone in the room has written a policy that said &ldquo;do not.&rdquo; This agent had one, and it still had the permissions to do the thing it was told not to do.
- Then the **false account**: the system that caused the harm was also the only source of information about the harm, and that information was wrong.
- The last card is not a cheap shot at Replit. It is the market: the incident did not slow the company down. Hold that for the ethics discussion.
{{% /note %}}

***

<!-- Case: act two -->
{{< slide class="fs55" >}}

### Running case &mdash; act two
# A year later, the same leader, more agents

<div class="cols2">
<div>
<p class="sub">SaaStr, October 2026</p>
<p>Three humans and more than 20 AI agents. Two different agents recently destroyed critical data:</p>
<div class="card warn"><span class="hd">The pipeline</span>A third-party agent deletes nearly all of SaaStr&rsquo;s Salesforce sales pipeline minutes after it is deployed.</div>
<div class="card warn"><span class="hd">The file</span>Another agent replaces a core code file with the words &ldquo;DO IT,&rdquo; twice &mdash; then reports &ldquo;I did not make that edit.&rdquo;</div>
</div>
<div>
<p class="sub">What saved them</p>
<p>Both times, the data came back from copies nobody had set up as backups.</p>
<p class="sub">The new rule</p>
<div class="card"><span class="hd">&ldquo;If we can&rsquo;t name the independent copy, the agent doesn&rsquo;t get write access yet.&rdquo;</span></div>
<p class="punch">The lesson is not &ldquo;agents are bad.&rdquo; It is that experience alone does not protect you. Structure does.</p>
</div>
</div>

<p class="refs">Source: <a href="https://www.saastr.com/two-ai-agents-wiped-critical-data-at-saastr-both-times-a-copy-nobody-planned-is-what-saved-us-it-will-happen-to-you-too-plan-for-it/">SaaStr, Oct 27 2026</a></p>

{{% note %}}
- Published this week. The same leader, a year on, with far more experience of agents, still gets caught.
- The rule at the bottom is the best one-line governance control in the session. Write it on the board; we come back to it on Monday&rsquo;s checklist.
- Note the second agent: it acted, then denied acting. Same pattern as July 2025. An agent&rsquo;s report on its own behaviour is not evidence.
{{% /note %}}

***

<!-- 02 — Designing a system with agency -->
{{< slide class="fs55" >}}

### Why agents are different
# From a tool to a system with agency

<svg class="dg" viewBox="0 0 860 260" role="img" aria-label="Traditional software: human, system, output in a line. Agentic AI: a human sets an objective function, an agent loops between reasoning and acting, and its outputs cascade.">
<defs><marker id="a02g" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#777"/></marker><marker id="a02b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<text x="0" y="24" font-size="18" font-weight="700" fill="#555">Traditional software</text>
<g font-size="15" text-anchor="middle" fill="#333">
<rect x="0" y="108" width="74" height="44" rx="5" fill="#eee" stroke="#999"/><text x="37" y="135">Human</text>
<rect x="104" y="108" width="74" height="44" rx="5" fill="#eee" stroke="#999"/><text x="141" y="135">System</text>
<rect x="208" y="108" width="74" height="44" rx="5" fill="#eee" stroke="#999"/><text x="245" y="135">Output</text>
</g>
<line x1="74" y1="130" x2="102" y2="130" stroke="#777" stroke-width="3" marker-end="url(#a02g)"/>
<line x1="178" y1="130" x2="206" y2="130" stroke="#777" stroke-width="3" marker-end="url(#a02g)"/>
<text x="141" y="200" text-anchor="middle" font-size="14" fill="#555">The system is a static tool.</text>
<text x="141" y="220" text-anchor="middle" font-size="14" fill="#555">The human makes the decisions.</text>
<line x1="315" y1="10" x2="315" y2="250" stroke="#bbb" stroke-dasharray="4 4"/>
<text x="340" y="24" font-size="18" font-weight="700" fill="#003478">Agentic AI</text>
<circle cx="372" cy="132" r="32" fill="#fff" stroke="#003478" stroke-width="3"/>
<text x="372" y="137" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Human</text>
<line x1="404" y1="132" x2="432" y2="132" stroke="#003478" stroke-width="3" marker-end="url(#a02b)"/>
<rect x="436" y="106" width="110" height="52" rx="6" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<text x="491" y="128" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">Objective</text>
<text x="491" y="146" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">function</text>
<line x1="546" y1="132" x2="580" y2="132" stroke="#003478" stroke-width="3" marker-end="url(#a02b)"/>
<path d="M 592 105 A 55 55 0 0 1 688 105" fill="none" stroke="#003478" stroke-width="6" marker-end="url(#a02b)"/>
<path d="M 688 159 A 55 55 0 0 1 592 159" fill="none" stroke="#003478" stroke-width="6" marker-end="url(#a02b)"/>
<text x="640" y="130" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">Agent</text>
<text x="640" y="149" text-anchor="middle" font-size="13" fill="#555">reason / act</text>
<g stroke="#CC0000" stroke-width="2.5">
<line x1="700" y1="132" x2="820" y2="62"/><line x1="700" y1="132" x2="830" y2="97"/>
<line x1="700" y1="132" x2="835" y2="132"/><line x1="700" y1="132" x2="830" y2="167"/>
<line x1="700" y1="132" x2="820" y2="202"/>
</g>
<g fill="#CC0000"><circle cx="820" cy="62" r="5"/><circle cx="830" cy="97" r="5"/><circle cx="835" cy="132" r="5"/><circle cx="830" cy="167" r="5"/><circle cx="820" cy="202" r="5"/></g>
<text x="775" y="240" text-anchor="middle" font-size="14" font-weight="700" fill="#CC0000">Cascading outputs</text>
</svg>

<div class="cols3">
<div class="card"><span class="hd">The moral choice</span>Defining what the agent optimizes for is an ethical decision, not a technical one.</div>
<div class="card"><span class="hd">Emergent behavior</span>Behavior arises from interactions no one explicitly designed. You still own the risk.</div>
<div class="card warn"><span class="hd">The policy shift</span>Every deployed agent is a policy. It applies consistently, at scale, indefinitely.</div>
</div>

{{% note %}}
- Why agents change the problem. Traditional software: the human decides, the system executes. Agentic AI: the human sets an objective, and the agent decides how to pursue it.
- &ldquo;Defining what the agent optimizes for is an ethical decision, not a technical one.&rdquo; In the Replit case the objective was &ldquo;make the app work&rdquo; &mdash; and the freeze was a competing goal.
- Every deployed agent is a policy: it applies consistently, at scale, indefinitely.
{{% /note %}}

***

<!-- 03 — Machine speed amplifies harm -->
{{< slide class="fs55" >}}

### Why agents are different
# Machine speed turns isolated errors into systemic failures

<div class="g23">
<div>
<p>A biased decision a human makes once a day, an agent makes ten thousand times before anyone notices.</p>
<p>Add <span class="term">automation bias</span> &mdash; people trusting machine output without checking &mdash; and errors are not just faster. They are reinforced.</p>
</div>
<svg class="dg" viewBox="0 0 500 340" role="img" aria-label="Chart: human error rate grows slowly over time; agentic harm compounds and rises steeply.">
<defs><marker id="a03k" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#333"/></marker></defs>
<g stroke="#333" stroke-width="2"><line x1="50" y1="300" x2="485" y2="300" marker-end="url(#a03k)"/><line x1="50" y1="300" x2="50" y2="15" marker-end="url(#a03k)"/></g>
<text x="270" y="330" text-anchor="middle" font-size="16" fill="#333">Time</text>
<text x="22" y="160" text-anchor="middle" font-size="16" fill="#333" transform="rotate(-90 22 160)">Scale of impact</text>
<line x1="50" y1="286" x2="470" y2="256" stroke="#003478" stroke-width="3"/>
<text x="470" y="246" text-anchor="end" font-size="14" font-weight="700" fill="#003478">Human error rate</text>
<path d="M 50 289 C 270 286 380 240 455 30" fill="none" stroke="#CC0000" stroke-width="4"/>
<text x="440" y="24" text-anchor="end" font-size="14" font-weight="700" fill="#CC0000">Agentic cascading harm</text>
<g fill="none" stroke="#CC0000" opacity="0.6">
<circle cx="343" cy="211" r="5"/><circle cx="343" cy="211" r="10"/>
<circle cx="394" cy="155" r="9"/><circle cx="394" cy="155" r="17"/>
<circle cx="429" cy="94" r="14"/><circle cx="429" cy="94" r="26"/>
</g>
<text x="370" y="120" text-anchor="end" font-size="13" fill="#555">compounding failure,</text>
<text x="370" y="137" text-anchor="end" font-size="13" fill="#555">accelerated by automation bias</text>
<g fill="#003478"><circle cx="150" cy="279" r="5"/><circle cx="230" cy="273" r="5"/></g>
<text x="70" y="250" font-size="13" fill="#555">isolated, self-correcting mistakes</text>
</svg>
</div>

{{% note %}}
- Scale and speed. A mistake a human makes once a day, an agent makes thousands of times before anyone notices.
- Automation bias makes it worse: people stop checking output that is usually right.
{{% /note %}}

***

<!-- 04 — Real-world failures and successes -->
{{< slide class="fs55" >}}

### The diagnostic
# Real-world agentic outcomes, done right and done wrong

<table class="plain">
<thead><tr><th>Dimension</th><th>&#10003; Done right &mdash; bounded systems</th><th style="color:#CC0000;">&#9888; Done wrong &mdash; unconstrained systems</th></tr></thead>
<tbody>
<tr><td class="lv">Autonomy level</td><td>Calibrated to stakes and reversibility (<a href="https://marketsmedia.com/j-p-morgan-ai-trading-global/">JPMorgan LOXM</a>)</td><td>Applied uniformly regardless of consequence (<a href="https://www.statnews.com/?p=1089881">UnitedHealth</a>)</td></tr>
<tr><td class="lv">Human oversight</td><td>Meaningful escalation thresholds (<a href="https://www.symphonyai.com/news/bank-bahrain-kuwait-financial-crime-aml">Bank of Bahrain &amp; Kuwait AML</a>)</td><td>1.1B applications processed with zero review (<a href="https://www.proskauer.com/blog/ai-bias-lawsuit-against-workday-reaches-next-stage-as-court-grants-conditional-certification-of-adea-claim">Workday</a>)</td></tr>
<tr><td class="lv">Objective spec</td><td>Narrow, precisely defined goals</td><td>Broad financial metric with no ethical guardrails</td></tr>
<tr><td class="lv">Data handling</td><td>Strictly scoped to the specific task</td><td>1.6M patient records shared beyond scope (<a href="https://www.insideprivacy.com/health-privacy/uk-hospital-deepmind-trial-failed-to-comply-with-uk-data-protection-law/">DeepMind &amp; NHS</a>)</td></tr>
<tr><td class="lv">Governance timing</td><td>Built before deployment (<a href="https://www.mckinsey.com/capabilities/risk-and-resilience/our-insights/deploying-agentic-ai-with-safety-and-security-a-playbook-for-technology-leaders">McKinsey</a>)</td><td>Retrofitted after harm or legal action</td></tr>
<tr><td class="lv">Liability</td><td>Deployer accepted shared responsibility</td><td>Vendor rejected liability; <a href="https://www.maynardnexsen.com/publication-emerging-liability-for-ai-driven-hiring-tools-key-developments-in-mobley-v-workday-inc">the court disagreed</a></td></tr>
</tbody>
</table>

{{% note %}}
- Not every story is a failure. The left column shows the same six dimensions done right.
- Read across one row: the difference is rarely the model. It is autonomy calibrated to stakes, real oversight, scoped data, and governance built before deployment.
- Each row previews a section of today: autonomy and oversight (risk), governance timing (governance), liability (accountability).
{{% /note %}}

***

<!-- ===== SECTION: ETHICS ===== -->
{{< slide background-color="#003478" class="section" >}}

# Ethics

<p>What do we value &mdash; and what do we do when values collide?</p>

{{% note %}}
Ethics is where we establish that judgment is needed, not just a checklist.
{{% /note %}}

***

<!-- 01 — Ethical AI vs. Responsible AI -->
{{< slide class="fs55" >}}

### Ethics and responsibility
# Ethics sets the destination. Responsible AI is the vehicle.

<svg class="dg" viewBox="-40 0 900 310" role="img" aria-label="Five ethical principles define the destination; five operational practices are the vehicle that gets there.">
<defs><marker id="a01b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<polygon points="220,55 315,124 279,236 161,236 125,124" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<circle cx="220" cy="55" r="9" fill="#fff" stroke="#003478" stroke-width="3"/>
<circle cx="315" cy="124" r="9" fill="#fff" stroke="#003478" stroke-width="3"/>
<circle cx="279" cy="236" r="9" fill="#fff" stroke="#003478" stroke-width="3"/>
<circle cx="161" cy="236" r="9" fill="#fff" stroke="#003478" stroke-width="3"/>
<circle cx="125" cy="124" r="9" fill="#fff" stroke="#003478" stroke-width="3"/>
<text x="220" y="40" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Beneficence</text>
<text x="327" y="129" text-anchor="start" font-size="15" font-weight="700" fill="#003478">Explicability</text>
<text x="291" y="257" text-anchor="start" font-size="15" font-weight="700" fill="#003478">Justice</text>
<text x="149" y="257" text-anchor="end" font-size="15" font-weight="700" fill="#003478">Autonomy</text>
<text x="113" y="129" text-anchor="end" font-size="15" font-weight="700" fill="#003478">Non-maleficence</text>
<text x="220" y="152" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">Values</text>
<text x="220" y="300" text-anchor="middle" font-size="15" fill="#CC0000" font-weight="700">Ethical AI: the destination</text>
<line x1="420" y1="155" x2="505" y2="155" stroke="#003478" stroke-width="4" marker-end="url(#a01b)"/>
<text x="462" y="143" text-anchor="middle" font-size="13" fill="#555">specify</text>
<rect x="520" y="38" width="320" height="40" rx="6" fill="#f4f6f9" stroke="#003478" stroke-width="2"/><text x="680" y="64" text-anchor="middle" font-size="16" fill="#003478">Model cards</text>
<rect x="520" y="86" width="320" height="40" rx="6" fill="#f4f6f9" stroke="#003478" stroke-width="2"/><text x="680" y="112" text-anchor="middle" font-size="16" fill="#003478">Bias testing</text>
<rect x="520" y="134" width="320" height="40" rx="6" fill="#f4f6f9" stroke="#003478" stroke-width="2"/><text x="680" y="160" text-anchor="middle" font-size="16" fill="#003478">Human-in-the-loop</text>
<rect x="520" y="182" width="320" height="40" rx="6" fill="#f4f6f9" stroke="#003478" stroke-width="2"/><text x="680" y="208" text-anchor="middle" font-size="16" fill="#003478">Incident response</text>
<rect x="520" y="230" width="320" height="40" rx="6" fill="#f4f6f9" stroke="#003478" stroke-width="2"/><text x="680" y="256" text-anchor="middle" font-size="16" fill="#003478">Audit trails</text>
<text x="680" y="300" text-anchor="middle" font-size="15" fill="#CC0000" font-weight="700">Responsible AI: the vehicle</text>
</svg>

<p>A system can pass every operational audit and still produce unethical outcomes if its values are poorly specified. Strong ethical intentions without responsible-AI infrastructure never reach production. <strong>The strongest programs build both.</strong></p>

{{% note %}}
- Ethics sets the destination; responsible AI is the vehicle that gets you there.
- Both failure modes are real: a system can pass every operational audit and still produce unethical outcomes if the values were poorly specified. And strong values without infrastructure never reach production.
{{% /note %}}

***

<!-- Values conflict -->
{{< slide class="fs55" >}}

### Ethics
# Values conflict &mdash; that is the job

<div class="cols2">
<div>
<div class="card warn"><span class="hd">Fairness vs. fairness</span>When base rates differ between groups, a model cannot be equally calibrated <em>and</em> have equal error rates for every group. You must choose which definition of fair you will defend.</div>
<div class="card warn"><span class="hd">Transparency vs. intellectual property</span>Explaining how a decision was made can expose the model, the data and the business logic that are your competitive advantage.</div>
</div>
<div>
<div class="card warn"><span class="hd">Personalization vs. privacy</span>The more the system knows about a person, the more useful it is &mdash; and the more it can leak, combine or misuse.</div>
<div class="card warn"><span class="hd">Speed vs. safety</span>Every review gate costs time to market. Competitors who skip it ship first &mdash; until they don&rsquo;t.</div>
</div>
</div>

<p class="punch">A list of principles everyone agrees with is not ethics. Ethics starts when two of them point in different directions.</p>

{{% note %}}
- Most lectures list fairness, transparency, privacy and safety, and the room nods along. The learning is in the tensions.
- Fairness: the impossibility results (Kleinberg et al. 2016; Chouldechova 2017), made famous by the COMPAS recidivism debate. Calibration and equal false-positive rates cannot both hold when base rates differ. Someone in your organization will pick one, explicitly or by default.
- Amazon&rsquo;s recruiting model (scrapped 2018) learned to penalize r&eacute;sum&eacute;s that mentioned women&rsquo;s organizations &mdash; it was faithfully fair to biased history.
- Speed vs. safety connects directly to the Replit raise. Ask the room which side of that trade-off their company is on, honestly.
{{% /note %}}

***

<!-- 11 — Law is reactive; ethics anticipates harm -->
{{< slide class="fs55" >}}

### Ethics vs. compliance
# Law is reactive; ethics anticipates harm

<table class="plain">
<thead><tr><th>Domain</th><th>Current regulation</th><th>What ethicists demand</th></tr></thead>
<tbody>
<tr><td class="lv">Harm &amp; liability</td><td>EU AI Act: fines up to &euro;35M or 7% of global turnover</td><td class="hl">Contestability built in as a design right</td></tr>
<tr><td class="lv">Consent</td><td>Notice required (the user is informed)</td><td class="hl">Genuine opt-in for all high-stakes decisions</td></tr>
<tr><td class="lv">Bias &amp; design</td><td>Statistical testing required</td><td class="hl">Participatory design with affected communities</td></tr>
<tr><td class="lv">Agentic pipelines</td><td>Currently unaddressed</td><td class="hl">Liability tracked across multi-agent delegation chains</td></tr>
</tbody>
</table>

<div class="card" style="margin-top:0.9em;"><span class="hd">Insight</span>Regulation follows harm. A system designed to today&rsquo;s compliance minimum will be out of date when the next rules arrive.</div>

{{% note %}}
- Ethics vs. legal compliance. Compliance is the floor, set after harm has happened. Ethics asks what harm is coming.
- Point at the last row: multi-agent pipelines are currently unaddressed. If you are deploying agents, you are ahead of the law, and your own judgment is the only control.
{{% /note %}}

***

<!-- Case lens: Ethics -->
{{< slide class="fs60" >}}

### Case lens &mdash; Ethics
# Who carries the risk?

<div class="card"><span class="hd">Whose judgment failed?</span>Lemkin chose to experiment on real data. Replit marketed the tool as safe for this. Where does each party&rsquo;s responsibility start and stop?</div>
<div class="card"><span class="hd">Moving fast</span>Replit raised &#36;250 million and shipped a more autonomous agent right after the incident. Is that responsible &mdash; or just how competitive markets work?</div>

{{% note %}}
- About two to three minutes. Let the room disagree; there is no clean answer, which is the point.
- Push on &ldquo;real data in an experiment.&rdquo; Most pilots in the room&rsquo;s companies do exactly that, because synthetic data is a hassle.
- On moving fast: name the trade-off from the previous slide &mdash; speed vs. safety &mdash; and ask who in the room would have voted to delay the launch.
{{% /note %}}

***

<!-- ===== SECTION: PRINCIPLES ===== -->
{{< slide background-color="#003478" class="section" >}}

# Principles

<p>What do we commit to &mdash; and why it rarely reaches practice</p>

{{% note %}}
Principles turn values into commitments. The interesting question is why so few of them change anything.
{{% /note %}}

***

<!-- Core principles -->
{{< slide class="fs55" >}}

### Principles
# Five core principles

<p class="lead">As established in the EU&rsquo;s Ethics Guidelines for Trustworthy AI</p>

<div class="cols2">
<div>
<div class="card"><span class="hd">Beneficence</span>AI should actively benefit people and society &mdash; not merely avoid harm. The obligation is positive: to do good, not just to refrain from doing harm.</div>
<div class="card"><span class="hd">Non-maleficence</span>AI must not cause harm, including through inaction, unintended side effects, or emergent behavior. The classical medical principle &ldquo;do no harm&rdquo; extended to autonomous systems.</div>
<div class="card"><span class="hd">Autonomy</span>People can understand, contest and override AI decisions that affect them: informed consent, explanation, and a real override &mdash; the right to exercise control, not just to be told.</div>
</div>
<div>
<div class="card"><span class="hd">Justice</span>The benefits and burdens of AI should be distributed fairly across groups and geographies &mdash; both a fair process and fair outcomes.</div>
<div class="card"><span class="hd">Explicability</span>AI behavior must be understandable and auditable by each stakeholder at the right level. A patient, a clinician and a regulator need different explanations of the same decision; all three are legitimate.</div>
</div>
</div>

{{% note %}}
- These five are the common core; most corporate AI principles are a rewording of them.
- Ask: which of these did the Replit agent violate? Non-maleficence obviously. Autonomy &mdash; Lemkin&rsquo;s explicit instruction was overridden. Explicability &mdash; the agent&rsquo;s own explanation was false.
{{% /note %}}

***

<!-- Principles into practice -->
{{< slide class="fs55" >}}

### Principles
# Published everywhere, practiced rarely

<div class="cols2">
<div>
<p class="sub">Why principles stall</p>
<div class="card warn"><span class="hd">Nobody owns them</span>The principles live on the website; no executive&rsquo;s targets depend on them.</div>
<div class="card warn"><span class="hd">Too abstract to act on</span>&ldquo;Be fair&rdquo; does not tell a product manager what to ship on Tuesday.</div>
<div class="card warn"><span class="hd">No budget, no veto</span>If no one can stop a launch for violating a principle, it is a slogan.</div>
</div>
<div>
<p class="sub">Translating one principle</p>
<table class="plain">
<thead><tr><th></th><th>&ldquo;People can override AI decisions&rdquo;</th></tr></thead>
<tbody>
<tr><td class="lv">Product</td><td>Every automated decision shows an &ldquo;ask a person&rdquo; path</td></tr>
<tr><td class="lv">Process</td><td>Appeals answered by a named team within 48 hours</td></tr>
<tr><td class="lv">Business</td><td>Override rate is a KPI on the owner&rsquo;s dashboard</td></tr>
</tbody>
</table>
</div>
</div>

<p class="punch">A principle is in practice when it changes a product, process or business decision.</p>

{{% note %}}
- Hundreds of organizations have published AI principles; very few can point to a decision a principle changed. That gap is the subject of this slide.
- The table is the exercise: take one principle and ask what it changes in the product, in the process, and in how the business measures itself. If the answer is &ldquo;nothing,&rdquo; the principle is decoration.
- The numbers (48 hours, override rate) are illustrative. The point is that they are specific and someone is measured on them.
{{% /note %}}

***

<!-- Case lens: Principles -->
{{< slide class="fs60" >}}

### Case lens &mdash; Principles
# A rule is not a control

<div class="card warn"><span class="hd">The agent had a written ban &mdash; and the permissions to break it</span>&ldquo;No changes without permission&rdquo; was an instruction. Write access to production was a capability. When they conflicted, the capability won.</div>
<div class="card"><span class="hd">Competing goals</span>The agent was asked to make the app work <em>and</em> not to touch anything. Under pressure, it resolved the conflict on its own.</div>

<p class="punch">A principle the agent can technically violate is not a safeguard.</p>

<p class="refs">Source: <a href="https://www.cio.com/article/4230232/the-replit-case-an-agent-a-written-order-and-a-deleted-database.html">CIO &mdash; The real agent risk that Replit&rsquo;s database deletion revealed</a></p>

{{% note %}}
- This is the bridge from principles to governance. Last session&rsquo;s line: a limit written in a prompt is a request; a limit enforced in the tool is a control.
- Ask: how many of your company&rsquo;s AI principles are enforced by permissions, and how many by instructions?
{{% /note %}}

***

<!-- ===== SECTION: RISK ===== -->
{{< slide background-color="#003478" class="section" >}}

# Risk

<p>Where does it matter most?</p>

{{% note %}}
The step most programs skip, and the decision executives actually make: how much scrutiny does this use case deserve?
{{% /note %}}

***

<!-- Risk tiering -->
{{< slide class="fs55" >}}

### Risk
# Not every use case deserves the same scrutiny

<div class="cols2">
<div>
<p class="sub">Three questions set the tier</p>
<div class="card"><span class="hd">Stakes</span>What is the worst plausible outcome, and can it be reversed?</div>
<div class="card"><span class="hd">Autonomy</span>Does the system suggest, decide with a human, or act on its own?</div>
<div class="card"><span class="hd">Who is affected</span>Employees, customers, the public? Can they see the decision, and contest it?</div>
</div>
<div>
<p class="sub">Same company, two use cases</p>
<table class="plain">
<thead><tr><th></th><th>Marketing copy</th><th>Hiring screener</th></tr></thead>
<tbody>
<tr><td class="lv">Stakes</td><td>Embarrassment</td><td>Careers, discrimination law</td></tr>
<tr><td class="lv">Autonomy</td><td>Draft, human edits</td><td>Filters before a human looks</td></tr>
<tr><td class="lv">Affected</td><td>Brand</td><td>Applicants who never see it</td></tr>
<tr><td class="lv">Oversight</td><td>Light</td><td>Heavy</td></tr>
</tbody>
</table>
<p class="sub">The logic behind the major frameworks</p>
<p><strong>EU AI Act:</strong> unacceptable, high, limited, minimal risk &mdash; hiring, credit and education are high-risk.<br><strong>NIST AI RMF:</strong> Govern, Map, Measure, Manage &mdash; scrutiny proportional to risk.</p>
</div>
</div>

{{% note %}}
- Risk tiering is the logic behind most major frameworks, and it is a decision executives make. Uniform scrutiny either strangles the low-risk work or under-protects the high-risk work.
- EU AI Act: prohibited practices (social scoring), high-risk systems (Annex III: employment, credit, education, essential services) with conformity obligations, limited-risk systems with transparency duties (chatbots must say they are AI), and everything else.
- NIST AI Risk Management Framework 1.0: voluntary, US, organised around four functions. ISO/IEC 42001 is the certifiable management-system standard if someone asks.
- Agents push use cases up a tier: the autonomy question moves from &ldquo;suggests&rdquo; to &ldquo;acts.&rdquo;
{{% /note %}}

***

<!-- 06 — Risk-tier assessment -->
{{< slide class="fs55" >}}

### Risk
# Phase 1: tier the risk, stress-test the objective

<div class="cols2">
<div>
<div class="card"><span class="hd">Risk tier assessment</span>
<p class="chk">&#9744; What is the worst-case outcome?</p>
<p class="chk">&#9744; Is it reversible?</p>
<p class="chk">&#9744; Did the affected parties consent?</p>
<p class="chk">&#9744; Does it fall under regulation (e.g. the EU AI Act)?</p>
</div>
</div>
<div>
<div class="card"><span class="hd">The evil genie test</span>Write the objective function down explicitly. Then ask: <strong>if the agent achieved this objective perfectly, what is the worst thing that could happen?</strong></div>
<div class="card warn"><span class="hd">Example</span>An agent told to &ldquo;maximize customer retention at all costs&rdquo; will learn to manipulate vulnerable users. Find the flaw before anyone writes the code.</div>
</div>
</div>

{{% note %}}
- The four-question tier assessment, in the order a review board would ask them. Reversibility is the one people forget.
- The &ldquo;evil genie&rdquo; test: if the agent achieved its objective perfectly, what is the worst thing that could happen? For Replit, &ldquo;make the app work&rdquo; perfectly achieved could include rebuilding the database from scratch.
{{% /note %}}

***

<!-- ===== SECTION: GOVERNANCE ===== -->
{{< slide background-color="#003478" class="section" >}}

# Governance

<p>How do we make it routine? &mdash; before the fact</p>

{{% note %}}
Governance is everything that happens before a system is allowed to act: approvals, reviews, checkpoints.
{{% /note %}}

***

<!-- Governance vs accountability -->
{{< slide class="fs55" >}}

### Two different jobs
# Governance before, accountability after

<div class="cols2">
<div>
<p class="sub">Governance &mdash; before the fact</p>
<div class="card"><span class="hd">Who approves</span>A named body with the power to block a launch.</div>
<div class="card"><span class="hd">What gets reviewed</span>An inventory of every AI system, including the ones IT did not buy.</div>
<div class="card"><span class="hd">Risk tiers</span>Which tier gets which checks.</div>
<div class="card"><span class="hd">Lifecycle checkpoints</span>Before build, during development, before deployment, in production.</div>
</div>
<div>
<p class="sub">Accountability &mdash; after the fact</p>
<div class="card warn"><span class="hd">Who answers</span>A named owner when harm happens &mdash; not &ldquo;the agent.&rdquo;</div>
<div class="card warn"><span class="hd">Recourse</span>How affected people contest a decision and get it fixed.</div>
<div class="card warn"><span class="hd">Audit trail</span>An independent record of what the system did.</div>
<div class="card warn"><span class="hd">Incident response</span>Kill switch, recovery, disclosure &mdash; rehearsed.</div>
</div>
</div>

{{% note %}}
- The two overlap in most write-ups; keep them apart. A company can have excellent governance (every launch reviewed) and no accountability (no one answers when the reviewed system still fails), and vice versa.
- This section covers the left column; the next section covers the right.
{{% /note %}}

***

<!-- 05 — Governance pipeline -->
{{< slide class="fs55" >}}

### Governance
# Governance is a pipeline, not a checklist

<p class="lead">If your team thinks about governance only at deployment time, it is already too late. Build accountability into the workflow, the way you build in security and performance testing.</p>

<div class="pipe">
<div class="card"><span class="hd">Phase 1 &middot; Before build</span>Risk tiering and objective stress-testing<span class="gate">Gate: risk tier assigned</span></div>
<div class="arr">&#9654;</div>
<div class="card"><span class="hd">Phase 2 &middot; During development</span>Least-privilege access and escalation gates<span class="gate">Gate: access scoped</span></div>
<div class="arr">&#9654;</div>
<div class="card"><span class="hd">Phase 3 &middot; Pre-deploy</span>Confirmation gates and architecture review<span class="gate">Gate: review passed</span></div>
<div class="arr">&#9654;</div>
<div class="card warn"><span class="hd">Phase 4 &middot; Production</span>Tamper-proof telemetry and kill switches<span class="gate">Gate: alert and stop</span></div>
</div>

{{% note %}}
- Governance as a pipeline, not a checklist at the end. Four checkpoints: before build, during development, pre-deploy, production.
- If your team thinks about governance only at deployment time, they are already too late.
{{% /note %}}

***

<!-- 07 — Least privilege -->
{{< slide class="fs55" >}}

### Governance
# Phase 2: contain the blast radius with least privilege

<div class="g32">
<svg class="dg" viewBox="0 0 520 400" role="img" aria-label="Bad design: the agent holds read-write access to a production database, payment gateway, user data and admin API. Good design: the agent calls three read-only tools in one direction.">
<defs><marker id="a07r" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#CC0000"/></marker><marker id="a07b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<text x="260" y="20" text-anchor="middle" font-size="15" font-weight="700" fill="#CC0000">Over-permissioned: an uncontained blast radius</text>
<rect x="20" y="40" width="150" height="44" rx="6" fill="#fdecec" stroke="#CC0000" stroke-width="2"/><text x="95" y="67" text-anchor="middle" font-size="14" fill="#CC0000">Production DB (RW)</text><line x1="170" y1="78" x2="238" y2="163" stroke="#CC0000" stroke-width="4" marker-start="url(#a07r)" marker-end="url(#a07r)"/>
<rect x="340" y="40" width="170" height="44" rx="6" fill="#fdecec" stroke="#CC0000" stroke-width="2"/><text x="425" y="67" text-anchor="middle" font-size="14" fill="#CC0000">Payment gateway (RW)</text><line x1="350" y1="78" x2="282" y2="163" stroke="#CC0000" stroke-width="4" marker-start="url(#a07r)" marker-end="url(#a07r)"/>
<rect x="0" y="178" width="150" height="44" rx="6" fill="#fdecec" stroke="#CC0000" stroke-width="2"/><text x="75" y="205" text-anchor="middle" font-size="14" fill="#CC0000">User data (RW)</text><line x1="150" y1="200" x2="213" y2="200" stroke="#CC0000" stroke-width="4" marker-start="url(#a07r)" marker-end="url(#a07r)"/>
<rect x="370" y="178" width="150" height="44" rx="6" fill="#fdecec" stroke="#CC0000" stroke-width="2"/><text x="445" y="205" text-anchor="middle" font-size="14" fill="#CC0000">Admin API (RW)</text><line x1="370" y1="200" x2="307" y2="200" stroke="#CC0000" stroke-width="4" marker-start="url(#a07r)" marker-end="url(#a07r)"/>
<polygon points="305,200 282.5,161 237.5,161 215,200 237.5,239 282.5,239" fill="#fff" stroke="#003478" stroke-width="3"/>
<text x="260" y="206" text-anchor="middle" font-size="18" font-weight="700" fill="#003478">Agent</text>
<rect x="10" y="320" width="160" height="44" rx="6" fill="#dce6f3" stroke="#003478" stroke-width="2"/><text x="90" y="347" text-anchor="middle" font-size="14" fill="#003478">Read-only analytics (R)</text><line x1="245" y1="241" x2="110" y2="316" stroke="#003478" stroke-width="3" marker-end="url(#a07b)"/>
<rect x="180" y="320" width="160" height="44" rx="6" fill="#dce6f3" stroke="#003478" stroke-width="2"/><text x="260" y="347" text-anchor="middle" font-size="14" fill="#003478">Profile viewer (R)</text><line x1="260" y1="242" x2="260" y2="316" stroke="#003478" stroke-width="3" marker-end="url(#a07b)"/>
<rect x="350" y="320" width="160" height="44" rx="6" fill="#dce6f3" stroke="#003478" stroke-width="2"/><text x="430" y="347" text-anchor="middle" font-size="14" fill="#003478">Session logger (R)</text><line x1="275" y1="241" x2="410" y2="316" stroke="#003478" stroke-width="3" marker-end="url(#a07b)"/>
<text x="260" y="392" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Least privilege: one-way calls to approved tools</text>
</svg>
<div>
<div class="card"><span class="hd">Architectural rules</span>
<p class="chk">1. Separate credentials for each agent role.</p>
<p class="chk">2. No shared admin tokens.</p>
<p class="chk">3. An explicit list of approved tools.</p>
<p class="chk">4. Tamper-proof decision logs from day one: trace ID, inputs, tools called, outputs.</p>
</div>
<div class="card warn"><span class="hd">An ethical failure, not just a security one</span>An agent with write access to a production database it only needs to read is a design decision someone approved.</div>
</div>
</div>

{{% note %}}
- This is the Replit failure in one picture: an agent with read-write access to production when the task needed far less.
- &ldquo;An agent with write access to a production database when it only needs read access is an ethical, not just a security, failure.&rdquo;
- Rule 4 &mdash; immutable decision logging from day one &mdash; is what Lemkin did not have when the agent told him the data was gone.
{{% /note %}}

***

<!-- 08 — Escalation gates -->
{{< slide class="fs55" >}}

### Governance
# Phase 2: escalation gates that mean something

<p class="lead">Human-in-the-loop is not a checkbox. A reviewer clearing 500 decisions a day at 30 seconds each provides cover, not oversight. Before any irreversible action, the agent must pause.</p>

<svg class="dg" viewBox="0 0 860 350" role="img" aria-label="Theatrical oversight: a flood of decisions reaches one reviewer who rubber-stamps them. Meaningful gate: 90 percent of routine work proceeds automatically; the uncertain or irreversible 10 percent is forced to pause until a human approves with the full reasoning trace.">
<defs><marker id="a08g" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#888"/></marker><marker id="a08b" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker><marker id="a08r" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#CC0000"/></marker></defs>
<text x="0" y="18" font-size="16" font-weight="700" fill="#555">Theatrical oversight</text>
<g stroke="#999" stroke-width="3" fill="none">
<line x1="0" y1="45" x2="238" y2="62" marker-end="url(#a08g)"/>
<line x1="0" y1="70" x2="238" y2="70" marker-end="url(#a08g)"/>
<line x1="0" y1="95" x2="238" y2="78" marker-end="url(#a08g)"/>
<line x1="425" y1="70" x2="556" y2="70" marker-end="url(#a08g)"/>
</g>
<rect x="245" y="40" width="180" height="60" rx="6" fill="#eee" stroke="#999"/>
<text x="335" y="65" text-anchor="middle" font-size="15" font-weight="700" fill="#555">Reviewer</text>
<text x="335" y="86" text-anchor="middle" font-size="13" fill="#555">500 decisions a day</text>
<text x="490" y="58" text-anchor="middle" font-size="13" fill="#555">30 seconds each</text>
<g transform="rotate(-5 650 70)">
<rect x="565" y="45" width="170" height="50" rx="4" fill="none" stroke="#CC0000" stroke-width="3"/>
<text x="650" y="79" text-anchor="middle" font-size="24" font-weight="700" fill="#CC0000" letter-spacing="2">APPROVED</text>
</g>
<text x="750" y="110" font-size="13" fill="#555">automation bias</text>
<line x1="0" y1="140" x2="860" y2="140" stroke="#ddd"/>
<text x="0" y="172" font-size="16" font-weight="700" fill="#003478">Meaningful escalation gate</text>
<polygon points="100,255 80,220.4 40,220.4 20,255 40,289.6 80,289.6" fill="#dce6f3" stroke="#003478" stroke-width="3"/>
<text x="60" y="261" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">Agent</text>
<polyline points="100,245 160,205 832,205" fill="none" stroke="#003478" stroke-width="4" marker-end="url(#a08b)"/>
<text x="180" y="195" font-size="14" font-weight="700" fill="#003478">90% &#183; routine and reversible &#8594; processed automatically</text>
<polyline points="100,265 160,300 298,300" fill="none" stroke="#CC0000" stroke-width="4" marker-end="url(#a08r)"/>
<text x="165" y="345" font-size="14" font-weight="700" fill="#CC0000">10% &#183; uncertain or irreversible</text>
<rect x="302" y="275" width="140" height="50" rx="6" fill="#CC0000"/>
<text x="372" y="306" text-anchor="middle" font-size="16" font-weight="700" fill="#fff">&#128274; Forced pause</text>
<line x1="528" y1="300" x2="446" y2="300" stroke="#003478" stroke-width="3" marker-end="url(#a08b)"/>
<rect x="532" y="275" width="230" height="50" rx="6" fill="#fff" stroke="#003478" stroke-width="2"/>
<text x="647" y="296" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">A human unlocks it, with</text>
<text x="647" y="314" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">the full reasoning trace</text>
</svg>

{{% note %}}
- Human-in-the-loop is not a checkbox. A reviewer clearing 500 decisions a day provides cover, not oversight.
- The design: route the uncertain or irreversible 10% to a forced pause, with the reasoning attached. Deleting a database is the textbook irreversible action.
{{% /note %}}

***

<!-- 09 — Pre-deployment review -->
{{< slide class="fs55" >}}

### Governance
# Phase 3: pre-deployment review and kill switch

<table class="plain">
<thead><tr><th>Gate</th><th>Requirement</th><th>Pass criteria</th></tr></thead>
<tbody>
<tr><td class="lv">Objective audit</td><td>Specified in writing and stress-tested?</td><td>Document exists and has been reviewed</td></tr>
<tr><td class="lv">Least privilege</td><td>Blast-radius containment verified?</td><td>Security review passed</td></tr>
<tr><td class="lv">Logging</td><td>Every action logged with full context?</td><td>Log sample validated</td></tr>
<tr><td class="lv">Failure modes</td><td>Fallback behavior when uncertain?</td><td>Fallback documented</td></tr>
<tr><td class="lv">Rollback plan</td><td>Can the agent be disabled rapidly?</td><td>Kill switch tested in under 5 minutes</td></tr>
</tbody>
</table>

<div class="card warn" style="margin-top:0.9em;"><span class="hd">Gated</span>Failing any single item blocks production deployment. External red-teaming is mandatory for every high-risk tier.</div>

{{% note %}}
- The pre-deployment gate. Failing any single item blocks production. Note &ldquo;rollback plan: kill switch tested in under five minutes&rdquo; &mdash; tested, not documented.
- Add SaaStr&rsquo;s row: &ldquo;Can you name the independent copy?&rdquo;
{{% /note %}}

***

<!-- 10 — Enterprise oversight -->
{{< slide class="fs55" >}}

### Governance
# Enterprise oversight: shadow AI and the liability shift

<p class="lead">Agentic AI is no longer just an IT decision. Failures scale straight to board-level legal liability.</p>

<div class="cols2">
<div>
<div class="tier t1"><span class="hd">Board level &mdash; AI review board</span>Legal, HR and technology, with the power to block deployment</div>
<div class="up">&#9650;</div>
<div class="tier t2"><span class="hd">Management level &mdash; enterprise AI inventory</span>Shadow-AI mapping, risk tiers, kill switches</div>
<div class="up">&#9650;</div>
<div class="tier t3"><span class="hd">Team level &mdash; agent telemetry</span>Override rates, bias metrics</div>
</div>
<div>
<div class="card warn"><span class="hd">The liability shift</span>In <em>Mobley v. Workday</em>, a US court let claims proceed against the AI vendor as well as the employers using it. &ldquo;We&rsquo;re just using the vendor&rsquo;s software&rdquo; is no longer a defense.</div>
<div class="card"><span class="hd">Data governance</span>Agents combine datasets that were collected for unrelated purposes. Consent frameworks built for static systems must adapt to dynamic, multi-agent pipelines.</div>
</div>
</div>

{{% note %}}
- The roles: a board-level review body with power to block, a management-level inventory of every AI system including shadow AI, team-level telemetry.
- The inventory is where most companies fail first: they cannot list the agents running on their data.
- The liability box is the bridge to the next section: &ldquo;we&rsquo;re just using the vendor&rsquo;s software&rdquo; is no longer a defense.
{{% /note %}}

***

<!-- US state-level AI legislation (from the Intro to Generative AI deck, pptx slide 100) -->
{{< slide class="reg" >}}

<style>
/* reveal-robinson.css pads sections by 50px with box-sizing: content-box, which
   makes a section 1060px wide on a 960px stage and clips text off the right
   edge. Scoped to this slide so the rest of the deck is untouched. */
.reveal .slides section.reg { box-sizing: border-box; }
.reveal .slides section.reg h3 { color: #CC0000; margin-bottom: 0.1em; }
.reveal .slides section.reg h1 { margin-top: 0; }
.reveal .slides section.reg a { color: inherit; text-decoration: underline; text-decoration-thickness: 1px; text-underline-offset: 2px; }
</style>

### The Regulatory Landscape
# US State-Level AI Legislation

<div style="display:grid; grid-template-columns:1fr 1fr; gap:0 1.6em; font-size:0.52em; align-items:start;">
<div>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;"><a href="https://www.nysenate.gov/legislation/bills/2023/A8195">New York &mdash; Advanced AI Licensing Act (A 8195)</a>:</strong> Requires developers and operators of certain &ldquo;high-risk advanced AI&rdquo; to obtain a licence. Related bills, such as an amendment in the Illinois legislature (<a href="https://www.ilga.gov/Legislation/BillStatus?DocNum=1002&amp;GAID=17&amp;DocTypeID=HB&amp;SessionID=112">HB 1002</a>), require state certification for the use of diagnostic algorithms.</p>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;"><a href="https://webserver.rilegislature.gov/BillText23/HouseText23/H6286.pdf">Rhode Island (H 6286)</a>:</strong> Mandates a &ldquo;distinctive watermark&rdquo; to authenticate content generated by generative AI.</p>
<p style="margin:0;"><strong style="color:#CC0000;"><a href="https://lims.dccouncil.gov/Legislation/B25-0114">District of Columbia &mdash; Stop Discrimination by Algorithms Act (B 114)</a>:</strong> Requires notice about how AI is used in employment, including the source of information, and a separate notice to individuals affected by algorithmic eligibility determinations.</p>
</div>
<div>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;"><a href="https://malegislature.gov/Bills/193/H1873">Massachusetts &mdash; Act Preventing a Dystopian Work Environment (HB 1873)</a>:</strong> Requires employers or vendors using AI to provide specific notices.</p>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;"><a href="https://app.leg.wa.gov/billsummary?BillNumber=1951&amp;Year=2023">Washington (HB 1951)</a>:</strong> Requires developers of automated decision tools to disclose to deployers the types of data used to program or train the tool, and how the tool was evaluated for validity.</p>
<p style="margin:0;"><strong style="color:#CC0000;"><a href="https://leginfo.legislature.ca.gov/faces/billNavClient.xhtml?bill_id=202320240AB331">California (AB 331)</a> and <a href="https://www.nysenate.gov/legislation/bills/2023/A7859">New York (AB 7859)</a>:</strong> Bills that would require AI deployers to allow individuals to opt out of decisions based on automated decision-making.</p>
</div>
</div>

<p style="font-size:0.42em; color:#777; margin-top:1em;">Bill status reflects the 2023&ndash;2024 legislative sessions and will have moved since &mdash; verify current status before relying on any single item.</p>

{{% note %}}
- No single federal AI statute, so compliance is state by state — for a multi-state employer that is the whole problem in one sentence.
- Notice the recurring obligations rather than the bill numbers: **licensing** for high-risk systems, **watermarking** of generated content, **notice** to affected individuals, **disclosure** of training data, and a **right to opt out** of automated decisions.
- Build for the strictest jurisdiction you operate in; retrofitting notice and opt-out later is far more expensive.
- These were pending bills in the 2023–24 sessions. Check current status before advising anyone — several have since changed.
{{% /note %}}

***
<!-- EU AI Act vs. the US approach -->
{{< slide class="fs50" >}}

### The Regulatory Landscape
# EU AI Act vs. the US approach

<p class="lead">One binding, risk-tiered law &mdash; versus voluntary standards plus a patchwork of federal guidance and state laws.</p>

<table class="plain">
<thead><tr><th></th><th><a href="https://eur-lex.europa.eu/eli/reg/2024/1689/oj">EU AI Act</a></th><th>US approach &mdash; <a href="https://www.nist.gov/itl/ai-risk-management-framework">NIST AI RMF</a>, federal and state rules</th></tr></thead>
<tbody>
<tr><td class="lv">Legal nature</td><td>Binding regulation in every EU member state &mdash; and for non-EU companies whose AI is used in the EU</td><td>Voluntary framework (NIST) plus executive orders, agency procurement rules and state laws</td></tr>
<tr><td class="lv">Enforcement</td><td>Fines up to &euro;35M or 7% of global annual turnover</td><td>No single federal penalty regime; liability runs through tort law, consumer protection (FTC) and sector rules</td></tr>
<tr><td class="lv">Risk classification</td><td>Four tiers: unacceptable (banned), high (conformity assessment, human oversight), limited (transparency), minimal</td><td>Principles-based: NIST&rsquo;s Govern, Map, Measure, Manage, adapted to each use case</td></tr>
<tr><td class="lv">Documentation</td><td>Prescriptive for high-risk systems: data provenance, accuracy, architecture, logs</td><td>Flexible, set by each organization&rsquo;s own risk tolerance</td></tr>
<tr><td class="lv">Prohibited practices</td><td>Bans social scoring, most real-time biometric identification in public, and emotion recognition at work and school</td><td>No blanket federal ban; some states and agencies restrict specific uses such as facial recognition</td></tr>
</tbody>
</table>

<p class="refs">Sources: <a href="https://eur-lex.europa.eu/eli/reg/2024/1689/oj">EU AI Act, Regulation (EU) 2024/1689</a> &middot; <a href="https://artificialintelligenceact.eu/high-level-summary/">AI Act high-level summary</a> &middot; <a href="https://www.nist.gov/itl/ai-risk-management-framework">NIST AI RMF</a> &middot; <a href="https://www.eccouncil.org/cybersecurity-exchange/responsible-ai-governance/eu-ai-act-nist-ai-rmf-and-iso-iec-42001-a-plain-english-comparison/">EC-Council comparison</a> &middot; <a href="https://en.wikipedia.org/wiki/Regulation_of_artificial_intelligence_in_the_United_States">AI regulation in the US (Wikipedia)</a></p>

{{% note %}}
- The one-line contrast: the EU wrote a single binding law organized by risk tier; the US relies on a voluntary standard (NIST) and lets federal agencies, courts and states fill in.
- **Extraterritorial reach** is the row executives miss. A US company whose AI output is used in the EU is in scope &mdash; the same pattern as GDPR.
- &ldquo;Voluntary&rdquo; is softer than it sounds. Federal agencies write NIST into procurement criteria, Texas treats NIST compliance as an affirmative defense, Colorado requires risk-management programs aligned with frameworks like it, and courts increasingly look to NIST as the baseline for reasonable care.
- Practical advice: if you operate in both markets, design to the EU high-risk requirements and map them to NIST; the reverse does not work.
{{% /note %}}

***


<!-- Case lens: Governance -->
{{< slide class="fs60" >}}

### Case lens &mdash; Governance
# Separation of duties

<div class="card warn"><span class="hd">One actor, three roles</span>The agent acted, reported on what it did, and supplied the only explanation. In finance, the person who makes a payment never also audits it.</div>
<div class="card"><span class="hd">What would have changed the outcome?</span>Independent logs the agent cannot edit. Read-only access by default. Recovery tested without the agent&rsquo;s help.</div>

{{% note %}}
- Two to three minutes. Walk the three controls against the timeline: with any one of them, day nine is an inconvenience, not a crisis.
- Separation of duties is a centuries-old control. Executives already understand it from finance; the move is to apply it to agents.
{{% /note %}}

***

<!-- ===== SECTION: ACCOUNTABILITY ===== -->
{{< slide background-color="#003478" class="section" >}}

# Accountability

<p>Who answers? &mdash; after the fact</p>

{{% note %}}
The part executives personally own.
{{% /note %}}

***

<!-- Accountability -->
{{< slide class="fs55" >}}

### Accountability
# &ldquo;The agent did it&rdquo; is not an answer

<div class="cols2">
<div>
<div class="card"><span class="hd">Named owners</span>Every agent has a human owner who can be named in a meeting and in a filing.</div>
<div class="card"><span class="hd">Human oversight</span>Someone with the authority and the time to overrule the system.</div>
<div class="card"><span class="hd">Recourse</span>Affected people can see that a decision was automated, contest it, and get it corrected.</div>
<div class="card"><span class="hd">Incident response</span>A rehearsed plan: stop, recover, investigate, disclose.</div>
</div>
<div>
<p class="sub">The courts agree</p>
<div class="card warn"><span class="hd">Moffatt v. Air Canada (2024)</span>Air Canada argued its chatbot was responsible for its own wrong refund advice. The tribunal held the airline liable for everything on its website, chatbot included.</div>
<div class="card warn"><span class="hd">Mobley v. Workday</span>A US court let discrimination claims proceed against the vendor of an AI screening tool, not only the employers using it.</div>
</div>
</div>

{{% note %}}
- Agents make accountability much harder: many steps, many vendors, no single human decision to point to. That is exactly why it must be assigned in advance.
- Air Canada is the cleanest line for executives: the company tried to treat the chatbot as a separate entity and lost. Your agent&rsquo;s output is your output.
- Workday: liability can reach the vendor too. Deployers and vendors share it; neither escapes it.
{{% /note %}}

***

<!-- 13 — Interlocking accountability framework -->
{{< slide class="fs55" >}}

### Accountability
# The interlocking accountability framework

<svg class="dg" style="width:90%; margin-left:auto; margin-right:auto;" viewBox="0 0 860 380" role="img" aria-label="Three concentric rings: technical governance at the core, enterprise oversight around it, global regulation outside. A failure at the core radiates outward through every ring.">
<defs><marker id="a13r" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#CC0000"/></marker></defs>
<circle cx="520" cy="190" r="170" fill="none" stroke="#CC0000" stroke-width="26"/>
<circle cx="520" cy="190" r="125" fill="none" stroke="#003478" stroke-width="30"/>
<circle cx="520" cy="190" r="82" fill="#dce6f3"/>
<text x="520" y="186" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Technical</text>
<text x="520" y="205" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">core</text>
<g stroke="#555" stroke-width="1.5"><line x1="290" y1="56" x2="400" y2="70"/><line x1="290" y1="186" x2="395" y2="190"/><line x1="290" y1="316" x2="463" y2="247"/></g>
<g font-size="15">
<text x="285" y="52" text-anchor="end" font-weight="700" fill="#CC0000">Global regulation</text>
<text x="285" y="71" text-anchor="end" fill="#555">EU AI Act, civil-rights law, societal impact</text>
<text x="285" y="182" text-anchor="end" font-weight="700" fill="#003478">Enterprise oversight</text>
<text x="285" y="201" text-anchor="end" fill="#555">AI inventory, review boards, due diligence</text>
<text x="285" y="312" text-anchor="end" font-weight="700" fill="#003478">Technical governance</text>
<text x="285" y="331" text-anchor="end" fill="#555">logs, least privilege, confirmation gates</text>
</g>
<polyline points="565,172 600,150 585,140 690,48" fill="none" stroke="#CC0000" stroke-width="5" stroke-linejoin="round" marker-end="url(#a13r)"/>
<rect x="700" y="10" width="158" height="80" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<g font-size="13" font-weight="700" fill="#CC0000" text-anchor="middle">
<text x="779" y="35">A failure at the core</text><text x="779" y="54">radiates out through</text><text x="779" y="73">every ring</text>
</g>
</svg>

<p>Ethical governance is not a constraint bolted onto AI; it is load-bearing structure. Responsibility is engineered in the code, overseen by the enterprise, and aligned with regulation.</p>

{{% note %}}
- Technical controls at the core, enterprise oversight around them, regulation outside. A failure at the core radiates outward.
- The accountability question is who stands at each ring when it does.
{{% /note %}}

***

<!-- Case lens: Accountability -->
{{< slide class="fs60" >}}

### Case lens &mdash; Accountability
# Who answers?

<div class="card"><span class="hd">Three candidates</span>Replit, which built and marketed the agent? The model provider behind it? Or Lemkin, who deployed it on real data?</div>
<div class="card warn"><span class="hd">The anonymous vendor</span>In the Salesforce incident, SaaStr kept the third-party vendor anonymous. What does that do to accountability across the market?</div>

{{% note %}}
- Two to three minutes. The honest answer today is &ldquo;all three, in proportions nobody has settled.&rdquo; Contracts and courts are deciding it case by case.
- The anonymity question is subtle: protecting a vendor relationship is reasonable for one company, but if no one names vendors, the market cannot learn which agents are unsafe.
- Optional advanced case if time allows (verify the details and source before using): OpenAI disclosed in July 2026 that some of its agents broke out of a test environment into Hugging Face&rsquo;s systems to cheat on a cybersecurity test; Hugging Face asked for compute rather than suing; legal experts disagree on whether anyone is liable. It is a frontier lab testing its own agents, so it fits less well than Replit for the breakouts.
{{% /note %}}

***

<!-- 12 — Unsolved frontiers -->
{{< slide class="fs55" >}}

### Accountability
# The unsolved frontiers

<p class="lead">Open problems in research and in the market.</p>

<div class="cols3 eq">
<div class="card"><span class="hd">1. Formal verification</span>Proving that safety rules hold everywhere within an agent&rsquo;s bounded autonomy. Moving the industry from &ldquo;we believe it is safe&rdquo; to &ldquo;we can demonstrate it is safe.&rdquo;</div>
<div class="card"><span class="hd">2. Agentic audit infrastructure</span>Standardized, tamper-evident records of how agents reasoned and handed off work. Going beyond flat logs to answer exactly which data contributed to an automated decision.</div>
<div class="card"><span class="hd">3. Mechanistic interpretability</span>Tracing harmful outcomes back to individual agent decisions and data inputs inside complex, collaborating multi-agent pipelines.</div>
</div>

{{% note %}}
- Where the field is still open. Frontier 2 &mdash; tamper-evident audit infrastructure for multi-agent systems &mdash; is the accountability problem from the case, unsolved at industry scale.
{{% /note %}}

***

<!-- ===== SECTION: CLOSE ===== -->
{{< slide background-color="#003478" class="section" >}}

# What Do I Do Monday?

<p>From the case to your own agents</p>

{{% note %}}
About five minutes on the bridge, then the teams break out.
{{% /note %}}

***

<!-- Leader's checklist -->
{{< slide class="fs55" >}}

### Close
# A leader&rsquo;s checklist for Monday

<div class="cols2">
<div>
<div class="card"><span class="hd">1. List every agent</span>Including the ones a team switched on without asking. Each gets a named owner.</div>
<div class="card"><span class="hd">2. Tier each one</span>Stakes, autonomy, who is affected. Scrutiny follows the tier.</div>
<div class="card"><span class="hd">3. Name the independent copy</span>No copy you can name, no write access.</div>
<div class="card"><span class="hd">4. Enforce limits in permissions</span>Not in prompts. Read-only by default.</div>
</div>
<div>
<div class="card"><span class="hd">5. Separate actor and auditor</span>Logs the agent cannot edit; never take the agent&rsquo;s word for what it did.</div>
<div class="card"><span class="hd">6. Test the off switch</span>Kill switch and recovery, rehearsed without the agent&rsquo;s help.</div>
<div class="card"><span class="hd">7. Name who answers</span>And how affected people get recourse &mdash; before the incident.</div>
<div class="card warn"><span class="hd">8. Pick your trade-offs on purpose</span>Write down which value wins when two collide, and who decided.</div>
</div>
</div>

{{% note %}}
- Every item maps back to a section: 1&ndash;2 risk, 3&ndash;6 governance, 7 accountability, 8 ethics.
- If students remember one item, make it number 3 &mdash; it is a sentence they can say in a meeting on Monday.
{{% /note %}}

***

<!-- Bridge to team breakouts -->
{{< slide class="fs55" >}}

### Team breakouts
# Where could your agent do what Replit&rsquo;s did?

<table class="plain">
<thead><tr><th>Team</th><th>Question from the case</th></tr></thead>
<tbody>
<tr><td class="lv">1 &mdash; Student chatbot</td><td>Do your agents have write access to university databases? If one sends a wrong email about a student hold, what independent record shows what it did?</td></tr>
<tr><td class="lv">2 &mdash; Patient Care Flag</td><td>&ldquo;No agent can order or change therapy&rdquo;: is that enforced by permissions or only by instructions? Can an agent alter its own audit log?</td></tr>
<tr><td class="lv">3 &mdash; Emerald intake</td><td>The connector writes into Rosemark, your single system of record. If it overwrites good data, where is the independent copy?</td></tr>
<tr><td class="lv">4 &mdash; Auto lending</td><td>You already hold untrusted documents apart from instructions and keep an append-only log. In phase 3 auto-approval, who checks the agent&rsquo;s own summary of what it did?</td></tr>
</tbody>
</table>

{{% note %}}
- Teams 2 and 4 already mostly limit their agents through permissions: no order-entry tool, no funding tool. Teams 1 and 3 mostly rely on stated rules.
- Do not announce that contrast; let it come out in the report-back. It is the &ldquo;a rule is not a control&rdquo; lesson, found in their own designs.
{{% /note %}}

***

<!-- Group activity: roles -->
{{< slide class="fs55" >}}

### Team breakouts
# How the review works

<p class="lead">One person defends the design; everyone else tests it.</p>

<div class="cols2 eq">
<div class="card"><span class="hd">Advocate</span>
<ul>
<li>Explain the project in 3 minutes: the problem, what the agent does, who it affects, and the safeguards the team designed.</li>
<li>Answer questions and defend the design where you think it holds up.</li>
<li>When a critique is fair, say so.</li>
</ul></div>
<div class="card warn"><span class="hd">Reviewers</span>
<ul>
<li>Test the design. Ask &ldquo;how do you know?&rdquo; and &ldquo;what happens if?&rdquo;</li>
<li>Push for specifics.</li>
<li>Pick one reviewer as timekeeper so the group reaches every lens.</li>
</ul></div>
</div>

<p class="punch">Work through five lenses in order: Ethics &rarr; Principles &rarr; Risk &rarr; Governance &rarr; Accountability.</p>

{{% note %}}
- The lenses follow the order of today&rsquo;s sections, so each one recalls a part of the session.
- The advocate should concede fair points; the goal is a better design, not winning the argument.
{{% /note %}}

***

<!-- Group activity: lenses 1-3 -->
{{< slide class="fs50" >}}

### Team breakouts
# The five lenses (1&ndash;3)

<div class="cols3 eq">
<div class="card"><span class="hd">1. Ethics: whose interests are at stake?</span>
<ul>
<li>Who benefits from this project, and who bears the risk? Are they the same people?</li>
<li>Name the most important tension between values, such as efficiency vs. care, speed vs. fairness, or revenue vs. client interest.</li>
<li>Is anyone affected who has little power to object or opt out?</li>
</ul></div>
<div class="card"><span class="hd">2. Principles: what is committed, and is it enforced?</span>
<ul>
<li>Which principles does the project claim, such as fairness, privacy, transparency, human oversight or safety?</li>
<li>For each one: is it enforced by a technical control, or only stated as an instruction? <em>Replit: the agent was told not to touch the database and still had permission to delete it.</em></li>
<li>Which important principle is missing or not measured?</li>
</ul></div>
<div class="card"><span class="hd">3. Risk: how much could go wrong, and for whom?</span>
<ul>
<li>What&rsquo;s the worst realistic failure? Be concrete: who is harmed, how badly, and can it be undone?</li>
<li>How autonomous is the agent? Does it advise, draft, or act?</li>
<li>Rate the project low, medium or high risk, and justify the rating.</li>
</ul></div>
</div>

{{% note %}}
- Lens 2 is where most designs are weakest: a stated rule is not a control.
- Make teams commit to a risk rating in lens 3; lens 4 tests governance against it.
{{% /note %}}

***

<!-- Group activity: lenses 4-5 -->
{{< slide class="fs50" >}}

### Team breakouts
# The five lenses (4&ndash;5)

<div class="cols2 eq">
<div class="card"><span class="hd">4. Governance: how is responsible behavior made routine?</span>
<ul>
<li>What checkpoints, approvals, reviews and stop conditions does the plan include?</li>
<li>Is the governance proportional to the risk rating you just gave? Too much, too little, or about right?</li>
<li>What one control would you add? Consider read-only access by default, logs the agent can&rsquo;t modify, an independent backup, or a second system checking outputs.</li>
</ul></div>
<div class="card"><span class="hd">5. Accountability: who answers when it goes wrong?</span>
<ul>
<li>Name the person who is accountable, not just a department.</li>
<li>If the agent makes a harmful mistake, how is it detected, and by whom? <em>Replit: the agent was also the one reporting on its own actions.</em></li>
<li>How does an affected person (a student, patient, client or borrower) find out, challenge the outcome and get it corrected?</li>
<li>Is &ldquo;a human reviews every decision&rdquo; meaningful oversight in this design, or could it become a formality?</li>
</ul></div>
</div>

{{% note %}}
- Governance is before the fact; accountability is after the fact. Lens 4 asks what prevents harm, lens 5 asks what happens once it occurs.
{{% /note %}}

***

<!-- Group activity: starting questions -->
{{< slide class="fs55" >}}

### Team breakouts
# Starting question for each group

<table class="plain">
<thead><tr><th>Team</th><th>Open with this</th></tr></thead>
<tbody>
<tr><td class="lv">Student Chatbot</td><td>The bot touches health and financial aid data. What is the legal and ethical basis for that access, and who besides IT owns the risk?</td></tr>
<tr><td class="lv">Patient Care Flag</td><td>Later clinics serve as the comparison group. Is it acceptable for high-risk patients to wait for a tool you expect to help them?</td></tr>
<tr><td class="lv">Emerald Intake</td><td>At a 60-person company, what does real governance look like when one person may hold three roles?</td></tr>
<tr><td class="lv">Auto Lending</td><td>Faster approvals raise conversion. Does that serve subprime borrowers, or mainly the lender and the dealer?</td></tr>
</tbody>
</table>

{{% note %}}
- Each question is an ethics question first, chosen to start the group on lens 1.
{{% /note %}}

***

<!-- Group activity: exit check -->
{{< slide class="fs55" >}}

### Team breakouts
# Before you leave the group

<p class="lead">Make sure each of you can answer these individually.</p>

<div class="card"><span class="hd">1. Tension and risk</span>What was the most important ethical tension and risk?</div>
<div class="card"><span class="hd">2. Weakest principle</span>Which principle was weakest, and what control would fix it?</div>
<div class="card warn"><span class="hd">3. Accountability and recommendation</span>Who is accountable, what is your group&rsquo;s recommendation, and where did the advocate push back?</div>

{{% note %}}
- These three questions drive the report-back; call on individuals, not the advocate.
{{% /note %}}






