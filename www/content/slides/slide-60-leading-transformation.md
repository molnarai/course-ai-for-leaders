+++
title = "Leading AI Transformation"
description = "Goal, readiness, path: start with a business outcome, assess readiness along three pillars, and lead the change through a sequence of nimble, owned, measured steps"
weight = 60
outputs = ["Reveal"]
math = false
thumbnail = "/imgs/slides/AI_Transformation_3-Step_Framework_thumb.jpg"

[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"

+++

<!--
    Slide deck: Leading AI Transformation.
    Source: content/blog/leading-business-transformation.md

    Spine: Why it stalls -> Step 1 Goal -> Step 2 Readiness (three pillars)
           -> Step 3 Path of nimble steps -> Worked example -> Leader's job -> Project.

    Diagram-first: most slides are a single inline SVG with notes carrying the talk track.
    Keep blank lines out of <svg> blocks: Markdown ends an HTML block at one.
    Palette follows reveal-robinson.css: GSU Blue #003478, GSU Crimson #CC0000.
    Crimson is reserved for blockers, failures and warnings.
-->

<style>
.reveal .slides section { box-sizing: border-box; }
.reveal .slides section.fs60 { font-size: 0.60em; }
.reveal .slides section.fs55 { font-size: 0.55em; }
.reveal .slides section.fs50 { font-size: 0.50em; }
.reveal .slides section[class*="fs"] h1 { font-size: 48px; margin-bottom: 0.3em; }
.reveal .slides section[class*="fs"] h3 { color: #CC0000; font-size: 24px; margin-bottom: 0.1em; }
.reveal svg.dg { width: 100%; height: auto; display: block; margin: 0.2em 0 0.4em 0; }
.reveal svg.dg text { font-family: inherit; }
.reveal .lead { font-style: italic; color: #555; margin-bottom: 0.5em; }
.reveal .refs { font-size: 0.62em; color: #777; margin-top: 0.4em; }
.reveal .refs a { color: #777; }
.reveal .punch { color: #003478; font-weight: 700; margin-top: 0.4em; }
.reveal .slides section.section { text-align: center; }
.reveal .slides section.section h1 { color: #fff; font-size: 2.3em; margin: 0; }
.reveal .slides section.section p { color: #c9d6e8; font-size: 0.66em; margin-top: 0.7em; }
.reveal .slides section.section h3 { color: #c9d6e8; font-size: 0.8em; }
.reveal:has(.slides section.section.present) .slide-footer img { filter: brightness(0) invert(1); }
.reveal:has(.slides section.section.present) .slide-number { color: #EDEEEF; }
</style>

<!-- ===== TITLE ===== -->
{{< slide background-color="#003478" class="section" >}}

# Leading AI Transformation

<p style="font-size:0.9em; color:#fff;">Goal &middot; Readiness &middot; Path</p>

<p>EMBA 8160 &mdash; AI for Leaders</p>

{{% note %}}
- Most AI initiatives do not fail because the technology is weak. They stall because nobody agreed on what they were for, the organization was not ready, or the team leapt from a demo to enterprise scale.
- Today: a three-step discipline a leader can own. Start with the goal, assess readiness along three pillars, chart a path of nimble steps.
{{% /note %}}

***

<!-- Adoption is not impact -->
{{< slide class="fs55" >}}

### Why this matters
# AI is everywhere. Impact is not.

<svg class="dg" viewBox="0 0 860 330" role="img" aria-label="Two bars. Only 21 percent of organizations using gen AI have fundamentally redesigned some workflows. Only 23.6 percent of small and mid-sized firms using gen AI say any of their staff have had AI training.">
<text x="0" y="40" font-size="19" font-weight="700" fill="#003478">Organizations using gen AI that have fundamentally redesigned at least some workflows</text>
<rect x="0" y="58" width="760" height="54" rx="6" fill="#eef1f5"/>
<rect x="0" y="58" width="160" height="54" rx="6" fill="#003478"/>
<text x="175" y="96" font-size="30" font-weight="700" fill="#003478">21%</text>
<text x="0" y="138" font-size="15" fill="#555">McKinsey, State of AI, March 2025. Yet workflow redesign was the attribute most strongly associated with reported EBIT impact.</text>
<text x="0" y="205" font-size="19" font-weight="700" fill="#003478">Small and mid-sized firms using gen AI whose staff have had <tspan font-style="italic">any</tspan> AI training</text>
<rect x="0" y="223" width="760" height="54" rx="6" fill="#eef1f5"/>
<rect x="0" y="223" width="179" height="54" rx="6" fill="#CC0000"/>
<text x="194" y="261" font-size="30" font-weight="700" fill="#CC0000">23.6%</text>
<text x="0" y="303" font-size="15" fill="#555">OECD, Generative AI and the SME Workforce, November 2025. Adoption is running ahead of preparation.</text>
</svg>

<p class="punch">Distributing tools is not the same as changing how work gets done.</p>

<p class="refs">Sources: <a href="https://www.mckinsey.com/~/media/mckinsey/business%20functions/quantumblack/our%20insights/the%20state%20of%20ai/march%202025/the-state-of-ai-how-organizations-are-rewiring-to-capture-value_final.pdf">McKinsey 2025</a> &middot; <a href="https://www.oecd.org/en/publications/generative-ai-and-the-sme-workforce_2d08b99d-en/full-report/component-6.html">OECD 2025</a></p>

{{% note %}}
- Two numbers, two different populations. Keep them separate: one is a global management survey, the other is SMEs.
- The McKinsey finding is an association, not proof of causation. But it points at something leaders control: changing the work, not just handing out licenses.
- The OECD number says many organizations are already using AI without having built the capability to use it responsibly.
{{% /note %}}

***

<!-- Four ways transformations stall -->
{{< slide class="fs55" >}}

### Why this matters
# Four ways AI transformations stall

<svg class="dg" viewBox="0 0 860 410" role="img" aria-label="Four failure patterns: tool-first thinking, the wrong diagnosis, pilot purgatory, and big-bang plans.">
<defs><marker id="a03" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="10" markerHeight="10" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker><marker id="a03r" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="10" markerHeight="10" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#CC0000"/></marker></defs>
<rect x="0" y="0" width="420" height="195" rx="10" fill="#f4f6f9"/>
<rect x="440" y="0" width="420" height="195" rx="10" fill="#f4f6f9"/>
<rect x="0" y="215" width="420" height="195" rx="10" fill="#f4f6f9"/>
<rect x="440" y="215" width="420" height="195" rx="10" fill="#f4f6f9"/>
<text x="20" y="32" font-size="20" font-weight="700" fill="#003478">Tool-first thinking</text>
<rect x="30" y="60" width="110" height="46" rx="6" fill="#003478"/>
<text x="85" y="89" text-anchor="middle" font-size="16" fill="#fff">Licenses</text>
<line x1="140" y1="83" x2="262" y2="83" stroke="#003478" stroke-width="3" marker-end="url(#a03)"/>
<rect x="270" y="60" width="110" height="46" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2" stroke-dasharray="6 4"/>
<text x="325" y="90" text-anchor="middle" font-size="24" font-weight="700" fill="#CC0000">?</text>
<text x="325" y="125" text-anchor="middle" font-size="13" fill="#555">the problem</text>
<text x="20" y="168" font-size="15" fill="#555">Access is rolled out first; the problem is found later.</text>
<text x="460" y="32" font-size="20" font-weight="700" fill="#003478">The wrong diagnosis</text>
<circle cx="540" cy="90" r="30" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<text x="540" y="96" text-anchor="middle" font-size="14" fill="#003478">Staff</text>
<text x="540" y="140" text-anchor="middle" font-size="13" fill="#555">more ready than</text>
<text x="540" y="156" text-anchor="middle" font-size="13" fill="#555">leaders believe</text>
<circle cx="760" cy="90" r="30" fill="#fff" stroke="#CC0000" stroke-width="3"/>
<text x="760" y="96" text-anchor="middle" font-size="14" fill="#CC0000">Leaders</text>
<text x="760" y="140" text-anchor="middle" font-size="13" fill="#555">direction and support</text>
<text x="760" y="156" text-anchor="middle" font-size="13" fill="#555">often the constraint</text>
<text x="650" y="96" text-anchor="middle" font-size="22" fill="#777">vs.</text>
<text x="460" y="183" font-size="15" fill="#555">Blaming employees misses the real bottleneck.</text>
<text x="20" y="247" font-size="20" font-weight="700" fill="#003478">Pilot purgatory</text>
<circle cx="140" cy="315" r="45" fill="none" stroke="#003478" stroke-width="3"/>
<path d="M 183 300 L 185 315 L 172 308" fill="#003478"/>
<text x="140" y="312" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Demo</text>
<text x="140" y="330" text-anchor="middle" font-size="13" fill="#555">again</text>
<line x1="195" y1="315" x2="300" y2="315" stroke="#CC0000" stroke-width="3" stroke-dasharray="6 4"/>
<text x="248" y="302" text-anchor="middle" font-size="22" font-weight="700" fill="#CC0000">&#10005;</text>
<rect x="305" y="292" width="100" height="46" rx="6" fill="#fff" stroke="#003478" stroke-width="2"/>
<text x="355" y="312" text-anchor="middle" font-size="13" fill="#003478">Owned, funded</text>
<text x="355" y="328" text-anchor="middle" font-size="13" fill="#003478">capability</text>
<text x="20" y="390" font-size="15" fill="#555">Impressive proofs of concept that never go live.</text>
<text x="460" y="247" font-size="20" font-weight="700" fill="#003478">Big-bang plans</text>
<path d="M 490 350 Q 650 230 810 350" fill="none" stroke="#CC0000" stroke-width="3" marker-end="url(#a03r)"/>
<circle cx="490" cy="350" r="6" fill="#003478"/>
<text x="490" y="372" text-anchor="middle" font-size="13" fill="#555">Today</text>
<text x="810" y="372" text-anchor="middle" font-size="13" fill="#555">First evidence</text>
<text x="650" y="282" text-anchor="middle" font-size="13" fill="#CC0000">untested assumptions, most of the budget</text>
<text x="460" y="398" font-size="15" fill="#555">You learn you were wrong after the money is spent.</text>
</svg>

<p class="punch">Each is a leadership failure, not a technical one.</p>

{{% note %}}
- Ask the room: which of these have you lived through? Usually all four get hands.
- The second panel is the surprise: McKinsey&rsquo;s *Superagency* research (Jan 2025) found employees more ready than leaders believed, and named leadership direction and support as a major constraint.
- Each of the three steps that follow is designed to counter one or more of these.
{{% /note %}}

***

<!-- The framework -->
{{< slide class="fs55" >}}

### The framework
# Goal &rarr; Readiness &rarr; Path

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Three chevrons: Start with the goal, assess readiness, chart the path. Each has a leadership question and an output.">
<polygon points="0,20 260,20 295,85 260,150 0,150" fill="#003478"/>
<polygon points="285,20 545,20 580,85 545,150 285,150 320,85" fill="#3a5f99"/>
<polygon points="570,20 825,20 860,85 825,150 570,150 605,85" fill="#7f9cc6"/>
<text x="130" y="72" text-anchor="middle" font-size="16" fill="#c9d6e8">STEP 1</text>
<text x="130" y="102" text-anchor="middle" font-size="24" font-weight="700" fill="#fff">Start with the goal</text>
<text x="432" y="72" text-anchor="middle" font-size="16" fill="#dce6f3">STEP 2</text>
<text x="432" y="102" text-anchor="middle" font-size="24" font-weight="700" fill="#fff">Assess readiness</text>
<text x="720" y="72" text-anchor="middle" font-size="16" fill="#fff">STEP 3</text>
<text x="720" y="102" text-anchor="middle" font-size="24" font-weight="700" fill="#fff">Chart the path</text>
<text x="0" y="190" font-size="13" font-weight="700" fill="#CC0000">THE QUESTION</text>
<text x="0" y="214" font-size="15" fill="#333">What business outcome are we</text>
<text x="0" y="234" font-size="15" fill="#333">changing, and how will we know?</text>
<text x="290" y="214" font-size="15" fill="#333">What stands between us and that</text>
<text x="290" y="234" font-size="15" fill="#333">outcome, across three pillars?</text>
<text x="580" y="214" font-size="15" fill="#333">What is the smallest next step that</text>
<text x="580" y="234" font-size="15" fill="#333">closes a gap and teaches us something?</text>
<line x1="0" y1="262" x2="860" y2="262" stroke="#ddd" stroke-width="1"/>
<text x="0" y="292" font-size="13" font-weight="700" fill="#CC0000">THE OUTPUT</text>
<rect x="0" y="305" width="265" height="80" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<text x="132" y="338" text-anchor="middle" font-size="17" font-weight="700" fill="#003478">Use-case charter</text>
<text x="132" y="362" text-anchor="middle" font-size="14" fill="#555">baseline &#183; target &#183; scope</text>
<rect x="290" y="305" width="265" height="80" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<text x="422" y="338" text-anchor="middle" font-size="17" font-weight="700" fill="#003478">Readiness profile</text>
<text x="422" y="362" text-anchor="middle" font-size="14" fill="#555">Workforce &#183; Organization &#183; Technology</text>
<rect x="580" y="305" width="280" height="80" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<text x="720" y="338" text-anchor="middle" font-size="17" font-weight="700" fill="#003478">Sequence of nimble steps</text>
<text x="720" y="362" text-anchor="middle" font-size="14" fill="#555">owner &#183; measure &#183; decision gate</text>
</svg>

{{% note %}}
- This is the whole session on one slide. Everything else unpacks one of these columns.
- The order matters. Readiness only has a meaning once you know the goal and scope. The path only has a direction once you know the gaps.
- Three pillars: workforce, organization and leadership, technology and systems. We unpack them in Step 2.
{{% /note %}}

***

<!-- ===== SECTION: GOAL ===== -->
{{< slide background-color="#003478" class="section" >}}

### Step 1
# Start with the Goal

<p>&ldquo;Adopt AI&rdquo; is not a goal</p>

***

<!-- Anatomy of a goal -->
{{< slide class="fs55" >}}

### Step 1 &middot; Goal
# From means to outcome

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="Weak goals describe means. A strong goal has four parts: outcome, measure, baseline to target, and scope or guardrails.">
<defs><marker id="a06" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<text x="0" y="22" font-size="13" font-weight="700" fill="#CC0000">MEANS, NOT GOALS</text>
<rect x="0" y="35" width="270" height="44" rx="6" fill="#fff" stroke="#999" stroke-width="1.5" stroke-dasharray="5 4"/>
<text x="135" y="63" text-anchor="middle" font-size="16" fill="#777">Use gen AI in customer service</text>
<rect x="0" y="89" width="270" height="44" rx="6" fill="#fff" stroke="#999" stroke-width="1.5" stroke-dasharray="5 4"/>
<text x="135" y="117" text-anchor="middle" font-size="16" fill="#777">Give everyone an AI assistant</text>
<rect x="0" y="143" width="270" height="44" rx="6" fill="#fff" stroke="#999" stroke-width="1.5" stroke-dasharray="5 4"/>
<text x="135" y="171" text-anchor="middle" font-size="16" fill="#777">Become an AI-first company</text>
<line x1="285" y1="111" x2="345" y2="111" stroke="#003478" stroke-width="3" marker-end="url(#a06)"/>
<text x="360" y="22" font-size="13" font-weight="700" fill="#CC0000">AN OUTCOME GOAL</text>
<rect x="360" y="35" width="500" height="152" rx="8" fill="#f4f6f9"/>
<text x="378" y="70" font-size="19" fill="#003478"><tspan font-weight="700">Reduce handling time</tspan> on billing</text>
<text x="378" y="96" font-size="19" fill="#003478">inquiries <tspan font-weight="700">by 20%</tspan> within <tspan font-weight="700">two quarters</tspan>,</text>
<text x="378" y="122" font-size="19" fill="#003478"><tspan font-weight="700">without lowering</tspan> customer satisfaction</text>
<text x="378" y="148" font-size="19" fill="#003478">or first-contact resolution.</text>
<text x="378" y="174" font-size="13" fill="#777">Baseline measured today: average handling time per inquiry</text>
<rect x="0" y="232" width="200" height="170" rx="8" fill="#003478"/>
<text x="100" y="270" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">Outcome</text>
<text x="100" y="304" text-anchor="middle" font-size="14" fill="#dce6f3">What business result</text>
<text x="100" y="322" text-anchor="middle" font-size="14" fill="#dce6f3">changes?</text>
<text x="100" y="370" text-anchor="middle" font-size="14" fill="#fff" font-style="italic">handling time</text>
<rect x="220" y="232" width="200" height="170" rx="8" fill="#3a5f99"/>
<text x="320" y="270" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">Measure</text>
<text x="320" y="304" text-anchor="middle" font-size="14" fill="#dce6f3">How will we know,</text>
<text x="320" y="322" text-anchor="middle" font-size="14" fill="#dce6f3">in numbers?</text>
<text x="320" y="370" text-anchor="middle" font-size="14" fill="#fff" font-style="italic">minutes per inquiry</text>
<rect x="440" y="232" width="200" height="170" rx="8" fill="#5a7db3"/>
<text x="540" y="270" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">Baseline &#8594; target</text>
<text x="540" y="304" text-anchor="middle" font-size="14" fill="#fff">Where are we now,</text>
<text x="540" y="322" text-anchor="middle" font-size="14" fill="#fff">where by when?</text>
<text x="540" y="370" text-anchor="middle" font-size="14" fill="#fff" font-style="italic">&#8722;20% in 2 quarters</text>
<rect x="660" y="232" width="200" height="170" rx="8" fill="#dce6f3"/>
<text x="760" y="270" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">Scope + guardrails</text>
<text x="760" y="304" text-anchor="middle" font-size="14" fill="#003478">Where, and what</text>
<text x="760" y="322" text-anchor="middle" font-size="14" fill="#003478">must not get worse?</text>
<text x="760" y="370" text-anchor="middle" font-size="14" fill="#003478" font-style="italic">billing &#183; CSAT, FCR</text>
</svg>

{{% note %}}
- &ldquo;Deploy a copilot to 5,000 employees&rdquo; is a means. So is &ldquo;become AI-first.&rdquo;
- The four boxes are the test. If a proposed goal is missing any one of them, send it back.
- Guardrails matter: a goal that improves speed while quietly degrading quality is not a win.
- Two more examples from the reading: proposal first drafts from three days to one with partner review unchanged; underwriting decisions within 24 hours from 40% to 70% for small commercial policies.
{{% /note %}}

***

<!-- Use-case charter canvas -->
{{< slide class="fs55" >}}

### Step 1 &middot; Goal
# The one-page use-case charter

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="A six-box charter canvas: problem, baseline, target, alternatives, intended scope, and value mechanism, which is highlighted as most often skipped.">
<rect x="0" y="0" width="280" height="195" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<rect x="290" y="0" width="280" height="195" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<rect x="580" y="0" width="280" height="195" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<rect x="0" y="210" width="280" height="195" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<rect x="290" y="210" width="280" height="195" rx="8" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<rect x="580" y="210" width="280" height="195" rx="8" fill="#fff" stroke="#CC0000" stroke-width="3"/>
<circle cx="32" cy="34" r="18" fill="#003478"/><text x="32" y="40" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">1</text>
<text x="60" y="41" font-size="20" font-weight="700" fill="#003478">Problem</text>
<text x="20" y="90" font-size="15" fill="#333">What business problem</text>
<text x="20" y="112" font-size="15" fill="#333">exists today, and who</text>
<text x="20" y="134" font-size="15" fill="#333">experiences it?</text>
<circle cx="322" cy="34" r="18" fill="#003478"/><text x="322" y="40" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">2</text>
<text x="350" y="41" font-size="20" font-weight="700" fill="#003478">Baseline</text>
<text x="310" y="90" font-size="15" fill="#333">How does the process</text>
<text x="310" y="112" font-size="15" fill="#333">perform now? Time, cost,</text>
<text x="310" y="134" font-size="15" fill="#333">quality, errors, customers.</text>
<circle cx="612" cy="34" r="18" fill="#003478"/><text x="612" y="40" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">3</text>
<text x="640" y="41" font-size="20" font-weight="700" fill="#003478">Target</text>
<text x="600" y="90" font-size="15" fill="#333">What improvement would</text>
<text x="600" y="112" font-size="15" fill="#333">matter, and by when?</text>
<circle cx="32" cy="244" r="18" fill="#003478"/><text x="32" y="250" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">4</text>
<text x="60" y="251" font-size="20" font-weight="700" fill="#003478">Alternatives</text>
<text x="20" y="300" font-size="15" fill="#333">Would process redesign,</text>
<text x="20" y="322" font-size="15" fill="#333">rules or plain software do</text>
<text x="20" y="344" font-size="15" fill="#333">it cheaper? AI must earn</text>
<text x="20" y="366" font-size="15" fill="#333">its place.</text>
<circle cx="322" cy="244" r="18" fill="#003478"/><text x="322" y="250" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">5</text>
<text x="350" y="251" font-size="20" font-weight="700" fill="#003478">Intended scope</text>
<text x="310" y="300" font-size="15" fill="#333">Supervised pilot,</text>
<text x="310" y="322" font-size="15" fill="#333">department, or enterprise?</text>
<text x="310" y="358" font-size="15" font-weight="700" fill="#003478">Readiness is always</text>
<text x="310" y="380" font-size="15" font-weight="700" fill="#003478">judged for a scope.</text>
<circle cx="612" cy="244" r="18" fill="#CC0000"/><text x="612" y="250" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">6</text>
<text x="640" y="251" font-size="20" font-weight="700" fill="#CC0000">Value mechanism</text>
<text x="600" y="300" font-size="15" fill="#333">How does an improvement</text>
<text x="600" y="322" font-size="15" fill="#333">become a business benefit?</text>
<text x="600" y="366" font-size="14" font-style="italic" fill="#CC0000">Most often skipped</text>
</svg>

{{% note %}}
- One page. Written before any readiness assessment, and before any purchase.
- Box 4 is the honesty check. Many good goals are not AI goals.
- Box 5 sets up Step 2: you cannot say whether you are &ldquo;ready&rdquo; until you say ready for what.
- Box 6 is next slide.
{{% /note %}}

***

<!-- Value mechanism -->
{{< slide class="fs55" >}}

### Step 1 &middot; Goal
# Saved time is not yet value

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Two hours saved per week is an intermediate result. A leadership decision turns it into capacity, service, reduced overtime or another benefit. Without a decision it evaporates.">
<defs><marker id="a08" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker><marker id="a08r" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#CC0000"/></marker></defs>
<rect x="0" y="150" width="200" height="90" rx="10" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<text x="100" y="186" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">&#8220;2 hours saved</text>
<text x="100" y="212" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">per week&#8221;</text>
<text x="100" y="270" text-anchor="middle" font-size="14" fill="#555">intermediate result</text>
<line x1="200" y1="195" x2="280" y2="195" stroke="#003478" stroke-width="3" marker-end="url(#a08)"/>
<polygon points="350,135 420,195 350,255 280,195" fill="#003478"/>
<text x="350" y="190" text-anchor="middle" font-size="14" font-weight="700" fill="#fff">Leader</text>
<text x="350" y="208" text-anchor="middle" font-size="14" font-weight="700" fill="#fff">decides</text>
<line x1="420" y1="195" x2="560" y2="45" stroke="#003478" stroke-width="3" marker-end="url(#a08)"/>
<line x1="420" y1="195" x2="560" y2="125" stroke="#003478" stroke-width="3" marker-end="url(#a08)"/>
<line x1="420" y1="195" x2="560" y2="205" stroke="#003478" stroke-width="3" marker-end="url(#a08)"/>
<line x1="420" y1="195" x2="560" y2="285" stroke="#003478" stroke-width="3" marker-end="url(#a08)"/>
<rect x="568" y="22" width="292" height="46" rx="6" fill="#003478"/>
<text x="714" y="51" text-anchor="middle" font-size="16" fill="#fff">More capacity, same headcount</text>
<rect x="568" y="102" width="292" height="46" rx="6" fill="#003478"/>
<text x="714" y="131" text-anchor="middle" font-size="16" fill="#fff">Better or faster service</text>
<rect x="568" y="182" width="292" height="46" rx="6" fill="#003478"/>
<text x="714" y="211" text-anchor="middle" font-size="16" fill="#fff">Less overtime or contractor spend</text>
<rect x="568" y="262" width="292" height="46" rx="6" fill="#003478"/>
<text x="714" y="291" text-anchor="middle" font-size="16" fill="#fff">Another measurable gain</text>
<path d="M 350 255 Q 350 360 540 360" fill="none" stroke="#CC0000" stroke-width="3" stroke-dasharray="7 5" marker-end="url(#a08r)"/>
<text x="380" y="300" font-size="14" fill="#CC0000">no owner, no decision</text>
<rect x="568" y="338" width="292" height="46" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2" stroke-dasharray="6 4"/>
<text x="714" y="367" text-anchor="middle" font-size="16" fill="#CC0000">Disappears into the working week</text>
</svg>

{{% note %}}
- This is box 6 of the charter. It is a leadership decision, not an analytics task.
- Decide in advance, and name who owns the decision. Otherwise the efficiency is real, but nobody can find it in the P&amp;L.
{{% /note %}}

***

<!-- Suitability screen -->
{{< slide class="fs55" >}}

### Step 1 &middot; Goal
# Is the goal AI-suitable?

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="Radar chart on five criteria: business value, data availability, problem fit, technical feasibility, risk profile. A strong candidate scores high on all five; a weak one scores low on data and problem fit.">
<g transform="translate(300,215) scale(0.85)">
<polygon points="0,-180 171,-56 106,146 -106,146 -171,-56" fill="none" stroke="#ccc" stroke-width="1.5"/>
<polygon points="0,-120 114,-37 71,97 -71,97 -114,-37" fill="none" stroke="#ccc" stroke-width="1.5"/>
<polygon points="0,-60 57,-19 35,49 -35,49 -57,-19" fill="none" stroke="#ccc" stroke-width="1.5"/>
<g stroke="#ccc" stroke-width="1.5"><line x1="0" y1="0" x2="0" y2="-180"/><line x1="0" y1="0" x2="171" y2="-56"/><line x1="0" y1="0" x2="106" y2="146"/><line x1="0" y1="0" x2="-106" y2="146"/><line x1="0" y1="0" x2="-171" y2="-56"/></g>
<polygon points="0,-180 171,-56 71,97 -106,146 -114,-37" fill="#003478" fill-opacity="0.18" stroke="#003478" stroke-width="3"/>
<polygon points="0,-120 57,-19 35,49 -71,97 -57,-19" fill="#CC0000" fill-opacity="0.10" stroke="#CC0000" stroke-width="3" stroke-dasharray="7 5"/>
<text x="0" y="-192" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">Business value</text>
<text x="180" y="-62" font-size="16" font-weight="700" fill="#003478">Data availability</text>
<text x="112" y="172" font-size="16" font-weight="700" fill="#003478">Problem fit</text>
<text x="-112" y="172" text-anchor="end" font-size="16" font-weight="700" fill="#003478">Technical feasibility</text>
<text x="-180" y="-62" text-anchor="end" font-size="16" font-weight="700" fill="#003478">Risk profile</text>
<text x="-6" y="-122" text-anchor="end" font-size="12" fill="#999">med</text>
<text x="-6" y="-62" text-anchor="end" font-size="12" fill="#999">low</text>
<text x="-8" y="-170" text-anchor="end" font-size="12" fill="#999">high</text>
</g>
<line x1="600" y1="40" x2="635" y2="40" stroke="#003478" stroke-width="3"/>
<text x="648" y="46" font-size="16" font-weight="700" fill="#003478">Strong candidate</text>
<text x="648" y="68" font-size="14" fill="#555">clear KPI, data on hand,</text>
<text x="648" y="86" font-size="14" fill="#555">language-heavy work</text>
<line x1="600" y1="130" x2="635" y2="130" stroke="#CC0000" stroke-width="3" stroke-dasharray="7 5"/>
<text x="648" y="136" font-size="16" font-weight="700" fill="#CC0000">Weak candidate</text>
<text x="648" y="158" font-size="14" fill="#555">thin data, and a rule</text>
<text x="648" y="176" font-size="14" fill="#555">would solve it anyway</text>
<rect x="600" y="230" width="260" height="150" rx="8" fill="#f4f6f9"/>
<text x="618" y="262" font-size="15" font-weight="700" fill="#003478">Use the screen to</text>
<text x="618" y="290" font-size="15" fill="#333">&#8226; rank candidate goals</text>
<text x="618" y="316" font-size="15" fill="#333">&#8226; avoid chasing problems</text>
<text x="630" y="338" font-size="15" fill="#333">AI will not solve</text>
<text x="618" y="364" font-size="13" font-style="italic" fill="#777">Suitability is not binary.</text>
</svg>

{{% note %}}
- Five criteria from the reading. Outer ring is high suitability, inner ring low.
- &ldquo;Problem fit&rdquo; means language-, pattern- or judgment-heavy work that rules handle poorly. If an if-then rule would do it, use the rule.
- &ldquo;Risk profile&rdquo; high means low risk with clear guidelines; low means high risk of harm, bias or regulatory exposure.
- The illustrated candidates are hypothetical. In practice teams score several candidate goals and compare shapes.
{{% /note %}}

***

<!-- ===== SECTION: READINESS ===== -->
{{< slide background-color="#003478" class="section" >}}

### Step 2
# Assess Readiness

<p>Can we achieve this outcome, at this scope, with what we have today?</p>

***

<!-- The three pillars -->
{{< slide class="fs55" >}}

### Step 2 &middot; Readiness
# Three pillars, two lenses

<svg class="dg" viewBox="0 0 860 440" role="img" aria-label="A temple. The roof is the goal at a stated scope. Three pillars: Workforce, Organization and Leadership, Technology and Systems. Two horizontal bands cross all pillars: business value, and responsible AI and risk. The foundation is evidence.">
<polygon points="430,0 860,70 0,70" fill="#003478"/>
<text x="430" y="52" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">The goal, at a stated scope</text>
<rect x="30" y="80" width="230" height="290" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="315" y="80" width="230" height="290" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="600" y="80" width="230" height="290" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<text x="145" y="112" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">Workforce</text>
<text x="145" y="140" text-anchor="middle" font-size="14" fill="#333">Can people use, evaluate</text>
<text x="145" y="158" text-anchor="middle" font-size="14" fill="#333">and work effectively</text>
<text x="145" y="176" text-anchor="middle" font-size="14" fill="#333">with the solution?</text>
<text x="430" y="112" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">Organization</text>
<text x="430" y="134" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">&amp; Leadership</text>
<text x="430" y="160" text-anchor="middle" font-size="14" fill="#333">Can we direct, support,</text>
<text x="430" y="178" text-anchor="middle" font-size="14" fill="#333">govern and sustain it?</text>
<text x="715" y="112" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">Technology</text>
<text x="715" y="134" text-anchor="middle" font-size="20" font-weight="700" fill="#003478">&amp; Systems</text>
<text x="715" y="160" text-anchor="middle" font-size="14" fill="#333">Will it run reliably,</text>
<text x="715" y="178" text-anchor="middle" font-size="14" fill="#333">securely, economically?</text>
<rect x="0" y="210" width="860" height="56" fill="#003478" fill-opacity="0.88"/>
<text x="430" y="234" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">Lens: Business value</text>
<text x="430" y="255" text-anchor="middle" font-size="13" fill="#dce6f3">better work? benefit captured? acceptable total cost?</text>
<rect x="0" y="286" width="860" height="56" fill="#CC0000" fill-opacity="0.88"/>
<text x="430" y="310" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">Lens: Responsible AI &amp; risk</text>
<text x="430" y="331" text-anchor="middle" font-size="13" fill="#fff">problems recognized? leaders accountable? safeguards enforced and monitored?</text>
<rect x="0" y="378" width="860" height="50" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<text x="430" y="410" text-anchor="middle" font-size="17" font-weight="700" fill="#003478">Foundation: evidence, not assurances</text>
</svg>

<p class="refs">A teaching framework, not a validated instrument. Draws on the <a href="https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=936225">NIST AI RMF</a> and 2025 OECD and McKinsey research.</p>

{{% note %}}
- Three pillars, each with one core question. The two lenses are applied inside every pillar rather than added as extra pillars; this mirrors NIST&rsquo;s treatment of governance as cross-cutting, not a one-time sign-off.
- The roof is the goal from Step 1. No roof, no meaningful assessment.
- The foundation is the habit we will insist on: every rating backed by evidence.
{{% /note %}}

***

<!-- Which pillar limits progress -->
{{< slide class="fs55" >}}

### Step 2 &middot; Readiness
# Find the limiting pillar

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Three mini temples, each with one short pillar. Enthusiastic workforce without organizational support. Committed leadership without a viable system. Excellent technology without a workforce or workflow to use it.">
<g transform="translate(0,0)">
<polygon points="140,20 270,60 10,60" fill="#003478"/>
<rect x="30" y="66" width="50" height="200" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="115" y="166" width="50" height="100" fill="#fff" stroke="#CC0000" stroke-width="3" stroke-dasharray="6 4"/>
<rect x="200" y="66" width="50" height="200" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<text x="55" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">W</text>
<text x="140" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#CC0000">O&amp;L</text>
<text x="225" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">T&amp;S</text>
<text x="140" y="328" text-anchor="middle" font-size="15" fill="#333">An enthusiastic workforce</text>
<text x="140" y="348" text-anchor="middle" font-size="15" fill="#333">without organizational</text>
<text x="140" y="368" text-anchor="middle" font-size="15" fill="#333">support</text>
</g>
<g transform="translate(295,0)">
<polygon points="140,20 270,60 10,60" fill="#003478"/>
<rect x="30" y="66" width="50" height="200" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="115" y="66" width="50" height="200" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="200" y="166" width="50" height="100" fill="#fff" stroke="#CC0000" stroke-width="3" stroke-dasharray="6 4"/>
<text x="55" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">W</text>
<text x="140" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">O&amp;L</text>
<text x="225" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#CC0000">T&amp;S</text>
<text x="140" y="328" text-anchor="middle" font-size="15" fill="#333">Committed leadership</text>
<text x="140" y="348" text-anchor="middle" font-size="15" fill="#333">without an operationally</text>
<text x="140" y="368" text-anchor="middle" font-size="15" fill="#333">viable system</text>
</g>
<g transform="translate(590,0)">
<polygon points="140,20 270,60 10,60" fill="#003478"/>
<rect x="30" y="166" width="50" height="100" fill="#fff" stroke="#CC0000" stroke-width="3" stroke-dasharray="6 4"/>
<rect x="115" y="66" width="50" height="200" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="200" y="66" width="50" height="200" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<text x="55" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#CC0000">W</text>
<text x="140" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">O&amp;L</text>
<text x="225" y="290" text-anchor="middle" font-size="14" font-weight="700" fill="#003478">T&amp;S</text>
<text x="140" y="328" text-anchor="middle" font-size="15" fill="#333">Excellent technology</text>
<text x="140" y="348" text-anchor="middle" font-size="15" fill="#333">without people or a</text>
<text x="140" y="368" text-anchor="middle" font-size="15" fill="#333">workflow to use it</text>
</g>
</svg>

<p class="punch">The shortest pillar is where the next step should go.</p>

{{% note %}}
- The pillars are deliberately distinct so the assessment can tell you *which* one is holding the roof down.
- Ask: which of these three temples does your organization look like right now? Given the *Superagency* findings, many will recognize the first one.
{{% /note %}}

***

<!-- Pillar 1: Workforce -->
{{< slide class="fs55" >}}

### Pillar 1
# Workforce: fit for the job

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="Three nested groups: everyone needs general AI literacy; workflow owners and managers need workflow ownership skills; a small group of technical specialists needs advanced skills. Six subdimensions are assessed.">
<ellipse cx="220" cy="215" rx="215" ry="195" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<ellipse cx="220" cy="270" rx="140" ry="135" fill="#7f9cc6"/>
<ellipse cx="220" cy="325" rx="70" ry="75" fill="#003478"/>
<text x="220" y="62" text-anchor="middle" font-size="18" font-weight="700" fill="#003478">Everyday users</text>
<text x="220" y="84" text-anchor="middle" font-size="14" fill="#003478">general AI literacy &#183; appropriate reliance</text>
<text x="220" y="172" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">Workflow owners</text>
<text x="220" y="192" text-anchor="middle" font-size="17" font-weight="700" fill="#fff">&amp; managers</text>
<text x="220" y="214" text-anchor="middle" font-size="13" fill="#fff">redesign &#183; review &#183; coaching</text>
<text x="220" y="318" text-anchor="middle" font-size="15" font-weight="700" fill="#fff">Technical</text>
<text x="220" y="337" text-anchor="middle" font-size="15" font-weight="700" fill="#fff">specialists</text>
<text x="480" y="22" font-size="13" font-weight="700" fill="#CC0000">ASSESS FOR THE USE CASE</text>
<rect x="480" y="36" width="380" height="46" rx="6" fill="#f4f6f9"/><text x="496" y="65" font-size="15" fill="#003478"><tspan font-weight="700">AI literacy</tspan> &amp; knowing when not to rely</text>
<rect x="480" y="90" width="380" height="46" rx="6" fill="#f4f6f9"/><text x="496" y="119" font-size="15" fill="#003478"><tspan font-weight="700">Role-specific proficiency</tspan> on real tasks</text>
<rect x="480" y="144" width="380" height="46" rx="6" fill="#f4f6f9"/><text x="496" y="173" font-size="15" fill="#003478"><tspan font-weight="700">Critical evaluation</tspan> &amp; domain judgment</text>
<rect x="480" y="198" width="380" height="46" rx="6" fill="#f4f6f9"/><text x="496" y="227" font-size="15" fill="#003478"><tspan font-weight="700">Responsible use</tspan> &amp; data handling</text>
<rect x="480" y="252" width="380" height="46" rx="6" fill="#f4f6f9"/><text x="496" y="281" font-size="15" fill="#003478"><tspan font-weight="700">Willingness, trust</tspan> &amp; participation</text>
<rect x="480" y="306" width="380" height="46" rx="6" fill="#f4f6f9"/><text x="496" y="335" font-size="15" fill="#003478"><tspan font-weight="700">Learning capacity</tspan> &amp; collaboration</text>
<rect x="480" y="364" width="380" height="46" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="670" y="393" text-anchor="middle" font-size="15" font-weight="700" fill="#CC0000">Attendance &#8800; readiness. Demonstrate it.</text>
</svg>

<p class="refs">Source: <a href="https://www.oecd.org/content/dam/oecd/en/publications/reports/2025/04/bridging-the-ai-skills-gap_b43c7c4a/66d0702e-en.pdf">OECD, Bridging the AI Skills Gap (2025)</a></p>

{{% note %}}
- OECD 2025: most workers need general AI literacy; only specialists need advanced skills. Yet much of the training on offer leans to the advanced end.
- So assess three groups with three different bars, not one bar for everyone. Python is not a workforce-wide requirement.
- Evidence: scenario-based assessments, reviewed work samples, error-detection exercises, policy scenarios, anonymous surveys, protected learning time.
- Whether leaders provide the time, incentives and resources is *not* scored here. That goes in the next pillar.
{{% /note %}}

***

<!-- Pillar 2: Organization and Leadership -->
{{< slide class="fs55" >}}

### Pillar 2
# Organization &amp; Leadership

<svg class="dg" viewBox="0 0 860 410" role="img" aria-label="A bridge from a promising application to a managed business capability, held up by seven supports: strategic alignment, executive sponsorship, operating model, workflow redesign, change and incentives, governance, and funding with value realization.">
<rect x="0" y="40" width="150" height="110" rx="10" fill="#fff" stroke="#003478" stroke-width="2" stroke-dasharray="6 4"/>
<text x="75" y="88" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">Promising</text>
<text x="75" y="110" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">application</text>
<rect x="710" y="40" width="150" height="110" rx="10" fill="#003478"/>
<text x="785" y="80" text-anchor="middle" font-size="16" font-weight="700" fill="#fff">Managed</text>
<text x="785" y="102" text-anchor="middle" font-size="16" font-weight="700" fill="#fff">business</text>
<text x="785" y="124" text-anchor="middle" font-size="16" font-weight="700" fill="#fff">capability</text>
<rect x="150" y="80" width="560" height="26" fill="#3a5f99"/>
<g fill="#dce6f3" stroke="#003478" stroke-width="2">
<rect x="160" y="106" width="70" height="200"/>
<rect x="238" y="106" width="70" height="200"/>
<rect x="316" y="106" width="70" height="200"/>
<rect x="394" y="106" width="70" height="200"/>
<rect x="472" y="106" width="70" height="200"/>
<rect x="550" y="106" width="70" height="200"/>
<rect x="628" y="106" width="70" height="200"/>
</g>
<g font-size="14" font-weight="700" fill="#003478" text-anchor="middle">
<text transform="translate(200,206) rotate(-90)">Strategic alignment</text>
<text transform="translate(278,206) rotate(-90)">Executive sponsorship</text>
<text transform="translate(356,206) rotate(-90)">Cross-functional ownership</text>
<text transform="translate(434,206) rotate(-90)" fill="#CC0000">Workflow &amp; role redesign</text>
<text transform="translate(512,206) rotate(-90)">Change &amp; incentives</text>
<text transform="translate(590,206) rotate(-90)">Governance &amp; risk</text>
<text transform="translate(668,206) rotate(-90)">Funding &amp; value</text>
</g>
<rect x="0" y="330" width="860" height="70" rx="8" fill="#f4f6f9"/>
<text x="20" y="360" font-size="15" fill="#333"><tspan font-weight="700" fill="#003478">Evidence:</tspan> named sponsor with decision rights &#183; responsibility matrix &#183; current and</text>
<text x="20" y="384" font-size="15" fill="#333">proposed workflow maps &#183; revised incentives &#183; AI policy &amp; risk assessment &#183; lifecycle budget</text>
</svg>

<p class="refs">Survey associations, not guarantees: <a href="https://www.mckinsey.com/our-insights/the-state-of-ai-2025">McKinsey, State of AI 2025</a></p>

{{% note %}}
- This pillar answers: can the organization turn a promising application into something owned, funded, governed and operated?
- Workflow redesign is highlighted because it is the factor McKinsey found most associated with reported EBIT impact, and the one most often skipped.
- Given the *Superagency* findings, this is frequently where the binding constraint sits. Leaders should expect to find gaps in their own pillar.
{{% /note %}}

***

<!-- Pillar 3: Technology and Systems -->
{{< slide class="fs55" >}}

### Pillar 3
# Technology: the demo is the tip

<svg class="dg" viewBox="0 0 860 430" role="img" aria-label="An iceberg. Above the waterline: model performance in a demo. Below the waterline: data and knowledge, task evaluation, integration, security and privacy, reliability and cost, operational ownership, and human oversight.">
<rect x="0" y="105" width="860" height="325" fill="#eef3fa"/>
<line x1="0" y1="105" x2="860" y2="105" stroke="#7f9cc6" stroke-width="3"/>
<polygon points="430,10 500,105 360,105" fill="#fff" stroke="#003478" stroke-width="2"/>
<text x="545" y="60" font-size="17" font-weight="700" fill="#003478">What the vendor shows:</text>
<text x="545" y="84" font-size="16" fill="#333">model performance in a demo</text>
<polygon points="360,105 500,105 650,230 600,380 430,420 260,380 210,230" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<text x="430" y="160" text-anchor="middle" font-size="12" font-weight="700" fill="#CC0000">WHAT MUST RUN IN PRODUCTION</text>
<g font-size="15" fill="#003478" font-weight="700" text-anchor="middle">
<text x="430" y="190">Data &amp; knowledge readiness</text>
<text x="430" y="220">Task evaluation on real cases</text>
<text x="430" y="250">Integration &amp; workflow fit</text>
<text x="430" y="280">Security, privacy, access</text>
<text x="430" y="310">Reliability, scale &amp; cost</text>
<text x="430" y="340">Operational ownership</text>
<text x="430" y="370" fill="#CC0000">Human oversight &amp; controls</text>
</g>
<text x="20" y="160" font-size="14" fill="#555">Evidence:</text>
<text x="20" y="182" font-size="14" fill="#555">data inventory</text>
<text x="20" y="202" font-size="14" fill="#555">evaluation dataset</text>
<text x="20" y="222" font-size="14" fill="#555">end-to-end tests</text>
<text x="20" y="242" font-size="14" fill="#555">security review</text>
<text x="20" y="262" font-size="14" fill="#555">load tests</text>
<text x="690" y="262" font-size="14" fill="#555">cost per task</text>
<text x="690" y="282" font-size="14" fill="#555">named service owner</text>
<text x="690" y="302" font-size="14" fill="#555">runbooks, rollback</text>
<text x="690" y="322" font-size="14" fill="#555">approval gates</text>
<text x="690" y="342" font-size="14" fill="#555">audit records</text>
</svg>

{{% note %}}
- Assess the whole operational solution, not the model in a demo.
- &ldquo;Cost per completed business task&rdquo; is the economic metric to ask for, not cost per token.
- NIST: evaluate before deployment and throughout operation. Monitoring, security, resilience, risk treatment are ongoing.
- The last row is next slide.
{{% /note %}}

***

<!-- Agents: recommend vs. act -->
{{< slide class="fs55" >}}

### Pillar 3 &middot; Agents
# Recommending is not executing

<svg class="dg" viewBox="0 0 860 380" role="img" aria-label="An autonomy spectrum from suggest, to draft for review, to act with approval, to act autonomously. Required controls rise with autonomy.">
<defs><linearGradient id="g15" x1="0" x2="1" y1="0" y2="0"><stop offset="0" stop-color="#dce6f3"/><stop offset="1" stop-color="#003478"/></linearGradient><marker id="a15" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="14" markerHeight="14" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<rect x="0" y="40" width="840" height="34" rx="17" fill="url(#g15)"/>
<polygon points="840,30 860,57 840,84" fill="#003478"/>
<text x="0" y="24" font-size="14" font-weight="700" fill="#003478">LESS AUTONOMY</text>
<text x="860" y="24" text-anchor="end" font-size="14" font-weight="700" fill="#003478">MORE AUTONOMY</text>
<g font-size="17" font-weight="700" fill="#003478" text-anchor="middle">
<text x="105" y="115">Suggest</text>
<text x="320" y="115">Draft for review</text>
<text x="540" y="115">Act with approval</text>
<text x="755" y="115">Act autonomously</text>
</g>
<g font-size="14" fill="#555" text-anchor="middle">
<text x="105" y="140">a recommendation</text>
<text x="320" y="140">a human edits and sends</text>
<text x="540" y="140">a human approves each action</text>
<text x="755" y="140">executes transactions</text>
</g>
<rect x="45" y="300" width="120" height="30" fill="#7f9cc6"/>
<rect x="260" y="255" width="120" height="75" fill="#5a7db3"/>
<rect x="480" y="205" width="120" height="125" fill="#3a5f99"/>
<rect x="680" y="160" width="150" height="170" fill="#CC0000"/>
<line x1="0" y1="330" x2="860" y2="330" stroke="#333" stroke-width="1.5"/>
<g font-size="13" fill="#fff" text-anchor="middle">
<text x="105" y="320">verify output</text>
<text x="320" y="282">review step</text>
<text x="320" y="300">escalation rules</text>
<text x="540" y="232">approval gates</text>
<text x="540" y="250">action limits</text>
<text x="540" y="268">audit records</text>
<text x="755" y="190">hard action limits</text>
<text x="755" y="208">kill switch</text>
<text x="755" y="226">independent backup</text>
<text x="755" y="244">fallback procedure</text>
<text x="755" y="262">monitoring</text>
</g>
<text x="0" y="362" font-size="15" font-weight="700" fill="#003478">Controls required</text>
</svg>

<p class="punch">Can a person review, intervene, or stop it? For agents, that row decides readiness.</p>

{{% note %}}
- Callback to the Responsible AI session: the Replit agent had a written order not to act, and still had the permissions to act.
- The further right a use case sits, the more of the Technology &amp; Systems pillar must be at level 3 before you deploy.
{{% /note %}}

***

<!-- Readiness for a scope -->
{{< slide class="fs55" >}}

### Step 2 &middot; Readiness
# &ldquo;Ready&rdquo; for what scope?

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="A grid rating the same team on three pillars for three scopes. For a supervised pilot all pillars are ready. For a department deployment they are developing. For enterprise operation they are low.">
<g font-size="15" font-weight="700" fill="#003478" text-anchor="middle">
<text x="340" y="24">Supervised pilot</text>
<text x="550" y="24">Department</text>
<text x="760" y="24">Enterprise</text>
</g>
<g font-size="16" font-weight="700" fill="#003478">
<text x="0" y="78">Workforce</text>
<text x="0" y="158">Organization</text>
<text x="0" y="178">&amp; Leadership</text>
<text x="0" y="248">Technology</text>
<text x="0" y="268">&amp; Systems</text>
</g>
<g>
<rect x="250" y="40" width="180" height="70" rx="6" fill="#003478"/>
<rect x="460" y="40" width="180" height="70" rx="6" fill="#7f9cc6"/>
<rect x="670" y="40" width="180" height="70" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<rect x="250" y="130" width="180" height="70" rx="6" fill="#003478"/>
<rect x="460" y="130" width="180" height="70" rx="6" fill="#7f9cc6"/>
<rect x="670" y="130" width="180" height="70" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<rect x="250" y="220" width="180" height="70" rx="6" fill="#003478"/>
<rect x="460" y="220" width="180" height="70" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<rect x="670" y="220" width="180" height="70" rx="6" fill="#fff" stroke="#CC0000" stroke-width="2"/>
</g>
<g font-size="22" font-weight="700" text-anchor="middle">
<text x="340" y="83" fill="#fff">3</text><text x="550" y="83" fill="#003478">2</text><text x="760" y="83" fill="#CC0000">1</text>
<text x="340" y="173" fill="#fff">3</text><text x="550" y="173" fill="#003478">2</text><text x="760" y="173" fill="#CC0000">1</text>
<text x="340" y="263" fill="#fff">3</text><text x="550" y="263" fill="#CC0000">1</text><text x="760" y="263" fill="#CC0000">1</text>
</g>
<rect x="0" y="315" width="275" height="95" rx="8" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="16" y="342" font-size="16" font-weight="700" fill="#CC0000">1 &#8212; Low</text>
<text x="16" y="366" font-size="13" fill="#333">Missing, unclear or untested.</text>
<text x="16" y="386" font-size="13" fill="#777">Assurances, demos, plans.</text>
<rect x="292" y="315" width="275" height="95" rx="8" fill="#7f9cc6"/>
<text x="308" y="342" font-size="16" font-weight="700" fill="#003478">2 &#8212; Developing</text>
<text x="308" y="366" font-size="13" fill="#003478">Works in a limited setting; gaps remain.</text>
<text x="308" y="386" font-size="13" fill="#003478">Pilot results, partial training.</text>
<rect x="585" y="315" width="275" height="95" rx="8" fill="#003478"/>
<text x="601" y="342" font-size="16" font-weight="700" fill="#fff">3 &#8212; Ready for the scope</text>
<text x="601" y="366" font-size="13" fill="#fff">Shown under representative conditions.</text>
<text x="601" y="386" font-size="13" fill="#dce6f3">Task tests, tested safeguards.</text>
</svg>

{{% note %}}
- Same team, same use case, three different answers depending on scope. That is why the charter states the intended scope.
- Illustrative ratings. Example from the reading: a team may be ready for an internal drafting assistant, but not for autonomous customer-facing decisions.
- Every rating needs evidence. &ldquo;We think so&rdquo; is a level 1.
{{% /note %}}

***

<!-- Averages hide blockers -->
{{< slide class="fs55" >}}

### Step 2 &middot; Readiness
# Averages hide blockers

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="A bar chart of eight subdimension ratings averaging 2.5, which looks fine. One rating, accountable ownership, is 1 and is a blocker, so the gate for this scope is closed. Four blocker types are listed.">
<line x1="40" y1="40" x2="40" y2="330" stroke="#999" stroke-width="1.5"/>
<line x1="40" y1="330" x2="520" y2="330" stroke="#999" stroke-width="1.5"/>
<g font-size="13" fill="#777" text-anchor="end"><text x="32" y="335">0</text><text x="32" y="245">1</text><text x="32" y="155">2</text><text x="32" y="65">3</text></g>
<g fill="#003478">
<rect x="55" y="60" width="44" height="270"/>
<rect x="115" y="60" width="44" height="270"/>
<rect x="175" y="150" width="44" height="180"/>
<rect x="235" y="60" width="44" height="270"/>
<rect x="355" y="60" width="44" height="270"/>
<rect x="415" y="150" width="44" height="180"/>
<rect x="475" y="60" width="44" height="270"/>
</g>
<rect x="295" y="240" width="44" height="90" fill="#CC0000"/>
<line x1="40" y1="105" x2="530" y2="105" stroke="#777" stroke-width="2" stroke-dasharray="8 5"/>
<text x="50" y="24" font-size="14" fill="#555">Dashed line: average 2.5 &#8212; &#8220;looks fine&#8221;</text>
<text x="317" y="228" text-anchor="middle" font-size="13" font-weight="700" fill="#CC0000">owner?</text>
<text x="280" y="360" text-anchor="middle" font-size="14" fill="#555">subdimension ratings for a controlled pilot</text>
<rect x="570" y="40" width="290" height="70" rx="8" fill="#CC0000"/>
<text x="715" y="70" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">GATE CLOSED</text>
<text x="715" y="94" text-anchor="middle" font-size="14" fill="#fff">for this scope</text>
<text x="570" y="146" font-size="13" font-weight="700" fill="#CC0000">ANY OF THESE BLOCKS DEPLOYMENT</text>
<g font-size="15" fill="#333">
<rect x="570" y="160" width="6" height="40" fill="#CC0000"/><text x="588" y="177">Lawful data access</text><text x="588" y="195">or data handling unresolved</text>
<rect x="570" y="212" width="6" height="40" fill="#CC0000"/><text x="588" y="229">Output quality not shown to</text><text x="588" y="247">meet the threshold</text>
<rect x="570" y="264" width="6" height="40" fill="#CC0000"/><text x="588" y="281">No accountable owner for</text><text x="588" y="299">the workflow or system</text>
<rect x="570" y="316" width="6" height="40" fill="#CC0000"/><text x="588" y="333">No way for a human to</text><text x="588" y="351">review, intervene or stop</text>
</g>
</svg>

<p class="punch">Blockers do not kill the goal. They tell you where the path must start.</p>

{{% note %}}
- A readiness profile is a diagnostic, not a score to average.
- The four blocker types apply regardless of how strong everything else looks.
- Bridge to Step 3: the blockers become the first steps of the path.
{{% /note %}}

***

<!-- ===== SECTION: PATH ===== -->
{{< slide background-color="#003478" class="section" >}}

### Step 3
# Chart a Path of Nimble Steps

<p>Small, owned, measured &mdash; each step ends in a decision</p>

***

<!-- Leap vs steps -->
{{< slide class="fs55" >}}

### Step 3 &middot; Path
# One leap or many steps?

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Left: a big-bang leap from today to the goal with no evidence until the end. Right: a staircase of small steps, each ending in a decision gate, with evidence along the way and an option to stop early.">
<defs><marker id="a19r" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#CC0000"/></marker></defs>
<text x="0" y="24" font-size="19" font-weight="700" fill="#CC0000">The big bang</text>
<line x1="20" y1="320" x2="400" y2="320" stroke="#999" stroke-width="1.5"/>
<circle cx="40" cy="300" r="9" fill="#003478"/>
<text x="40" y="345" text-anchor="middle" font-size="14" fill="#555">Today</text>
<rect x="340" y="60" width="60" height="40" rx="6" fill="#003478"/>
<text x="370" y="86" text-anchor="middle" font-size="14" font-weight="700" fill="#fff">Goal</text>
<path d="M 48 295 Q 180 20 335 80" fill="none" stroke="#CC0000" stroke-width="3" stroke-dasharray="8 5" marker-end="url(#a19r)"/>
<rect x="110" y="170" width="200" height="60" rx="6" fill="#fff" stroke="#ccc"/>
<text x="210" y="196" text-anchor="middle" font-size="14" fill="#555">One program, one budget,</text>
<text x="210" y="216" text-anchor="middle" font-size="14" fill="#555">one launch date</text>
<text x="0" y="380" font-size="15" fill="#CC0000">First real evidence arrives at the end.</text>
<line x1="430" y1="20" x2="430" y2="390" stroke="#ddd" stroke-width="2"/>
<text x="460" y="24" font-size="19" font-weight="700" fill="#003478">Nimble steps</text>
<line x1="460" y1="320" x2="860" y2="320" stroke="#999" stroke-width="1.5"/>
<circle cx="480" cy="300" r="9" fill="#003478"/>
<text x="480" y="345" text-anchor="middle" font-size="14" fill="#555">Today</text>
<rect x="800" y="60" width="60" height="40" rx="6" fill="#003478"/>
<text x="830" y="86" text-anchor="middle" font-size="14" font-weight="700" fill="#fff">Goal</text>
<polyline points="480,300 540,300 540,250 600,250 600,200 660,200 660,150 720,150 720,100 790,100" fill="none" stroke="#003478" stroke-width="4"/>
<g fill="#CC0000">
<polygon points="540,288 550,300 540,312 530,300"/>
<polygon points="600,238 610,250 600,262 590,250"/>
<polygon points="660,188 670,200 660,212 650,200"/>
<polygon points="720,138 730,150 720,162 710,150"/>
</g>
<path d="M 660 212 L 660 280" stroke="#999" stroke-width="2" stroke-dasharray="4 4"/>
<text x="668" y="275" font-size="13" fill="#777">stop or adjust</text>
<text x="460" y="380" font-size="15" fill="#003478">Evidence at every step. Failure is cheap.</text>
</svg>

{{% note %}}
- The big bang bets everything on untested assumptions. You learn they were wrong after most of the money is spent.
- Nimble steps move forward and generate evidence for the next decision. Each red diamond is a gate.
- Stopping at a gate is not failure. It is the system working.
{{% /note %}}

***

<!-- Anatomy of a nimble step -->
{{< slide class="fs55" >}}

### Step 3 &middot; Path
# Anatomy of a nimble step

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="A loop: a gap from the readiness profile leads to a step, which is measured against the baseline, then reaches a decision gate with three options: expand scope, adjust and repeat, or stop. Seven properties are annotated.">
<defs><marker id="a20" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<rect x="0" y="150" width="150" height="80" rx="10" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="75" y="184" text-anchor="middle" font-size="17" font-weight="700" fill="#CC0000">Gap</text>
<text x="75" y="206" text-anchor="middle" font-size="13" fill="#555">shortest pillar</text>
<line x1="150" y1="190" x2="205" y2="190" stroke="#003478" stroke-width="3" marker-end="url(#a20)"/>
<rect x="212" y="130" width="200" height="120" rx="10" fill="#003478"/>
<text x="312" y="168" text-anchor="middle" font-size="19" font-weight="700" fill="#fff">Step</text>
<text x="312" y="194" text-anchor="middle" font-size="14" fill="#dce6f3">one owner</text>
<text x="312" y="214" text-anchor="middle" font-size="14" fill="#dce6f3">weeks, not quarters</text>
<text x="312" y="234" text-anchor="middle" font-size="14" fill="#dce6f3">reversible</text>
<line x1="412" y1="190" x2="467" y2="190" stroke="#003478" stroke-width="3" marker-end="url(#a20)"/>
<rect x="474" y="130" width="170" height="120" rx="10" fill="#3a5f99"/>
<text x="559" y="168" text-anchor="middle" font-size="19" font-weight="700" fill="#fff">Measure</text>
<text x="559" y="194" text-anchor="middle" font-size="14" fill="#fff">vs. baseline</text>
<text x="559" y="214" text-anchor="middle" font-size="14" fill="#fff">criteria set</text>
<text x="559" y="234" text-anchor="middle" font-size="14" fill="#fff">before starting</text>
<line x1="644" y1="190" x2="680" y2="190" stroke="#003478" stroke-width="3" marker-end="url(#a20)"/>
<polygon points="735,135 790,190 735,245 680,190" fill="#CC0000"/>
<text x="735" y="196" text-anchor="middle" font-size="16" font-weight="700" fill="#fff">Gate</text>
<line x1="790" y1="190" x2="815" y2="80" stroke="#003478" stroke-width="2" marker-end="url(#a20)"/>
<line x1="790" y1="190" x2="815" y2="190" stroke="#003478" stroke-width="2" marker-end="url(#a20)"/>
<line x1="790" y1="190" x2="815" y2="300" stroke="#003478" stroke-width="2" marker-end="url(#a20)"/>
<text x="860" y="70" text-anchor="end" font-size="15" font-weight="700" fill="#003478">Expand</text>
<text x="860" y="215" text-anchor="end" font-size="15" font-weight="700" fill="#003478">Adjust</text>
<text x="860" y="320" text-anchor="end" font-size="15" font-weight="700" fill="#777">Stop</text>
<path d="M 735 245 Q 735 330 420 330 Q 75 330 75 236" fill="none" stroke="#003478" stroke-width="2" stroke-dasharray="7 5" marker-end="url(#a20)"/>
<text x="420" y="320" text-anchor="middle" font-size="14" fill="#003478">next gap</text>
<g font-size="13" font-weight="700" fill="#CC0000">
<text x="75" y="135" text-anchor="middle">GAP-TARGETED</text>
<text x="312" y="112" text-anchor="middle">GOAL-ANCHORED &#183; OWNED</text>
<text x="312" y="275" text-anchor="middle">SMALL &#183; TIME-BOXED &#183; REVERSIBLE</text>
<text x="559" y="112" text-anchor="middle">MEASURED</text>
<text x="735" y="118" text-anchor="middle">ENDS IN A DECISION</text>
</g>
<rect x="0" y="360" width="860" height="52" rx="8" fill="#f4f6f9"/>
<text x="430" y="392" text-anchor="middle" font-size="16" fill="#003478">A step moves a charter measure, or removes a named blocker to moving it.</text>
</svg>

{{% note %}}
- The seven properties from the reading are in red around the loop: goal-anchored, gap-targeted, small and time-boxed, reversible, owned, measured against a baseline, ends in a decision.
- Gap-targeted means the pillar that is currently the binding constraint, not the one that is most fun to work on. Technology teams love to keep tuning the model while the ownership gap stays open.
- Success criteria are set before the step starts. Otherwise every result looks like success.
{{% /note %}}

***

<!-- Scope ladder -->
{{< slide class="fs55" >}}

### Step 3 &middot; Path
# Climb the scope ladder

<svg class="dg" viewBox="0 0 860 430" role="img" aria-label="A four-rung ladder: explore, controlled pilot, defined-scope deployment, scale. For each rung, what must be true to enter and what the stage must prove.">
<line x1="330" y1="10" x2="330" y2="420" stroke="#003478" stroke-width="5"/>
<line x1="530" y1="10" x2="530" y2="420" stroke="#003478" stroke-width="5"/>
<text x="310" y="22" text-anchor="end" font-size="13" font-weight="700" fill="#CC0000">TO ENTER</text>
<text x="550" y="22" font-size="13" font-weight="700" fill="#CC0000">MUST PROVE</text>
<rect x="330" y="40" width="200" height="66" fill="#003478"/>
<text x="430" y="70" text-anchor="middle" font-size="18" font-weight="700" fill="#fff">Scale</text>
<text x="430" y="92" text-anchor="middle" font-size="13" fill="#dce6f3">multiple units, enterprise</text>
<rect x="330" y="140" width="200" height="66" fill="#3a5f99"/>
<text x="430" y="170" text-anchor="middle" font-size="18" font-weight="700" fill="#fff">Defined scope</text>
<text x="430" y="192" text-anchor="middle" font-size="13" fill="#fff">department, routine review</text>
<rect x="330" y="240" width="200" height="66" fill="#5a7db3"/>
<text x="430" y="270" text-anchor="middle" font-size="18" font-weight="700" fill="#fff">Controlled pilot</text>
<text x="430" y="292" text-anchor="middle" font-size="13" fill="#fff">one team, every output reviewed</text>
<rect x="330" y="340" width="200" height="66" fill="#dce6f3"/>
<text x="430" y="370" text-anchor="middle" font-size="18" font-weight="700" fill="#003478">Explore</text>
<text x="430" y="392" text-anchor="middle" font-size="13" fill="#003478">volunteers, sandbox</text>
<g font-size="14" fill="#333" text-anchor="end">
<text x="310" y="68">Repeatable playbook; platform</text><text x="310" y="88">&amp; governance capacity</text>
<text x="310" y="168">Redesigned workflow; service</text><text x="310" y="188">owner; monitoring; run budget</text>
<text x="310" y="268">No open blockers; baseline</text><text x="310" y="288">captured; users trained</text>
<text x="310" y="368">A charter and an</text><text x="310" y="388">approved tool</text>
</g>
<g font-size="14" fill="#333">
<text x="550" y="68">Replicable and sustainable</text><text x="550" y="88">economically</text>
<text x="550" y="168">Benefit holds at volume and</text><text x="550" y="188">shows up in business results</text>
<text x="550" y="268">Measured improvement vs.</text><text x="550" y="288">baseline, acceptable risk</text>
<text x="550" y="368">Plausible and worth</text><text x="550" y="388">measuring</text>
</g>
</svg>

{{% note %}}
- Each rung needs readiness *for that rung*, not for the top of the ladder. That is what makes the first steps affordable.
- At the upper rungs, a hub-and-spoke model helps: a central team supplies platforms, guardrails and expertise; business units adapt them to their workflows.
- Pilot purgatory is what happens when nobody defines the right-hand column for the pilot rung.
{{% /note %}}

***

<!-- Advance the pillars together -->
{{< slide class="fs55" >}}

### Step 3 &middot; Path
# Lift the lowest pillar first

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Pillar levels across three snapshots. In each snapshot, the lowest pillar blocking the next scope receives the next step, until all three clear the threshold for the next rung.">
<defs><marker id="a22" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#CC0000"/></marker></defs>
<line x1="0" y1="310" x2="860" y2="310" stroke="#999" stroke-width="1.5"/>
<line x1="0" y1="110" x2="860" y2="110" stroke="#CC0000" stroke-width="2" stroke-dasharray="8 5"/>
<text x="0" y="100" font-size="14" fill="#CC0000">needed for the next scope</text>
<g transform="translate(40,0)">
<rect x="0" y="180" width="50" height="130" fill="#003478"/>
<rect x="60" y="250" width="50" height="60" fill="#3a5f99" stroke="#CC0000" stroke-width="3"/>
<rect x="120" y="180" width="50" height="130" fill="#7f9cc6"/>
<line x1="85" y1="240" x2="85" y2="160" stroke="#CC0000" stroke-width="3" marker-end="url(#a22)"/>
<text x="85" y="345" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Week 0</text>
</g>
<g transform="translate(330,0)">
<rect x="0" y="180" width="50" height="130" fill="#003478"/>
<rect x="60" y="150" width="50" height="160" fill="#3a5f99"/>
<rect x="120" y="200" width="50" height="110" fill="#7f9cc6" stroke="#CC0000" stroke-width="3"/>
<line x1="145" y1="190" x2="145" y2="130" stroke="#CC0000" stroke-width="3" marker-end="url(#a22)"/>
<text x="85" y="345" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Week 4</text>
</g>
<g transform="translate(620,0)">
<rect x="0" y="100" width="50" height="210" fill="#003478"/>
<rect x="60" y="100" width="50" height="210" fill="#3a5f99"/>
<rect x="120" y="100" width="50" height="210" fill="#7f9cc6"/>
<text x="85" y="345" text-anchor="middle" font-size="15" font-weight="700" fill="#003478">Week 8: gate opens</text>
</g>
<g font-size="13" fill="#555" text-anchor="middle">
<text x="65" y="330">W</text><text x="125" y="330">O&amp;L</text><text x="185" y="330">T&amp;S</text>
<text x="355" y="330">W</text><text x="415" y="330">O&amp;L</text><text x="475" y="330">T&amp;S</text>
<text x="645" y="330">W</text><text x="705" y="330">O&amp;L</text><text x="765" y="330">T&amp;S</text>
</g>
<text x="0" y="388" font-size="15" fill="#333">Technology the workforce cannot use, or training for a workflow nobody redesigned, is the appearance of progress.</text>
</svg>

{{% note %}}
- The rule: direct the next step at the lowest-rated pillar that blocks the next scope, and keep the other two from falling behind.
- Illustrative timeline. The red arrow marks where the next step goes in each snapshot.
{{% /note %}}

***

<!-- ===== SECTION: CASE ===== -->
{{< slide background-color="#003478" class="section" >}}

### Worked example
# A Regional Insurer

<p>Reduce handling time on billing inquiries by 20% in two quarters, without lowering CSAT or first-contact resolution</p>

***

<!-- Case: readiness profile -->
{{< slide class="fs55" >}}

### Worked example &middot; Readiness
# Profile for a controlled pilot

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="Insurer readiness profile. Workforce developing, level 2. Organization and Leadership low, level 1. Technology and Systems developing, level 2. Two blockers: no workflow owner, and informal use of unapproved tools with customer data.">
<text x="0" y="22" font-size="15" fill="#555">Solution: an AI assistant that drafts responses for service agents from policy and billing records.</text>
<polygon points="300,40 590,82 10,82" fill="#003478"/>
<text x="300" y="72" text-anchor="middle" font-size="15" font-weight="700" fill="#fff">Billing AHT &#8722;20% &#183; controlled pilot</text>
<rect x="40" y="90" width="120" height="230" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="240" y="245" width="120" height="75" fill="#fff" stroke="#CC0000" stroke-width="3" stroke-dasharray="6 4"/>
<rect x="440" y="90" width="120" height="230" fill="#dce6f3" stroke="#003478" stroke-width="2"/>
<rect x="40" y="170" width="120" height="150" fill="#7f9cc6"/>
<rect x="440" y="170" width="120" height="150" fill="#7f9cc6"/>
<rect x="240" y="245" width="120" height="75" fill="#CC0000" fill-opacity="0.15"/>
<text x="100" y="130" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">Workforce</text>
<text x="300" y="200" text-anchor="middle" font-size="16" font-weight="700" fill="#CC0000">Org &amp; Leadership</text>
<text x="500" y="122" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">Technology</text>
<text x="500" y="142" text-anchor="middle" font-size="16" font-weight="700" fill="#003478">&amp; Systems</text>
<text x="100" y="260" text-anchor="middle" font-size="40" font-weight="700" fill="#fff">2</text>
<text x="300" y="300" text-anchor="middle" font-size="40" font-weight="700" fill="#CC0000">1</text>
<text x="500" y="260" text-anchor="middle" font-size="40" font-weight="700" fill="#fff">2</text>
<g font-size="13" fill="#333">
<text x="40" y="345">Agents eager; many use</text><text x="40" y="363">consumer AI informally.</text><text x="40" y="381">Error spotting untested.</text>
<text x="240" y="345">Sponsor, but no workflow</text><text x="240" y="363">owner; review undefined;</text><text x="240" y="381">metrics reward speed only.</text>
<text x="440" y="345">Good generic demo. Billing</text><text x="440" y="363">integration untested; no</text><text x="440" y="381">evaluation set of real cases.</text>
</g>
<rect x="620" y="90" width="240" height="230" rx="8" fill="#fff" stroke="#CC0000" stroke-width="3"/>
<text x="740" y="122" text-anchor="middle" font-size="17" font-weight="700" fill="#CC0000">Blockers</text>
<circle cx="645" cy="164" r="12" fill="#CC0000"/><text x="645" y="169" text-anchor="middle" font-size="14" font-weight="700" fill="#fff">!</text>
<text x="668" y="160" font-size="15" fill="#333">No accountable</text>
<text x="668" y="180" font-size="15" fill="#333">workflow owner</text>
<circle cx="645" cy="234" r="12" fill="#CC0000"/><text x="645" y="239" text-anchor="middle" font-size="14" font-weight="700" fill="#fff">!</text>
<text x="668" y="230" font-size="15" fill="#333">Unapproved tools</text>
<text x="668" y="250" font-size="15" fill="#333">used with customer</text>
<text x="668" y="270" font-size="15" fill="#333">data</text>
</svg>

{{% note %}}
- An illustrative case built for teaching, not a real company.
- Note the shape: enthusiastic workforce, promising technology, and the leadership pillar is the shortest. That is the *Superagency* pattern.
- The two blockers mean no pilot yet, however good the demo looks. They are where the path starts.
{{% /note %}}

***

<!-- Case: the path as a timeline -->
{{< slide class="fs50" >}}

### Worked example &middot; Path
# Six steps, about fourteen weeks

<svg class="dg" viewBox="0 0 860 450" role="img" aria-label="Gantt chart. Step 1, weeks 0 to 2: name a workflow owner and issue data guidance. Step 2, weeks 2 to 5: build an evaluation set and test offline. Step 3, weeks 2 to 4 in parallel: redesign the workflow with agents. Step 4, week 5 to 6: train 12 pilot agents. Step 5, weeks 6 to 12: controlled pilot. Step 6, weeks 12 to 14: decide how to use freed capacity and adjust metrics. Each ends in a gate.">
<g font-size="12" fill="#999" text-anchor="middle">
<text x="300" y="18">0</text><text x="370" y="18">2</text><text x="440" y="18">4</text><text x="510" y="18">6</text><text x="580" y="18">8</text><text x="650" y="18">10</text><text x="720" y="18">12</text><text x="790" y="18">14</text>
</g>
<text x="860" y="18" text-anchor="end" font-size="12" fill="#999">wk</text>
<g stroke="#eee" stroke-width="1">
<line x1="300" y1="26" x2="300" y2="400"/><line x1="370" y1="26" x2="370" y2="400"/><line x1="440" y1="26" x2="440" y2="400"/><line x1="510" y1="26" x2="510" y2="400"/><line x1="580" y1="26" x2="580" y2="400"/><line x1="650" y1="26" x2="650" y2="400"/><line x1="720" y1="26" x2="720" y2="400"/><line x1="790" y1="26" x2="790" y2="400"/>
</g>
<g font-size="14" fill="#003478">
<text x="0" y="52" font-weight="700">1 Name owner; data guidance</text><text x="0" y="70" font-size="12" fill="#777">VP of Service &#183; O&amp;L, W</text>
<text x="0" y="112" font-weight="700">2 Evaluation set, offline test</text><text x="0" y="130" font-size="12" fill="#777">Ops lead + IT &#183; T&amp;S</text>
<text x="0" y="172" font-weight="700">3 Redesign workflow with agents</text><text x="0" y="190" font-size="12" fill="#777">Workflow owner &#183; O&amp;L, W</text>
<text x="0" y="232" font-weight="700">4 Train 12 pilot agents</text><text x="0" y="250" font-size="12" fill="#777">Team manager &#183; W</text>
<text x="0" y="292" font-weight="700">5 Controlled pilot</text><text x="0" y="310" font-size="12" fill="#777">Workflow owner &#183; all three</text>
<text x="0" y="352" font-weight="700">6 Capture value; fix metrics</text><text x="0" y="370" font-size="12" fill="#777">VP of Service &#183; O&amp;L</text>
</g>
<rect x="300" y="40" width="70" height="30" rx="4" fill="#3a5f99"/>
<rect x="370" y="100" width="105" height="30" rx="4" fill="#7f9cc6"/>
<rect x="370" y="160" width="70" height="30" rx="4" fill="#3a5f99"/>
<rect x="475" y="220" width="35" height="30" rx="4" fill="#003478"/>
<rect x="510" y="280" width="210" height="30" rx="4" fill="#003478"/>
<rect x="720" y="340" width="70" height="30" rx="4" fill="#3a5f99"/>
<g fill="#CC0000">
<polygon points="370,43 382,55 370,67 358,55"/>
<polygon points="475,103 487,115 475,127 463,115"/>
<polygon points="440,163 452,175 440,187 428,175"/>
<polygon points="510,223 522,235 510,247 498,235"/>
<polygon points="720,283 732,295 720,307 708,295"/>
<polygon points="790,343 802,355 790,367 778,355"/>
</g>
<g font-size="12" fill="#CC0000">
<text x="390" y="60">blockers cleared?</text>
<text x="495" y="120">meets threshold? else adjust or stop</text>
<text x="460" y="180">workflow signed off?</text>
<text x="530" y="240">agents pass check?</text>
<text x="740" y="300" >expand,</text><text x="740" y="314">adjust, stop</text>
<text x="808" y="360" text-anchor="start">plan</text>
</g>
<rect x="0" y="410" width="860" height="38" rx="6" fill="#f4f6f9"/>
<text x="430" y="435" text-anchor="middle" font-size="15" fill="#003478">If step 2 fails, the insurer has spent <tspan font-weight="700">five weeks</tspan> learning it, not a year.</text>
</svg>

{{% note %}}
- Read it top to bottom. Step 1 clears both blockers. Steps 2 and 3 run in parallel on two different pillars. Step 4 trains for the redesigned workflow, not the tool in general.
- Pilot success measures: handling time, CSAT, first-contact resolution, error rate, rework, all against the baseline.
- Step 6 is the value mechanism from the charter: decide what the freed capacity becomes, and stop rewarding speed alone. It is a prerequisite for climbing to the defined-scope rung.
- The numbers (200 evaluation cases, 12 agents, time boxes) are illustrative.
{{% /note %}}

***

<!-- Measure value not activity -->
{{< slide class="fs55" >}}

### Step 3 &middot; Path
# Measure value, not activity

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Activity metrics such as users with access and prompts per week compared with value metrics measured against a baseline: quality, rework, cycle time, risk incidents, and the business outcome.">
<rect x="0" y="0" width="330" height="330" rx="10" fill="#f4f6f9"/>
<text x="165" y="40" text-anchor="middle" font-size="19" font-weight="700" fill="#777">Activity</text>
<text x="165" y="64" text-anchor="middle" font-size="14" fill="#999">easy to count, says little</text>
<g font-size="16" fill="#999" text-anchor="middle">
<rect x="35" y="95" width="260" height="46" rx="6" fill="#fff" stroke="#ccc"/><text x="165" y="124">Users with access</text>
<rect x="35" y="155" width="260" height="46" rx="6" fill="#fff" stroke="#ccc"/><text x="165" y="184">Prompts per week</text>
<rect x="35" y="215" width="260" height="46" rx="6" fill="#fff" stroke="#ccc"/><text x="165" y="244">Training completions</text>
</g>
<text x="400" y="175" text-anchor="middle" font-size="28" fill="#999">vs.</text>
<rect x="470" y="0" width="390" height="330" rx="10" fill="#003478"/>
<text x="665" y="40" text-anchor="middle" font-size="19" font-weight="700" fill="#fff">Value, against the baseline</text>
<text x="665" y="64" text-anchor="middle" font-size="14" fill="#dce6f3">reported against the charter, every step</text>
<g font-size="16" fill="#fff">
<text x="500" y="110">Quality</text><text x="500" y="150">Rework</text><text x="500" y="190">Cycle time</text><text x="500" y="230">Risk incidents</text><text x="500" y="270" font-weight="700">Business outcome</text>
</g>
<g stroke="#7f9cc6" stroke-width="2">
<line x1="660" y1="104" x2="830" y2="104"/><line x1="660" y1="144" x2="830" y2="144"/><line x1="660" y1="184" x2="830" y2="184"/><line x1="660" y1="224" x2="830" y2="224"/><line x1="660" y1="264" x2="830" y2="264"/>
</g>
<g fill="#fff">
<circle cx="720" cy="104" r="6"/><circle cx="720" cy="144" r="6"/><circle cx="720" cy="184" r="6"/><circle cx="720" cy="224" r="6"/><circle cx="720" cy="264" r="6"/>
</g>
<g fill="#7f9cc6">
<circle cx="790" cy="104" r="6"/><circle cx="680" cy="144" r="6"/><circle cx="670" cy="184" r="6"/><circle cx="680" cy="224" r="6"/><circle cx="780" cy="264" r="6"/>
</g>
<text x="720" y="300" text-anchor="middle" font-size="12" fill="#fff">&#9679; baseline</text>
<text x="800" y="300" text-anchor="middle" font-size="12" fill="#7f9cc6">&#9679; now</text>
<text x="0" y="372" font-size="16" fill="#333">Communicate results regularly, <tspan font-weight="700" fill="#003478">including failures</tspan>. It builds trust and keeps funding tied to evidence.</text>
</svg>

{{% note %}}
- Activity metrics are useful for operations, not for deciding whether the transformation is working.
- The dot plot is schematic: each value metric is compared to its baseline. Direction matters per metric (rework and cycle time should go down).
{{% /note %}}

***

<!-- ===== SECTION: LEADER ===== -->
{{< slide background-color="#003478" class="section" >}}

# What This Asks of Leaders

<p>A discipline for leaders, more than a tool for analysts</p>

***

<!-- Leader's job at each step -->
{{< slide class="fs55" >}}

### The leader's job
# Different work at each step

<svg class="dg" viewBox="0 0 860 420" role="img" aria-label="The three chevrons again with the leader's job under each, and a band across all three for what leaders do throughout.">
<polygon points="0,0 260,0 295,50 260,100 0,100" fill="#003478"/>
<polygon points="285,0 545,0 580,50 545,100 285,100 320,50" fill="#3a5f99"/>
<polygon points="570,0 825,0 860,50 825,100 570,100 605,50" fill="#7f9cc6"/>
<text x="130" y="58" text-anchor="middle" font-size="22" font-weight="700" fill="#fff">Goal</text>
<text x="432" y="58" text-anchor="middle" font-size="22" font-weight="700" fill="#fff">Readiness</text>
<text x="720" y="58" text-anchor="middle" font-size="22" font-weight="700" fill="#fff">Path</text>
<g font-size="15" fill="#333">
<text x="0" y="140" font-weight="700" fill="#003478">Insist on an outcome</text><text x="0" y="160">and a baseline.</text>
<text x="0" y="192" font-weight="700" fill="#003478">Say no</text><text x="0" y="212">to use cases that lack one.</text>
<text x="0" y="244" font-weight="700" fill="#003478">Decide in advance</text><text x="0" y="264">how gains are captured.</text>
<text x="290" y="140" font-weight="700" fill="#003478">Ask for evidence,</text><text x="290" y="160">not assurances.</text>
<text x="290" y="192" font-weight="700" fill="#003478">Look at your own pillar</text><text x="290" y="212">first: sponsorship, decision</text><text x="290" y="232">rights, incentives.</text>
<text x="580" y="140" font-weight="700" fill="#003478">Fund steps, not programs.</text>
<text x="580" y="172" font-weight="700" fill="#003478">Protect learning time.</text>
<text x="580" y="204" font-weight="700" fill="#003478">Celebrate a good &#8220;stop.&#8221;</text>
<text x="580" y="236" font-weight="700" fill="#003478">Keep the gates honest.</text>
</g>
<rect x="0" y="300" width="860" height="110" rx="10" fill="#f4f6f9" stroke="#003478" stroke-width="2"/>
<text x="20" y="330" font-size="13" font-weight="700" fill="#CC0000">THROUGHOUT</text>
<text x="20" y="358" font-size="15" fill="#333"><tspan font-weight="700" fill="#003478">Involve the people whose work changes</tspan>: they hold the knowledge that makes redesign work.</text>
<text x="20" y="384" font-size="15" fill="#333"><tspan font-weight="700" fill="#003478">Be transparent</tspan> about what AI can and cannot do. <tspan font-weight="700" fill="#003478">Model appropriate reliance</tspan>. Decide on partial evidence.</text>
</svg>

{{% note %}}
- Same three chevrons as the framework slide. Now the row underneath is the leader&rsquo;s own to-do list.
- &ldquo;Celebrate a good stop&rdquo;: a well-run step that ends in stop saved the organization money and taught it something. If stopping is punished, the gates stop being honest.
- Leading here means comfort with ambiguity: deciding on partial evidence and changing course when the evidence says to.
{{% /note %}}

***

<!-- Common traps mapped to the framework -->
{{< slide class="fs55" >}}

### The leader's job
# Six traps, and where they hide

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Six traps placed on the framework. Goal: starting from the tool; leaving freed capacity unclaimed. Readiness: blaming the workforce; mistaking usage for readiness; scoring by average. Path: skipping workflow redesign.">
<polygon points="0,0 260,0 295,50 260,100 0,100" fill="#003478"/>
<polygon points="285,0 545,0 580,50 545,100 285,100 320,50" fill="#3a5f99"/>
<polygon points="570,0 825,0 860,50 825,100 570,100 605,50" fill="#7f9cc6"/>
<text x="130" y="58" text-anchor="middle" font-size="22" font-weight="700" fill="#fff">Goal</text>
<text x="432" y="58" text-anchor="middle" font-size="22" font-weight="700" fill="#fff">Readiness</text>
<text x="720" y="58" text-anchor="middle" font-size="22" font-weight="700" fill="#fff">Path</text>
<g>
<rect x="0" y="125" width="265" height="110" rx="8" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="16" y="155" font-size="16" font-weight="700" fill="#CC0000">&#9888; Starting from the tool</text>
<text x="16" y="180" font-size="14" fill="#333">Charter written after the</text>
<text x="16" y="198" font-size="14" fill="#333">purchase? Revisit it honestly.</text>
<rect x="0" y="250" width="265" height="110" rx="8" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="16" y="280" font-size="16" font-weight="700" fill="#CC0000">&#9888; Unclaimed capacity</text>
<text x="16" y="305" font-size="14" fill="#333">No value-realization plan,</text>
<text x="16" y="323" font-size="14" fill="#333">so the gains vanish.</text>
<rect x="290" y="125" width="265" height="72" rx="8" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="306" y="153" font-size="16" font-weight="700" fill="#CC0000">&#9888; Blaming the workforce</text>
<text x="306" y="177" font-size="14" fill="#333">Check leadership&#8217;s pillar first.</text>
<rect x="290" y="207" width="265" height="72" rx="8" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="306" y="235" font-size="16" font-weight="700" fill="#CC0000">&#9888; Usage = readiness</text>
<text x="306" y="259" font-size="14" fill="#333">Use without review is a risk.</text>
<rect x="290" y="289" width="265" height="72" rx="8" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="306" y="317" font-size="16" font-weight="700" fill="#CC0000">&#9888; Scoring by average</text>
<text x="306" y="341" font-size="14" fill="#333">An open blocker is still a no.</text>
<rect x="580" y="125" width="280" height="110" rx="8" fill="#fff" stroke="#CC0000" stroke-width="2"/>
<text x="596" y="155" font-size="16" font-weight="700" fill="#CC0000">&#9888; Skipping redesign</text>
<text x="596" y="180" font-size="14" fill="#333">AI on an unchanged process</text>
<text x="596" y="198" font-size="14" fill="#333">captures little and adds rework.</text>
</g>
</svg>

{{% note %}}
- Each trap maps to the step where it is most likely to bite, and the step that guards against it.
- Ask teams to name the trap they think their own organization is most exposed to.
{{% /note %}}

***

<!-- Project deliverables -->
{{< slide class="fs55" >}}

### Your project
# Apply it to one use case

<svg class="dg" viewBox="0 0 860 400" role="img" aria-label="Five deliverables in sequence: use-case charter, readiness profile, critical gaps, path of nimble steps, and a recommendation with four options: explore, controlled pilot, defined-scope deployment, or defer.">
<defs><marker id="a29" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="12" markerHeight="12" markerUnits="userSpaceOnUse" orient="auto-start-reverse"><path d="M0,0 L10,5 L0,10 z" fill="#003478"/></marker></defs>
<g>
<rect x="0" y="20" width="150" height="150" rx="10" fill="#003478"/>
<rect x="175" y="20" width="150" height="150" rx="10" fill="#003478"/>
<rect x="350" y="20" width="150" height="150" rx="10" fill="#3a5f99"/>
<rect x="525" y="20" width="150" height="150" rx="10" fill="#3a5f99"/>
</g>
<g stroke="#003478" stroke-width="3"><line x1="150" y1="95" x2="170" y2="95" marker-end="url(#a29)"/><line x1="325" y1="95" x2="345" y2="95" marker-end="url(#a29)"/><line x1="500" y1="95" x2="520" y2="95" marker-end="url(#a29)"/><line x1="675" y1="95" x2="695" y2="95" marker-end="url(#a29)"/></g>
<g font-size="30" font-weight="700" fill="#7f9cc6" text-anchor="middle"><text x="75" y="60">1</text><text x="250" y="60">2</text><text x="425" y="60">3</text><text x="600" y="60">4</text></g>
<g font-size="17" font-weight="700" fill="#fff" text-anchor="middle">
<text x="75" y="100">Use-case</text><text x="75" y="122">charter</text>
<text x="250" y="100">Readiness</text><text x="250" y="122">profile</text>
<text x="425" y="100">Critical</text><text x="425" y="122">gaps</text>
<text x="600" y="100">Path of</text><text x="600" y="122">nimble steps</text>
</g>
<g font-size="13" fill="#333">
<text x="0" y="198">problem &#183; baseline</text><text x="0" y="216">target &#183; alternatives</text><text x="0" y="234">scope &#183; value</text>
<text x="175" y="198">1&#8211;3 per pillar and</text><text x="175" y="216">subdimension, with</text><text x="175" y="234">evidence &amp; unknowns</text>
<text x="350" y="198">top three, incl.</text><text x="350" y="216">blockers; owner and</text><text x="350" y="234">corrective action</text>
<text x="525" y="198">time box &#183; owner</text><text x="525" y="216">measure &#183; gate</text>
</g>
<rect x="705" y="20" width="155" height="215" rx="10" fill="#fff" stroke="#CC0000" stroke-width="3"/>
<text x="782" y="50" text-anchor="middle" font-size="30" font-weight="700" fill="#CC0000">5</text>
<text x="782" y="78" text-anchor="middle" font-size="16" font-weight="700" fill="#CC0000">Recommend</text>
<g font-size="14" fill="#003478" text-anchor="middle">
<text x="782" y="112">Explore</text><text x="782" y="140">Controlled pilot</text><text x="782" y="168">Defined-scope</text><text x="782" y="186">deployment</text><text x="782" y="216">Defer</text>
</g>
<rect x="0" y="280" width="860" height="100" rx="10" fill="#f4f6f9"/>
<text x="430" y="320" text-anchor="middle" font-size="18" font-weight="700" fill="#003478">A strong submission shows which pillar is limiting progress</text>
<text x="430" y="350" text-anchor="middle" font-size="16" fill="#333">and argues that the first steps of the path are aimed there.</text>
</svg>

{{% note %}}
- Prefer task demonstrations, workflow maps and pilot data over self-assessments as evidence.
- The recommendation is one of four. &ldquo;Defer&rdquo; is a legitimate answer when the blockers cannot be cleared within the project horizon.
{{% /note %}}

***

<!-- Close -->
{{< slide class="fs55" >}}

### To close
# Which pillar is limiting you?

<svg class="dg" viewBox="0 0 860 210" role="img" aria-label="Summary: goal, readiness, path.">
<polygon points="0,20 260,20 295,85 260,150 0,150" fill="#003478"/>
<polygon points="285,20 545,20 580,85 545,150 285,150 320,85" fill="#3a5f99"/>
<polygon points="570,20 825,20 860,85 825,150 570,150 605,85" fill="#7f9cc6"/>
<text x="130" y="80" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">Outcome, baseline,</text>
<text x="130" y="104" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">scope</text>
<text x="432" y="80" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">Three pillars,</text>
<text x="432" y="104" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">evidence, blockers</text>
<text x="720" y="80" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">Small steps,</text>
<text x="720" y="104" text-anchor="middle" font-size="20" font-weight="700" fill="#fff">honest gates</text>
<text x="430" y="196" text-anchor="middle" font-size="18" font-style="italic" fill="#555">Do we face an employee-readiness problem, or a leadership-support problem?</text>
</svg>

<p class="refs">Further reading:
<a href="https://oecd.org/en/publications/2025/04/bridging-the-ai-skills-gap_b43c7c4a/full-report.html">OECD, Bridging the AI Skills Gap (2025)</a> &middot;
<a href="https://www.mckinsey.com/capabilities/tech-and-ai/our-insights/superagency-in-the-workplace-empowering-people-to-unlock-ais-full-potential-at-work">McKinsey, Superagency in the Workplace (2025)</a> &middot;
<a href="https://www.mckinsey.com/~/media/mckinsey/business%20functions/quantumblack/our%20insights/the%20state%20of%20ai/march%202025/the-state-of-ai-how-organizations-are-rewiring-to-capture-value_final.pdf">McKinsey, The State of AI (March 2025)</a> &middot;
<a href="https://www.oecd.org/en/publications/generative-ai-and-the-sme-workforce_2d08b99d-en/full-report/component-6.html">OECD, Generative AI and the SME Workforce (2025)</a> &middot;
<a href="https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=936225">NIST AI RMF</a> &middot;
Full write-up: <a href="/blog/leading-business-transformation/">Leading AI Transformation</a></p>

<p class="refs">The framework is a teaching tool, not a validated instrument. The survey findings are associations; no readiness score guarantees success.</p>

{{% note %}}
- Close on the discussion question from the *Superagency* reading. Give teams two minutes to answer it for their project organization.
- Point students to the blog post for the full tables of subdimensions and evidence.
{{% /note %}}
