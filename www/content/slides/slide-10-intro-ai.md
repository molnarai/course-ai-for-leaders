+++
title = "Introduction to Generative AI"
description = "Define, de-mystify, and deploy generative AI — from the history of AI to LLMs, prompting, agents, and enterprise implementation"
weight = 10
outputs = ["Reveal"]
math = true
thumbnail = "/imgs/Evolution_of_AI.png"


[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"

+++

<!--
    Slide deck for topic-01 — Introduction to Generative AI

    Two kinds of slides are used here:
      1. Image slides — figures, diagrams, screenshots and section dividers.
         Format: {{</* slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-000.png" */>}}
         Source images live in www/static/imgs/intro-ai-hugo-slide-images
      2. Native slides — text-heavy slides transcribed to markdown + HTML so the
         text stays selectable, searchable, accessible and editable.
         They use the helper classes defined in the style block below.

    Every content slide carries speaker notes in a {{%/* note */%}} block.
-->

<style>
/* Helper classes for the transcribed (non-image) slides in this deck.
   Palette follows reveal-robinson.css — GSU Blue #003478, GSU Crimson #CC0000. */

/* reveal-robinson.css pads sections by 50px with box-sizing: content-box, which
   makes every section 1060px wide on a 960px stage and clips text off the right
   edge. Scoped correction so the transcribed slides fit. */
.reveal .slides section { box-sizing: border-box; }
/* Body scale for the transcribed slides — each one is set to the largest step
   that still fits the 960x700 stage without overflowing. */
.reveal .slides section.fs66 { font-size: 0.66em; }
.reveal .slides section.fs63 { font-size: 0.63em; }
.reveal .slides section.fs60 { font-size: 0.60em; }
.reveal .slides section.fs55 { font-size: 0.55em; }
.reveal .slides section.fs54 { font-size: 0.54em; }
.reveal .slides section.fs52 { font-size: 0.52em; }
.reveal .slides section.fs48 { font-size: 0.48em; }

/* Titles stay a constant size regardless of the body scale (px, so they do not
   inherit the em reduction above). */
.reveal .slides section[class*="fs"] h1 { font-size: 56px; margin-bottom: 0.45em; }

.reveal .cols2 { display: grid; grid-template-columns: 1fr 1fr; gap: 0 2em; align-items: start; }
/* Four equal boxes. grid-auto-rows: 1fr makes both rows the same height and
   the default stretch alignment makes each card fill its cell, so all four end
   up identical regardless of how much text they hold. */
.reveal .grid2x2 { display: grid; grid-template-columns: 1fr 1fr;
                   grid-template-rows: 1fr auto 1fr; gap: 0.55em 1.6em; }
.reveal .grid2x2 > .card { margin: 0; height: 100%; padding: 0.45em 0.8em; }
.reveal .grid2x2 > .card p { margin: 0.4em 0 0 0; }
/* Divider between the "like humans" row and the "rationally" row. It spans
   both columns, and the auto-sized middle row keeps the two card rows equal.
   A horizontal-rule element cannot be used here — reveal-hugo splits slides on
   one, exactly as it does on the deck's *** markers. Note that even writing the
   tag name in a comment triggers it, which is why it is spelled out. */
.reveal .grid2x2 > .rowline { grid-column: 1 / -1; height: 0; margin: 0;
                              border-top: 1px solid #b9c4d4; }
.reveal .cols3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 0 1.5em; align-items: start; }
.reveal .cols4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 0.8em 1.2em; align-items: start; }

.reveal .sub { color: #CC0000; font-weight: 700; margin: 0.9em 0 0.3em 0; }
.reveal .cols2 > div > .sub:first-child,
.reveal .cols3 > div > .sub:first-child,
.reveal .cols4 > div > .sub:first-child { margin-top: 0; }

.reveal .card { background: #f4f6f9; border-left: 4px solid #003478;
                border-radius: 6px; padding: 0.55em 0.9em; margin: 0 0 0.6em 0; }
.reveal .card .hd { color: #003478; font-weight: 700; display: block; margin-bottom: 0.15em; }

.reveal .lead { font-style: italic; color: #555; text-align: center;
                max-width: 82%; margin: 0 auto 0.9em auto; }
.reveal .term { color: #CC0000; font-weight: 700; }
.reveal .refs { font-size: 0.62em; color: #777; margin-top: 0.8em; }
.reveal .refs a { color: #777; }
.reveal .cols2 p, .reveal .cols3 p, .reveal .cols4 p { margin: 0.35em 0; }

/* Section divider slides — flat brand panel carrying the deck's "DE …" motif.
   Colours sampled from the original divider images: panel #1F4099,
   prefix #97CAEB, word #EDEEEF. */
.reveal .slides section.section    { text-align: center; }
.reveal .slides section.section h1 { color: #EDEEEF; font-size: 2.8em;
                                     letter-spacing: 0.01em; margin: 0; }
.reveal .slides section.section h1 .de { color: #97CAEB; }

/* Outline slide — numbered agenda, terms in GSU Crimson as in the original. */
.reveal .slides ol.outline      { margin: 0.5em 0 0 1.4em; }
.reveal .slides ol.outline li   { margin-bottom: 0.55em; padding-left: 0.2em; }

/* Token-sequence figure (MLM / TLM), rebuilt from the original bitmap so the
   labels are readable and scale with the slide instead of being ~6pt. */
.reveal .tok        { display: grid; grid-template-columns: 92px repeat(12, 1fr);
                      gap: 2px 3px; align-items: center; margin: 0 0 10px 0; }
.reveal .tok .rl    { font-size: 11px; line-height: 1.15; text-align: left; color: #333; }
.reveal .tok .rl b  { font-size: 12px; }
.reveal .tok .cell  { border: 1px solid #7a7a7a; border-radius: 2px; text-align: center;
                      font-size: 11px; line-height: 1.5; white-space: nowrap;
                      letter-spacing: -0.01em; overflow: hidden; }
.reveal .tok .pred  { background: #E0CCE7; }
.reveal .tok .tokc  { background: #CCE5FF; }
.reveal .tok .posc  { background: #CDEB8B; }
.reveal .tok .langc { background: #DEDEDE; }
.reveal .tok .langc.fr { background: #fff; }
.reveal .tok .bar   { grid-column: 2 / span 12; background: #C5C5C5; border: 1px solid #7a7a7a;
                      text-align: center; font-size: 11px; line-height: 1.6; }
.reveal .tok .up,
.reveal .tok .plus  { text-align: center; font-size: 10px; line-height: 1; color: #444; }

/* Title slide — live type over the branded background. The text block is
   left-aligned and width-limited so it clears the motif in the lower right. */
.reveal .slides section.title { text-align: left; }
.reveal .slides section.title .titlebox { max-width: 82%; }
.reveal .slides section.title h1 { color: #fff; font-size: 1.75em; line-height: 1.08;
                                   margin: 0 0 0.35em 0; text-shadow: 0 2px 12px rgba(0,0,0,0.35); }
.reveal .slides section.title .tagline { color: #9FC5E8; font-size: 0.62em; font-weight: 700;
                                   letter-spacing: 0.04em; margin: 0 0 2.2em 0; }
.reveal .slides section.title .byline { color: #EDEEEF; font-size: 0.6em; font-weight: 700;
                                   margin: 0 0 0.45em 0; }
.reveal .slides section.title .when { color: #b9cde6; font-size: 0.52em; margin: 0; }

/* The theme's footer branding and slide number are dark, drawn for white
   slides. Reverse them to white while a dark divider or the title is on screen. */
.reveal:has(.slides section.section.present) .slide-footer img,
.reveal:has(.slides section.title.present) .slide-footer img { filter: brightness(0) invert(1); }
.reveal:has(.slides section.section.present) .slide-number,
.reveal:has(.slides section.title.present) .slide-number { color: #EDEEEF; }
</style>

<!-- 000 — Title -->
<!-- Background is intro-ai-000.png with the baked-in title, e-mail and date
     cloned out, so that type is live and editable for the next cohort. -->
{{< slide background-image="/imgs/intro-ai-hugo-slide-images/intro-ai-000-bg.png" class="title" >}}

<div class="titlebox">

# Introduction to Generative AI

<p class="tagline">Define &nbsp;&middot;&nbsp; De-mystify &nbsp;&middot;&nbsp; Deploy &nbsp;&middot;&nbsp; Develop</p>

<!-- <p class="byline">Péter Molnár &nbsp;&middot;&nbsp; pmolnar@gsu.edu</p> -->

<p class="when">EMBA 8160 &mdash; AI for Leaders &nbsp;&middot;&nbsp; Session 1</p>

</div>

{{% note %}}
- Welcome. One session, five parts: Define, De-mystify, Deploy, De-risk, Develop.
- Goal is not to make you engineers — it is to make you able to ask the right questions of the people building this.
{{% /note %}}

***

<!-- 002 — Outline: the five D's -->
{{< slide >}}

# Outline

<ol class="outline">
<li><span class="term">Define</span>: Introduce and explain the concept of Generative AI.</li>
<li><span class="term">De-mystify</span>: Break down the components of Generative AI to make them understandable.</li>
<li><span class="term">Deploy</span>: Explore the business applications of Generative AI and how they can be implemented.</li>
<li><span class="term">Develop</span>: Look into future prospects and innovations in the field of Generative AI.</li>
</ol>

{{% note %}}
- **Define** what the words mean, **De-mystify** the machinery, **Deploy** it in the business, **De-risk** the exposure, **Develop** what comes next.
- De-risk is covered in depth in the Responsible AI session; today runs Define through Develop.
{{% /note %}}

***

<!-- ===== DEFINE ===== -->
<!-- 003 — Section divider: DEFINE -->
{{< slide background-color="#1F4099" class="section" >}}

<h1><span class="de">DE</span> FINE</h1>

{{% note %}}
Part one: vocabulary. Most disagreements about AI strategy are really disagreements about definitions.
{{% /note %}}

***

<!-- 004 — What is Artificial Intelligence? -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-004.png" >}}
<h1></h1>

{{% note %}}
- Two classic definitions: Kurzweil (1990) frames AI by the *task*; Luger and Stublefield (1993) frame it by the *behavior*.
- The map shows AI is an umbrella: machine learning, planning, robotics, NLP, expert systems, speech, vision.
- Generative AI is one narrow branch — deep learning inside machine learning. Keep that proportion in mind when vendors say "AI".
{{% /note %}}

***

<!-- 005 — Desk Set (1957): the office computer arrives -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-005.png" >}}
<h1></h1>

{{% note %}}
- 1957: EMERAC arrives in the research department and the staff assume they are about to be replaced.
- The anxiety pattern is 70 years old and repeats with every wave. Worth remembering when your own teams react.
{{% /note %}}

***

<!-- 006 — Text-based adventure game (Zork) -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-006.png" >}}
<h1></h1>

{{% note %}}
- Zork felt like conversation but accepted only three command shapes: basic, verb-object, verb-object-prep-object.
- A hand-written grammar, not understanding — the illusion breaks the moment you step outside the grammar.
- Contrast with an LLM, which has no fixed command list at all.
{{% /note %}}

***

<!-- 007 — Blocks World — Terry Winograd, 1971 -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-007.png" >}}
<h1></h1>

{{% note %}}
- SHRDLU resolved pronouns, asked clarifying questions, and tracked what it was holding — genuinely impressive dialogue.
- It worked because the world was tiny: a few blocks and pyramids, fully specified.
- The lesson that shaped the next 30 years: closed worlds are tractable, open worlds are not.
{{% /note %}}

***

<!-- 008 — WarGames (1983) -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-008.png" >}}
<h1></h1>

{{% note %}}
- 1983: the public image of AI becomes an autonomous system with real-world authority and no human in the loop.
- Same governance question we now ask about agents: what can it do without asking?
{{% /note %}}

***

<!-- 009 — IBM Watson competes on Jeopardy -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-009.png" >}}
<h1></h1>

{{% note %}}
- 2011: Watson beats Jennings and Rutter, winning &#36;77,147 — a landmark for natural language processing.
- Strength was speed and answer-probability; weakness was ambiguous clues.
- Note this was retrieval and scoring over a curated database, not generation. Different machine from what we use today.
{{% /note %}}

***

<!-- 010 — Acting Humanly: the Turing Test -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-010.png" >}}
<h1></h1>

{{% note %}}
- Turing replaces "can machines think?" with a game you can actually score.
- The original Imitation Game is about a man and a woman fooling an interrogator; the machine version substitutes for player A.
- Note what it measures: indistinguishable *behavior* through a text channel. Not understanding, not consciousness. That distinction still matters commercially.
{{% /note %}}

***

<!-- 011 — Types of Artificial Intelligence — ANI, AGI, ASI -->
{{< slide class="fs66" >}}

# Types of Artificial Intelligence

<div class="cols3">
<div>
<p class="sub">Artificial Narrow Intelligence (ANI)</p>
<div class="card"><span class="hd">Definition</span>Performs specific tasks; limited to pre-defined functions.</div>
<div class="card"><span class="hd">Example</span>Voice assistants, recommendation systems, self-driving cars.</div>
</div>
<div>
<p class="sub">Artificial General Intelligence (AGI)</p>
<div class="card"><span class="hd">Definition</span>Capable of understanding and learning any intellectual task a human can do.</div>
<div class="card"><span class="hd">Example</span>Theoretical; not yet achieved.</div>
</div>
<div>
<p class="sub">Artificial Super Intelligence (ASI)</p>
<div class="card"><span class="hd">Definition</span>Surpasses human intelligence in all areas.</div>
<div class="card"><span class="hd">Concerns</span>Raises ethical and safety issues; currently speculative.</div>
</div>
</div>

{{% note %}}
- Everything you can buy today is ANI — narrow, however impressive the demo.
- AGI is a research goal, ASI is speculation. Most public AI anxiety is about the third column; most business decisions are about the first.
- When a vendor's pitch quietly slides from column one to column two, that is your cue to ask for the benchmark.
{{% /note %}}

***

<!-- 012 — Four approaches: think/act, humanly/rationally -->
{{< slide class="fs52" >}}

# Four Ways to Define AI

<div class="grid2x2">
<div class="card">
<span class="hd">Think like humans</span>
Aim <strong>to replicate the cognitive processes of humans</strong>, including reasoning, learning, understanding, and problem-solving.
<p>Creating AI that can <strong>model human cognition</strong>, such as cognitive architectures and some natural language processing applications that attempt to <strong>simulate the way humans understand and process</strong> language.</p>
</div>
<div class="card">
<span class="hd">Act like humans</span>
Designed to <strong>mimic</strong> human behavior and actions through interactions that <strong>feel natural</strong>.
<p>Alan Turing suggests we should ask if the machine can win a game, called the "Imitation Game".</p>
</div>
<div class="card">
<span class="hd">Think rationally</span>
<strong>Formalize "correct" reasoning using a mathematical model</strong> (e.g. of deductive reasoning).
<p>Logic-programs <strong>encode knowledge in formal logical</strong> statements and use mathematical deduction to perform reasoning.</p>
<p>Formalizing common sense knowledge is difficult. General deductive inference is computationally intractable.</p>
</div>
<div class="card">
<span class="hd">Act rationally</span>
Agent <strong>that perceives its environment</strong> and can execute <strong>actions to change it</strong>. Agents have inherent goals that they want to achieve (e.g. survive, reproduce).
<p>Though, true maximization of goals requires omniscience and unlimited computational abilities. Limited rationality involves <strong>maximizing goals</strong> within the computational and other <strong>resources available</strong>.</p>
</div>
</div>

<p class="refs">Framework from Stuart Russell's and Peter Norvig's textbook, <em>Artificial Intelligence: A Modern Approach</em>.</p>

{{% note %}}
- Two axes: thinking versus acting, human-like versus rational. Four quadrants, four different research programs.
- Symbolic AI lived in "think rationally" and hit the common-sense wall. LLMs live in "act like humans".
- "Act rationally" — the agent quadrant — is where the industry is heading now, and it is the one with the governance problem.
{{% /note %}}

***

<!-- ===== HISTORY OF AI ===== -->
<!-- 013 — Section divider: History of Artificial Intelligence -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-013.png" >}}
<h1></h1>

{{% note %}}
A short history — because the field has been through this hype cycle before, and the pattern is instructive.
{{% /note %}}

***

<!-- 014 — The History of AI in Business Decision Making -->
{{< slide class="fs48" >}}

# The History of AI in Business Decision Making

<div class="cols4">
<div>
<p class="sub">1950s–1960s</p>
<div class="card"><span class="hd">Theoretical Foundations</span>
<ul><li>Early AI research focused on symbolic processing and rule-based systems.</li>
<li>AI was primarily a subject of academic research and speculation.</li></ul>
</div>
</div>
<div>
<p class="sub">1970s–1980s</p>
<div class="card"><span class="hd">Expert Systems</span>
<ul><li>Introduction of expert systems designed to emulate human decision-making.</li>
<li>Used in various domains, including medical diagnosis and geological exploration.</li></ul>
</div>
</div>
<div>
<p class="sub">Late 1980s–1990s</p>
<div class="card"><span class="hd">AI Winter and Rise of Machine Learning</span>
<ul><li>Period of reduced funding and interest in AI, known as the "AI Winter."</li>
<li>Emergence of machine learning, focusing on data-driven AI applications.</li></ul>
</div>
</div>
<div>
<p class="sub">2000s</p>
<div class="card"><span class="hd">Internet and Big Data</span>
<ul><li>Explosion of the internet and availability of big data.</li>
<li>Advancements in search engines, recommendation systems, and targeted advertising.</li></ul>
</div>
</div>
<div>
<p class="sub">2010s</p>
<div class="card"><span class="hd">Deep Learning Breakthroughs</span>
<ul><li>Deep learning enables remarkable feats in image and speech recognition, natural language processing.</li>
<li>AI applications begin transforming industries with autonomous vehicles and advanced analytics.</li></ul>
</div>
</div>
<div>
<p class="sub">2020s</p>
<div class="card"><span class="hd">Current Applications and Strategic Integration</span>
<ul><li>AI becomes integral to strategic planning and operations.</li>
<li>Businesses leverage AI for competitive advantages, predictive analytics, and customer relationship management.</li></ul>
</div>
</div>
<div>
<p class="sub">Future Prospects</p>
<div class="card"><span class="hd">Ongoing Impact and Innovation</span>
<ul><li>Generative AI and emerging technologies promise new capabilities.</li>
<li>AI continues to evolve, shaping business strategies and operations further.</li></ul>
</div>
</div>
</div>

{{% note %}}
- Note the AI Winter in the middle: funding collapsed when expert systems failed to scale. Hype cycles in this field have a history of ending.
- The inflection is the 2000s — not a smarter algorithm, but the internet producing enough data to learn from.
- Ask yourself where your organization sits on this timeline. Many are still in the 2000s analytics era.
{{% /note %}}

***

<!-- 015 — ELIZA -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-015.png" >}}
<h1></h1>

{{% note %}}
- Weizenbaum at MIT CSAIL: ELIZA reflects your input back as a question. Pure pattern substitution, no model of meaning.
- People confided in it anyway. Weizenbaum was disturbed enough by that to spend his career warning about it.
- The "ELIZA effect" — attributing understanding to a system that has none — is the single most relevant historical lesson for how your staff will react to a chatbot.
{{% /note %}}

***

<!-- 016 — MYCIN -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-016.png" >}}
<h1></h1>

{{% note %}}
- Stanford, 1974: a rule-based expert system for medical diagnosis, and reportedly better than junior doctors.
- Architecture is worth noting: knowledge base plus rules engine, knowledge elicited from a human expert.
- It was never deployed clinically — liability and workflow, not accuracy, were the blockers. That is still the usual reason good models never ship.
{{% /note %}}

***

<!-- 017 — Samuel's Checker Program -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-017.png" >}}
<h1></h1>

{{% note %}}
- Arthur Samuel, 1952: the program improved as it played and eventually beat its own creator.
- First convincing demonstration that a machine can learn rather than be programmed.
- It also produced the first wave of "the machines will surpass us" anxiety, and pushed the field toward non-symbolic, learning-based AI.
{{% /note %}}

***

<!-- 018 — Logic Theorist -->
{{< slide class="fs66" >}}

# Logic Theorist

<p>Created by <strong>Allen Newell, Herbert Simon, and Cliff Shaw in 1955–56</strong>, the Logic Theorist was an early <span class="term">symbolic AI program capable of proving 38 elementary theorems</span> from Whitehead and Russell's <em>Principia Mathematica</em>.</p>

<p>This work laid the <strong>groundwork</strong> for the development of <span class="term">automated theorem provers</span> and <span class="term">knowledge-based systems</span>.</p>

<p class="refs">Background: Newell and Simon's Logic Theorist — historical background and impact on cognitive modeling, <em>Proceedings of the Human Factors and Ergonomics Society Annual Meeting</em>, 2006.</p>

{{% note %}}
- Often called the first artificial intelligence program — it predates the term itself, coined at Dartmouth in 1956.
- It did not search exhaustively; it used heuristics to prune, which is the idea that made symbolic AI practical.
- For one theorem it found a proof shorter than Russell and Whitehead's own.
{{% /note %}}

***

<!-- 019 — General Problem Solver (GPS) -->
{{< slide class="fs66" >}}

# General Problem Solver (GPS)

<p>Also developed by <strong>Newell, Simon, and Shaw</strong>, GPS was a <span class="term">domain-independent problem solver</span> that used <span class="term">state-space search</span> and <span class="term">means-ends analysis</span> to solve problems represented with formal operators.</p>

<p>It was a significant step towards <span class="term">creating machines that could solve a wide variety of problems</span> using general intelligence.</p>

<p class="refs">RAND Corporation report P-1584, "Report on a General Problem-Solving Program", 1959.</p>

{{% note %}}
- The ambition in the name: separate the *problem-solving method* from the *problem*, so one engine handles anything you can formalize.
- Means-ends analysis — measure the gap between current and goal state, pick the operator that reduces it — is still how planning modules in agents work.
- It failed on real problems because formalizing them turned out to be the hard part. The knowledge, not the search, was the bottleneck.
{{% /note %}}

***

<!-- ===== DE-MYSTIFY ===== -->
<!-- 020 — Section divider: DE-MYSTIFY -->
{{< slide background-color="#1F4099" class="section" >}}

<h1><span class="de">DE</span> MYSTIFY</h1>

{{% note %}}
Part two: open the box. You do not need the mathematics, but you do need to know what the machine is actually doing.
{{% /note %}}

***

<!-- 021 — Generative AI ~ Machine Learning + Data -->
{{< slide class="fs66" >}}

# Generative AI ~ Machine Learning + Data

<div class="cols2">
<div>
<div class="card">Subset of AI <strong>capable of producing new content</strong> (text, images, videos, audio)</div>
<div class="card"><strong>Trained on large datasets</strong> to understand patterns, structures, and features</div>
<div class="card">Generates <strong>original outputs resembling</strong> training data but not exact copies</div>
</div>
<div>
<div class="card">Useful in creation of <strong>content, images, natural language, drug discovery, personalized recommendations</strong> etc.</div>
<div class="card">Encompasses <strong>various neural-network model architectures</strong> (Generative Adversarial Networks, Variational Autoencoders, Transformer-based models)</div>
<div class="card">Demonstrated capabilities in <strong>generating coherent and contextually relevant</strong> content</div>
</div>
</div>

{{% note %}}
- The definition that matters commercially: it produces *new* artifacts rather than classifying existing ones.
- "Resembling training data but not exact copies" is the sentence your legal team will care about — it is also why provenance is hard to prove either way.
- Generative AI is machine learning plus scale of data. No new theory; mostly more data and more compute.
{{% /note %}}

***

<!-- 022 — Decision-making with Analytics and Machine Learning -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-022.png" >}}
<h1></h1>

{{% note %}}
- The full pipeline: sources, ETL into an analytics base table, supervised training, then inference feeding a decision.
- Two distinct loops — training happens rarely and expensively; inference happens constantly and cheaply.
- Most of the cost and most of the failure modes are on the left, in the data plumbing, not in the model.
{{% /note %}}

***

<!-- 023 — Types of Machine Learning -->
{{< slide class="fs66" >}}

# Types of Machine Learning

<div class="cols3">
<div>
<p class="sub">Supervised</p>
<p>Is trained on a labeled dataset, where the input data is paired with corresponding output labels.</p>
<p>The goal is for the model to learn the mapping from inputs to outputs, allowing it to make predictions on new, unseen data.</p>
<p><strong>Example</strong>: Predicting house prices based on features such as square footage, number of bedrooms, and location, using a dataset where each house's price is provided.</p>
</div>
<div>
<p class="sub">Unsupervised</p>
<p>Deals with unlabeled data, and the algorithm aims to discover patterns, relationships, or structures within the data without explicit guidance.</p>
<p>It explores the inherent structure of the dataset.</p>
<p><strong>Example</strong>: Clustering customer data based on purchasing behavior, where the algorithm groups customers with similar buying patterns together without any predefined labels.</p>
</div>
<div>
<p class="sub">Reinforcement</p>
<p>Involves an agent interacting with an environment and learning to make decisions by receiving feedback in the form of rewards or penalties.</p>
<p>The agent learns to take actions that maximize cumulative rewards over time.</p>
<p><strong>Example</strong>: Teaching a computer program to play a game. The program takes actions in the game environment (e.g., moving a character) and receives rewards or penalties based on its performance, learning to improve its strategy over time.</p>
</div>
</div>

{{% note %}}
- Supervised learning needs labels, and labels are the expensive part — usually human effort you have to budget for.
- Unsupervised finds structure you did not ask for, which is useful for discovery and dangerous for decisions.
- Reinforcement learning needs a reward signal you can define. Getting the reward wrong is how you get a system that games the metric.
- LLM pre-training is none of these three exactly — it is self-supervised, which we come to shortly.
{{% /note %}}

***

<!-- 024 — Neural Networks -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-024.png" >}}
<h1></h1>

{{% note %}}
- Loosely inspired by biology: layers of nodes, each passing a weighted signal forward.
- "Learning" means adjusting connection weights — via backpropagation and gradient descent — to reduce error.
- The biological analogy is marketing more than science. Treat it as a flexible function fitter, not a brain.
{{% /note %}}

***

<!-- 025 — A Brief History of Neural Nets -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-025.png" >}}
<h1></h1>

{{% note %}}
- Backpropagation dates to Werbos in 1974; the Transformer to 2017; ChatGPT to 2022. The theory ran decades ahead of the deployment.
- Hinton appears three times across forty years — through two AI winters. Persistence, not sudden genius.
- What changed recently was GPUs and data volume, which is why the curve looks vertical at the right edge.
{{% /note %}}

***

<!-- 026 — Training Neural Networks -->
{{< slide class="fs63" >}}

# Training Neural Networks

<div class="cols2">
<div>
<p class="sub">Training Steps</p>
<p><strong>Data Collection:</strong> Gather a large, diverse dataset relevant to the task.</p>
<p><strong>Data Preprocessing:</strong> Clean, normalize, possibly augment the data.</p>
<p><strong>Model Design:</strong> Choose an appropriate neural network architecture for the task.</p>
<p><strong>Weight Initialization:</strong> Initialize weights randomly.</p>
<p><strong>Training Loop:</strong></p>
<ol>
<li>Pass input data through the network to obtain predictions.</li>
<li>Compute the loss by comparing predictions with true labels using a loss function.</li>
<li>Calculate gradients of the loss with respect to the weights.</li>
<li>Adjust the weights in the direction that minimally reduces the loss, typically using an optimizer like SGD, Adam, etc.</li>
</ol>
<p><strong>Evaluation:</strong> Assess model performance using a validation set and adjust hyperparameters as needed.</p>
</div>
<div>
<p class="sub">Challenges / Risks</p>
<p><strong>Overfitting/Underfitting:</strong> The model learns noise and details from the training data that do not generalize, or the model is too simple to capture the underlying pattern in the data.</p>
<p><strong>Improper Initialization:</strong> Poor weight initialization can lead to slow convergence or training stagnation.</p>
<p><strong>Vanishing/Exploding Gradients:</strong> Gradients become too small or too large, hindering effective weight updates.</p>
<p><strong>Class Imbalance:</strong> Disproportionate representation of classes can bias the model towards the majority class.</p>
<p><strong>Poor Hyperparameter Choices:</strong> Incorrectly chosen hyperparameters can lead to suboptimal training results.</p>
<p><strong>Inadequate Evaluation:</strong> Not using proper evaluation metrics or validation techniques can misrepresent model performance.</p>
<p><strong>Computational Constraints:</strong> Large models require significant computational resources, which can limit experimentation.</p>
</div>
</div>

{{% note %}}
- The loop is mechanical: predict, measure error, adjust, repeat. Everything interesting is in the data and the loss function.
- Overfitting is the one to internalize — a model that scores well in the lab and fails in production has usually memorized rather than generalized.
- Class imbalance is where bias enters quietly. If the training data under-represents a group, the model will too.
- Insist on seeing validation results on held-out data, never training accuracy.
{{% /note %}}

***

<!-- 027 — Deep Learning -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-027.png" >}}
<h1></h1>

{{% note %}}
- "Deep" simply means many layers. Each layer extracts more abstract features than the one below.
- The diagram shows a convolutional vision stack: edges, then textures, then parts, then objects.
- The payoff is that you stop hand-engineering features — the network learns them. That is what made vision and speech work.
{{% /note %}}

***

<!-- 028 — Deep Neural Networks -->
{{< slide class="fs52" >}}

# Deep Neural Networks

<div class="cols2">
<div>
<p class="sub">Differences</p>
<p><strong>Depth of Layers</strong>: Deep learning networks have many hidden layers (deep architecture), whereas regular neural networks typically have fewer hidden layers.</p>
<p><strong>Feature Learning:</strong> Deep learning networks automatically learn hierarchical feature representations from raw data, while regular neural networks may require manual feature engineering.</p>
<p><strong>Complexity and Abstraction</strong>: Deep learning models can capture more complex patterns and higher levels of abstraction compared to regular neural networks.</p>
<p><strong>Computational Resources</strong>: Deep learning models generally require more computational power and data for training due to their complexity and depth.</p>
<p><strong>Performance</strong>: On tasks involving large-scale data and complex patterns, deep learning networks often outperform regular neural networks, especially in fields like computer vision and natural language processing.</p>
</div>
<div>
<p class="sub">History</p>
<p><strong>1998 — LeNet-5</strong>: Digit recognition, approximately 60,000 parameters.</p>
<p><strong>2012 — AlexNet</strong>: ImageNet competition, image classification. 60 million parameters.</p>
<p><strong>2014 — GoogleNet (Inception v1)</strong>: ImageNet competition, 22 layers deep, 4 million parameters, introducing the inception module.</p>
<p><strong>2015 — ResNet (Microsoft)</strong>: ImageNet competition, 152 layers and introduced residual learning to ease training of networks.</p>
<p><strong>2018 — BERT (Google)</strong>: language representation model, 110 million parameters for base model, 340 million for large model. It was used for NLP tasks.</p>
<p><strong>2019 — GPT-2 (OpenAI)</strong>: large-scale unsupervised language model, 1.5 billion parameters and was used for various NLP tasks.</p>
<p><strong>2020 — GPT-3 (OpenAI)</strong>: autoregressive language model, had 175 billion parameters, strong performance on many NLP tasks.</p>
<p><strong>2022 — PaLM (Google)</strong>: language model with 540 billion parameters, trained on a high-quality text corpus, state-of-the-art few-shot learning results.</p>
<p><strong>2023 — GPT-4 (OpenAI)</strong>: multimodal LLM, had 1.76 trillion parameters and could take image and text as inputs, producing text outputs.</p>
</div>
</div>

{{% note %}}
- Follow the parameter counts down the right column: 60 thousand to 1.76 trillion in 25 years.
- That is roughly seven orders of magnitude, and it is the whole story of why capability jumped.
- It is also why only a handful of organizations train frontier models — the rest of us consume them. That is the buy-versus-build decision we reach later.
{{% /note %}}

***

<!-- 029 — Data Sources -->
{{< slide class="fs48" >}}

# Data Sources

<div class="cols2">
<div>
<p class="sub">Images</p>
<p><strong>ImageNet</strong>: Used for visual object recognition software research, over 14 million images and thousands of object categories.</p>
<p><strong>COCO (Common Objects in Context)</strong>: Features object detection, segmentation, and captioning, over 200,000 labelled images, 80 categories.</p>
<p><strong>PASCAL VOC (Visual Object Classes)</strong>: Images for classification, detection, and segmentation tasks with 20 different object categories.</p>
<p><strong>CIFAR-10 and CIFAR-100</strong>: Two datasets with 60,000 32x32 color images in 10 and 100 classes, respectively, used for object recognition.</p>
<p><strong>Cityscapes</strong>: Focuses on semantic understanding of urban street scenes, with high-quality pixel-level annotations of 5,000 images in 50 different cities.</p>
<p><strong>LSUN (Large-scale Scene Understanding)</strong>: Contains around one million labeled images for each of 10 scene categories and 20 object categories.</p>
<p><strong>Places</strong>: A scene-centric database with more than 10 million images depicting 400+ unique scene categories.</p>
<p><strong>Kinetics</strong>: A large-scale, high-quality YouTube videos.</p>
<p><strong>Open Images Dataset</strong>: About ~9 million images, with image-level labels, object bounding boxes, object segmentation masks, and visual relationships.</p>
<p><strong>MS COCO (Microsoft Common Objects in Context)</strong>: A large-scale dataset for object detection, segmentation, and captioning.</p>
</div>
<div>
<p class="sub">Text</p>
<p><strong>BooksCorpus and English Wikipedia</strong>: Used for BERT and its variants, providing a diverse range of topics and language styles.</p>
<p><strong>Common Crawl</strong>: web crawl, used by GPT, RoBERTa, offering a broad snapshot of the internet's text.</p>
<p><strong>WebText2</strong>: Utilized by OpenAI for training GPT models, compiled from web pages and designed to represent a wide array of internet text.</p>
<p><strong>CC-NEWS</strong>: News articles, used in conjunction with other corpora like BooksCorpus and English Wikipedia for training models like RoBERTa.</p>
<p><strong>STORIES</strong>: A subset of Common Crawl focusing on narrative content, used for training language models to understand and generate story-like text.</p>
<p><strong>Reddit</strong>: Derived from Reddit posts, used for training GPT-2 and GPT-3 to understand conversational language and diverse topics.</p>
<p><strong>Giga5</strong>: Part of the training dataset for XLNet, consisting of English Gigaword (5th Edition), a comprehensive archive of newswire text.</p>
<p><strong>ClueWeb</strong>: Used by XLNet, web pages intended for research on information retrieval, language modeling, and web search.</p>
<p><strong>Common Crawl (filtered)</strong>: A refined version of the Common Crawl dataset, filtered for quality and relevance, used for training GPT-3.</p>
<p><strong>GitHub code</strong>: A corpus of public GitHub repositories used by models like CODEX for understanding and generating programming code.</p>
</div>
</div>

{{% note %}}
- These are the corpora the frontier models were actually trained on — mostly scraped web text and public image sets.
- Two executive implications: you cannot audit what is in Common Crawl, and copyright status of much of it is unresolved and in active litigation.
- Also note what is absent: your industry's proprietary data. That gap is exactly where your competitive advantage lives.
{{% /note %}}

***

<!-- 030 — Large Language Models -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-030.png" >}}
<h1></h1>

{{% note %}}
- Four axes to classify any model you are offered: parameters, type, availability, originality.
- **Type** is the one people miss: a foundation model is not chat-ready. Instruction- and chat-tuned variants are different products.
- **Availability** — public weights versus private API — determines whether you can run it in your own environment. That drives the data-residency conversation.
{{% /note %}}

***

<!-- ===== BUILDING LLMs ===== -->
<!-- 031 — Section divider: Building LLMs -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-031.png" >}}
<h1></h1>

{{% note %}}
How these models are actually assembled — data cleaning, tokenization, architecture, pre-training, fine-tuning, alignment.
{{% /note %}}

***

<!-- 032 — LLM Variations -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-032.png" >}}
<h1></h1>

{{% note %}}
- One transformer stack, many task shapes: classification, entailment, similarity, multiple choice.
- The trick is formatting the input with delimiters so different tasks fit the same architecture.
- This is the ancestor of prompting — you are still formatting input to steer one general model.
{{% /note %}}

***

<!-- 033 — Data Cleaning -->
{{< slide class="fs66" >}}

# Data Cleaning

<div class="cols2">
<div>
<p class="sub">Reasons</p>
<p><strong>Improving Model Performance:</strong> Clean data helps in training more accurate and reliable models.</p>
<p><strong>Reducing Noise:</strong> Prevent model from learning incorrect patterns due to irrelevant or noisy data, may lead to better generalization to new, unseen data.</p>
<p><strong>Handling Data Sparsity:</strong> Ensure that models can handle rare or unseen words or n-grams effectively.</p>
<p><strong>Mitigating Bias:</strong> Reducing biases present in the training data, which is crucial for building fair and unbiased models.</p>
<p><strong>Enhancing Model Robustness:</strong> Eliminating duplicates and inconsistencies contribute to the robustness of the model, making it less prone to overfitting and more stable in its predictions.</p>
</div>
<div>
<p class="sub">Techniques</p>
<p><u>Document/Sentence Level</u></p>
<ul>
<li><strong>Data Filtering:</strong> Removing low-quality text entries that contain excessive spelling and grammatical errors to improve the overall quality of the dataset.</li>
<li><strong>Deduplication:</strong> Eliminating duplicate sentences or documents in the dataset to prevent the model from overfitting on repeated instances of the same or similar text.</li>
</ul>
<p><u>Word Level</u></p>
<ul>
<li><strong>Text Preprocessing:</strong> Standardizing text by converting to lowercase, removing special characters, and stemming words to their root form to reduce the complexity of the language the model needs to learn.</li>
</ul>
</div>
</div>

{{% note %}}
- Unglamorous and decisive. Garbage in, confidently-worded garbage out.
- "Mitigating bias" is listed as a data-cleaning step, not an ethics afterthought — that is the right place for it.
- Deduplication matters more than people expect: repeated text gets memorized and can be regurgitated verbatim, which is a leak risk.
{{% /note %}}

***

<!-- 034 — Tokenization -->
{{< slide class="fs66" >}}

# Tokenization

<div class="cols2">
<div>
<p class="sub">Handling Vocabulary</p>
<ul>
<li>Converts text into tokens (words, subwords, characters).</li>
<li>Manages <strong>vocabulary size</strong> for model learning.</li>
<li>Ensures efficient text processing and understanding.</li>
</ul>
<p class="sub">Dealing with Out-of-Vocabulary (OOV) Words</p>
<ul>
<li>Uses strategies like <em>BytePairEncoding</em> (BPE), <em>WordPieceEncoding</em>, and <em>SentencePieceEncoding</em>.</li>
<li>Breaks down <strong>rare/unseen words into sub-word</strong> units.</li>
<li>Reduces OOV issues and improves generalization.</li>
</ul>
<p class="sub">Efficient Training and Inference</p>
<ul>
<li>Breaks text into smaller units.</li>
<li>Reduces computational complexity.</li>
<li>Enables training on larger datasets and faster inference.</li>
</ul>
</div>
<div>
<p class="sub">Capturing Semantic and Syntactic Information</p>
<ul>
<li>Subwords capture linguistic units (prefixes, suffixes).</li>
<li>Enhances understanding of language structure and meaning.</li>
</ul>
<p class="sub">Supporting Multilingual Models</p>
<ul>
<li>Language-agnostic tokenization (e.g., SentencePiece).</li>
<li>Tokenizes multiple languages without specific rules.</li>
<li>Essential for multilingual LLMs understanding/generating text across languages.</li>
</ul>
</div>
</div>

{{% note %}}
- The model never sees words. It sees token IDs — integers into a fixed vocabulary.
- This explains several famous failures: counting letters, arithmetic on long numbers, spelling puzzles. The model cannot see inside a token.
- Practical consequence: you are billed per token, and non-English text often costs more tokens for the same meaning.
{{% /note %}}

***

<!-- 035 — Tokenization Examples -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-035.png" >}}
<h1></h1>

{{% note %}}
- Character tokenization gives a tiny vocabulary but very long sequences; word tokenization gives short sequences but a huge vocabulary and an OOV problem.
- Subword tokenization is the compromise everyone actually uses.
{{% /note %}}

***

<!-- 036 — The tokenization process: subwords to token IDs -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-036.png" >}}
<h1></h1>

{{% note %}}
- Follow the pipeline: subword split, add CLS and SEP markers, map to integers, feed the model.
- "Demystifying" becomes dem / ##yst / ##ifying — three tokens for one word. That is why token counts exceed word counts.
{{% /note %}}

***

<!-- 037 — Position Encoding -->
{{< slide class="fs66" >}}

# Position Encoding

<div class="cols2">
<div>
<p>Consider the sentence</p>
<blockquote>"I walked to the store after I left home."</blockquote>
<p>Without position encoding, the model might not distinguish between "I walked to the store" and "I left home" as <strong>sequential actions</strong>, potentially confusing the order of events.</p>
<p>With proper position encoding, the model can understand that "left home" came before "walked to the store," <strong>preserving the narrative's temporal sequence</strong>.</p>
</div>
<div>
<p>Position encoding is required of Large Language Models (LLMs) and other <span class="term">transformer-based architectures</span> because these models do not inherently capture the sequential order of input tokens.</p>
<p>Unlike <span class="term">Recurrent Neural Networks (RNNs) or Long Short-Term Memory networks (LSTMs), which process sequences</span> in order and thus have an intrinsic understanding of position, transformers process input tokens in parallel.</p>
<p>Position encoding is necessary to provide the model with <span class="term">information about the order of tokens</span>, which is crucial for understanding language where the meaning often depends on the sequence of words.</p>
<p>Position encoding allows the model to understand word order and the <span class="term">relationships between words in a sentence</span>, which is essential for tasks like translation, question answering, and text generation.</p>
</div>
</div>

{{% note %}}
- Transformers read all tokens at once — that parallelism is what makes them fast to train, and it is why order has to be added back in explicitly.
- Without it the model sees a bag of words. "Dog bites man" and "man bites dog" would be identical.
- This is also why context windows have limits: position information has to be encoded for every slot.
{{% /note %}}

***

<!-- 038 — LLM Architectures: Transformers -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-038.png" >}}
<h1></h1>

{{% note %}}
- The 2017 "Attention Is All You Need" architecture — encoder on the left, decoder on the right.
- Self-attention lets every token weigh every other token, which is how long-range context is captured.
- One sentence for the boardroom: attention made training parallelizable, parallel training made scale affordable, scale produced the capability jump.
{{% /note %}}

***

<!-- 039 — Model Pre-training -->
{{< slide class="fs66" >}}

# Model Pre-training

<div class="cols2">
<div>
<p>Model pre-training in the context of Large Language Models (LLMs) involves training the model on a massive amount of (usually) unlabeled text data, typically in a <span class="term">self-supervised manner</span>.</p>
<p>This foundational step allows LLMs to <span class="term">acquire fundamental language understanding capabilities</span>, which can be useful across a wide range of language-related tasks.</p>
</div>
<div>
<ol>
<li><strong>Data Preparation:</strong> The model is exposed to a vast corpus of text data, which could include web pages, books, articles, and other forms of written language.</li>
<li><strong>Self-Supervised Learning:</strong> The model learns by predicting parts of the input data. E.g. words in the input text are masked or hidden. This process enables the model to learn word meanings, grammar, and the ability to form coherent text.</li>
<li><strong>Adjusting Model Weights:</strong> The model learns by gradually adjusting its weights to minimize the difference between its predictions and the actual data.</li>
<li><strong>Iteration:</strong> Passing the entire dataset through the model multiple times (epochs).</li>
<li><strong>Outcome:</strong> A model that has a general understanding of the language it was trained on.</li>
</ol>
</div>
</div>

{{% note %}}
- Self-supervised is the key word: no human labels needed, the text supplies its own answers by hiding parts of itself.
- That is what unlocked training on the entire web — labeling at that scale would be impossible.
- The output of this stage is a foundation model: fluent, knowledgeable, and not yet useful or safe as a product.
{{% /note %}}

***

<!-- 040a — Common Self-supervised Training Methods (text) -->
{{< slide class="fs66" >}}

# Common Self-supervised Training Methods

<div class="cols2">
<div>
<p><span class="term">Masked Language Modeling (MLM):</span> Randomly masking out tokens in the input and training the model to predict the masked tokens based on their context.</p>
<p><span class="term">Autoregressive Language Modeling:</span> Training the model to predict the next token in a sequence given the previous tokens, thus learning to generate text.</p>
<p><span class="term">Next Sentence Prediction (NSP):</span> Given a pair of sentences, the model predicts if the second sentence is the subsequent sentence in the original document, used in early models like BERT.</p>
</div>
<div>
<p><span class="term">Contrastive Learning:</span> Learning representations by contrasting positive pairs (related data points) against negative pairs (unrelated data points).</p>
<p><span class="term">Replaced Token Detection (RTD):</span> Training a model to distinguish between original tokens and those replaced by a generator in the input sequence, as used in ELECTRA.</p>
</div>
</div>

{{% note %}}
- Five objectives, but two matter commercially: MLM and autoregressive.
- MLM hides tokens and predicts them from both sides — that is BERT, good for understanding.
- Autoregressive predicts the next token from the left only — that is GPT, good for generation.
- The choice of pre-training objective determines what the model is good at. Generation requires autoregression.
{{% /note %}}

***

<!-- 040b — MLM / TLM figure, rebuilt as HTML (was unreadable in the bitmap) -->
{{< slide class="fs66" >}}

# How Masking Works

<div class="tok">
<div class="rl"><b>Masked Language Modeling (MLM)</b></div>
<div></div>
<div class="cell pred">take</div>
<div></div>
<div></div>
<div class="cell pred">[/s]</div>
<div></div>
<div></div>
<div class="cell pred">drink</div>
<div></div>
<div class="cell pred">now</div>
<div></div>
<div></div>
<div></div>
<div class="up">&nbsp;</div>
<div class="up">&uarr;</div>
<div class="up">&nbsp;</div>
<div class="up">&nbsp;</div>
<div class="up">&uarr;</div>
<div class="up">&nbsp;</div>
<div class="up">&nbsp;</div>
<div class="up">&uarr;</div>
<div class="up">&nbsp;</div>
<div class="up">&uarr;</div>
<div class="up">&nbsp;</div>
<div class="up">&nbsp;</div>
<div></div><div class="bar">Transformer</div>
<div></div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="rl">Token<br>embeddings</div>
<div class="cell tokc">[/s]</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">a</div>
<div class="cell tokc">seat</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">have</div>
<div class="cell tokc">a</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">[/s]</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">relax</div>
<div class="cell tokc">and</div>
<div></div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="rl">Position<br>embeddings</div>
<div class="cell posc">0</div>
<div class="cell posc">1</div>
<div class="cell posc">2</div>
<div class="cell posc">3</div>
<div class="cell posc">4</div>
<div class="cell posc">5</div>
<div class="cell posc">6</div>
<div class="cell posc">7</div>
<div class="cell posc">8</div>
<div class="cell posc">9</div>
<div class="cell posc">10</div>
<div class="cell posc">11</div>
<div></div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="rl">Language<br>embeddings</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
</div>
<div class="tok">
<div class="rl"><b>Translation Language Modeling (TLM)</b></div>
<div></div>
<div></div>
<div class="cell pred">curtains</div>
<div class="cell pred">were</div>
<div></div>
<div></div>
<div></div>
<div class="cell pred">les</div>
<div></div>
<div></div>
<div class="cell pred">bleus</div>
<div></div>
<div></div>
<div class="up">&nbsp;</div>
<div class="up">&nbsp;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&nbsp;</div>
<div class="up">&nbsp;</div>
<div class="up">&nbsp;</div>
<div class="up">&uarr;</div>
<div class="up">&nbsp;</div>
<div class="up">&nbsp;</div>
<div class="up">&uarr;</div>
<div class="up">&nbsp;</div>
<div></div><div class="bar">Transformer</div>
<div></div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="up">&uarr;</div>
<div class="rl">Token<br>embeddings</div>
<div class="cell tokc">[/s]</div>
<div class="cell tokc">the</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">blue</div>
<div class="cell tokc">[/s]</div>
<div class="cell tokc">[/s]</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">rideaux</div>
<div class="cell tokc">étaient</div>
<div class="cell tokc">[MASK]</div>
<div class="cell tokc">[/s]</div>
<div></div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="rl">Position<br>embeddings</div>
<div class="cell posc">0</div>
<div class="cell posc">1</div>
<div class="cell posc">2</div>
<div class="cell posc">3</div>
<div class="cell posc">4</div>
<div class="cell posc">5</div>
<div class="cell posc">0</div>
<div class="cell posc">1</div>
<div class="cell posc">2</div>
<div class="cell posc">3</div>
<div class="cell posc">4</div>
<div class="cell posc">5</div>
<div></div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="plus">+</div>
<div class="rl">Language<br>embeddings</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc">en</div>
<div class="cell langc fr">fr</div>
<div class="cell langc fr">fr</div>
<div class="cell langc fr">fr</div>
<div class="cell langc fr">fr</div>
<div class="cell langc fr">fr</div>
<div class="cell langc fr">fr</div>
</div>

<p class="refs">Cross-lingual language model pre-training. MLM uses continuous streams of text; TLM uses pairs of parallel sentences — to predict a masked English word the model can attend to both the English sentence and its French translation.</p>

{{% note %}}
- Walk the bottom three rows first: every token is the sum of three embeddings — what the token is, where it sits, and which language it is in.
- Top row is the task: roughly 15% of tokens are replaced by [MASK] and the model must recover them from the surrounding context, both left and right.
- TLM is the same trick across a sentence pair. To recover the masked English word the model may look at the French, which is how one model learns to align two languages.
- No human labelled any of this. The text supplies its own answers — that is what made training on the whole web possible.
{{% /note %}}

***

<!-- 041 — Text Corpora for Pre-training -->
{{< slide class="fs66" >}}

# Text Corpora for Pre-training

<div class="cols2">
<div>
<p><span class="term">BooksCorpus</span>: A collection of text from books, providing a diverse range of narratives, styles, and vocabulary.</p>
<p><span class="term">English Wikipedia</span>: The entirety of English Wikipedia articles, offering a wide array of knowledge across countless subjects.</p>
<p><span class="term">Common Crawl</span>: A massive web crawl that includes text from billions of web pages, providing a rich and varied source of language use and information.</p>
<p><span class="term">WebText2</span>: A dataset compiled from web pages, designed to represent a wide array of internet text.</p>
<p><span class="term">CC-NEWS</span>: A corpus consisting of news articles, capturing a variety of writing styles and topics from journalistic sources.</p>
</div>
<div>
<p><span class="term">STORIES</span>: A subset of Common Crawl focusing on narrative content, useful for understanding storytelling and narrative structures.</p>
<p><span class="term">Reddit</span>: A dataset derived from Reddit posts, useful for conversational language and a wide range of topics discussed by users.</p>
<p><span class="term">Giga5</span>: Part of the training dataset for XLNet, consisting of English Gigaword (5th Edition), a comprehensive archive of newswire text.</p>
<p><span class="term">ClueWeb</span>: A dataset used by XLNet, consisting of web pages intended for research on information retrieval, language modeling, and web search.</p>
</div>
</div>

{{% note %}}
- Notice the mix: books and Wikipedia for quality, Common Crawl and Reddit for breadth and conversational tone.
- The model's default voice, its blind spots and its cultural assumptions all come from this list.
- None of it is your data. Everything specific to your business has to be added later, by fine-tuning or retrieval.
{{% /note %}}

***

<!-- 042 — Fine-tuning and Instruction Tuning -->
{{< slide class="fs66" >}}

# Fine-tuning and Instruction Tuning

<div class="cols2">
<div>
<p><span class="term">Task-Specific Data</span>: After pre-training on a large corpus, the LLM is fine-tuned using a dataset that is specific to the desired task, which could be anything from sentiment analysis to question-answering. This dataset is usually much smaller than the pre-training corpus and contains labeled data that provides clear examples of the task.</p>
<p><span class="term">Continued Training</span>: During fine-tuning, the model's weights are further adjusted to minimize the loss on the new task-specific dataset. This process involves using an optimization algorithm, such as stochastic gradient descent, to update the weights based on the error the model makes in its predictions.</p>
<p><span class="term">Preserving General Knowledge</span>: Fine-tuning aims to preserve the broad language understanding the model has gained during pre-training while also specializing its knowledge to perform well on the specific task. This is often</p>
</div>
<div>
<p>a delicate balance, as too much fine-tuning can cause the model to "forget" its general capabilities (a phenomenon known as catastrophic forgetting).</p>
<p><span class="term">Hyperparameter Adjustment</span>: Fine-tuning often requires adjusting hyperparameters, such as the learning rate, to ensure that the model's pre-trained knowledge is not overwritten too quickly. The learning rate might be set lower than during pre-training to make smaller, more precise updates to the model's weights.</p>
<p><span class="term">Evaluation and Iteration</span>: The fine-tuned model is evaluated on a validation set to monitor its performance. Based on these results, the model may be fine-tuned iteratively with adjustments to hyperparameters or the training procedure to optimize its performance on the task.</p>
</div>
</div>

{{% note %}}
- Fine-tuning is cheap relative to pre-training — small labeled dataset, short run. This is the part you might actually do in-house.
- Catastrophic forgetting is the trap: over-specialize and you lose the general competence you paid for.
- Before funding a fine-tune, ask whether prompting or retrieval would get you there. Usually it will, at a fraction of the cost.
{{% /note %}}

***

<!-- 043 — Training (LLaMA-2) -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-043.png" >}}
<h1></h1>

{{% note %}}
- A real pipeline end to end: pre-training, supervised fine-tuning, then RLHF with two separate reward models.
- Note there are two reward models — one for helpfulness, one for safety. They pull in opposite directions and are tuned deliberately.
- Human preference data sits at the top and feeds everything. People, not just compute, are on the critical path.
{{% /note %}}

***

<!-- 044 — Alignment -->
{{< slide class="fs66" >}}

# Alignment

<div class="cols2">
<div>
<p class="lead" style="text-align:left; max-width:100%; color:#CC0000; font-style:normal; font-weight:700;">The step of alignment when building Large Language Models (LLMs) is a crucial process aimed at ensuring that the model's outputs are aligned with human values, goals, and ethical standards.</p>
</div>
<div>
<p><span class="hd" style="color:#003478; font-weight:700;">Addressing Unintended Behaviors:</span> LLMs, by default, predict the next token based on probabilities learned during training. Outputs can be untruthful, biased, or harmful. Alignment seeks to steer the model away from such behaviors towards more desirable responses.</p>
<p><span class="hd" style="color:#003478; font-weight:700;">Incorporating Human Feedback:</span> Reinforcement Learning from Human Feedback (RLHF), where human raters evaluate the model's outputs and provide feedback. This feedback is used to adjust the model's parameters and improve its alignment with human preferences.</p>
<p><span class="hd" style="color:#003478; font-weight:700;">Fine-Tuning with Aligned Objectives:</span> Using datasets that include instructions, positive/negative examples, or specific guidelines that reflect the desired aligned behavior. This fine-tuning process helps the model learn to generate responses that are more aligned with the provided instructions and examples.</p>
</div>
</div>

{{% note %}}
- A raw pre-trained model is not safe or useful as a product — it just continues text. Alignment is what turns it into an assistant.
- Whose values? The rater pool's, and the guidelines they were given. Those are commercial decisions made by the vendor, not neutral facts.
- This is the direct link into the Responsible AI session: alignment is a technical control, not a governance framework.
{{% /note %}}

***

<!-- 045 — Reinforcement Learning w/ Human Feedback (RLHF) -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-045.png" >}}
<h1></h1>

{{% note %}}
- Three steps: demonstrate desired behavior, train a reward model on human rankings, then optimize the policy against that reward with PPO.
- Step two is the clever part — humans rank outputs rather than write them, which is far cheaper and more consistent.
- The reward model becomes a proxy for human judgment. Optimize too hard against a proxy and you get reward hacking.
{{% /note %}}

***

<!-- ===== GENERATIVE MODELS ===== -->
<!-- 046 — Section divider: Generative Models -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-046.png" >}}
<h1></h1>

{{% note %}}
From training to generation — what actually happens when the model produces text.
{{% /note %}}

***

<!-- 047 — Generative Models -->
{{< slide class="fs66" >}}

# Generative Models

<p>Generative AI models have impacted various domains, including vision, language, and multimodal tasks, by enabling the creation of new and realistic content.</p>

<p>In <span class="term">computer vision</span>, generative adversarial networks (GANs) can be used generating high-quality images. These models consist of a generator network that learns to produce images resembling a given dataset, and a discriminator network that learns to distinguish between real and generated images. Applications include <strong>image synthesis</strong>, <strong>super-resolution</strong>, and <strong>style transfer</strong>.</p>

<p>In <span class="term">natural language processing</span> (NLP), generative AI models like OpenAI's GPT (Generative Pre-trained Transformer) can <strong>generate coherent and contextually relevant text</strong>. These models leverage transformer architectures, which enable them to capture long-range dependencies and semantic relationships within text data. By <strong>pre-training on large corpora of text data</strong>, GPT models learn to generate human-like text in a variety of styles and tones. Applications include language <strong>translation</strong>, <strong>conversational agents</strong>, and <strong>content summarization</strong>.</p>

<p><span class="term">Multimodal generative AI</span> models integrate information from multiple modalities, such as text, images, and audio, to generate rich and diverse content. These models leverage techniques from both computer vision and natural language processing to <strong>process and understand different types of data</strong>. By learning joint representations across modalities, multimodal generative models can generate outputs that incorporate information from multiple sources. Applications include <strong>image captioning</strong>, <strong>video synthesis</strong>, and <strong>audiovisual translation</strong>.</p>

{{% note %}}
- Three families, three domains: GANs for images, transformers for text, multimodal models combining them.
- Multimodal is where the commercial action is now — a model that reads a chart, a contract scan or a photo of a damaged part.
- When scoping a use case, name the modality first. It determines cost, vendor and risk profile more than anything else.
{{% /note %}}

***

<!-- 048 — Tokenization and Embedding -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-048.png" >}}
<h1></h1>

{{% note %}}
- Each token ID is looked up in an embedding layer and becomes an N-dimensional vector.
- Those vectors are where meaning lives — similar concepts land near each other in the space.
- This is also the machinery behind semantic search and RAG, which we reach shortly.
{{% /note %}}

***

<!-- 049 — Next Token Prediction -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-049.png" >}}
<h1></h1>

{{% note %}}
- This is the whole engine: given the tokens so far, produce a probability distribution over the next token, pick one, append it, repeat.
- There is no plan and no draft. The apparent reasoning is the by-product of one-token-at-a-time prediction.
- Which is exactly why chain-of-thought prompting works — making the model write the steps gives it more tokens to condition on.
{{% /note %}}

***

<!-- 050 — Selection based on Probability -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-050.png" >}}
<h1></h1>

{{% note %}}
- The model returns a probability for every token in the vocabulary — "Buck" 51%, "Three" 31%, "and" 12%.
- A separate sampling step chooses one. That step is a dial you control, not part of the model.
- The API exposes these as logprobs, which is useful when you need a confidence signal for routing or review.
{{% /note %}}

***

<!-- 051 — Sampling Methods -->
{{< slide class="fs66" >}}

# Sampling Methods

<div class="cols2">
<div>
<p class="sub">Argmax Selection</p>
<p>Simplest method where the token with the <strong>highest predicted probability</strong> is selected as the next token.</p>
<p>Commonly used in <strong>deterministic models</strong> where the goal is to generate the most likely sequence based on the model's predictions. Example: In a language model, after computing the probabilities of all possible next tokens, the token with the highest probability is chosen.</p>
<p class="sub">Beam Search</p>
<p>Beam search <strong>maintains multiple hypotheses</strong> (beams) at each step and <strong>expands them until a complete sequence is formed</strong>. It selects the beam with the highest overall probability at the end.</p>
<p>Commonly used in machine translation where maintaining <strong>multiple potential sequences</strong> can improve accuracy by considering context over longer spans.</p>
</div>
<div>
<p class="sub">Sampling</p>
<p>Instead of always picking the token with the highest probability, sampling involves <strong>randomly selecting a token based on its probability distribution</strong>. This introduces variability and can help generate more diverse text.</p>
<p><u>Variations:</u></p>
<ul>
<li><strong>Temperature Sampling</strong>: Adjusts the randomness of predictions by scaling the logits before applying <em>softmax</em>. A higher temperature increases randomness, while a lower temperature makes predictions more deterministic.</li>
<li><strong>Top-k Sampling</strong>: Only considers the <strong>top-k most probable</strong> tokens and samples from them, effectively narrowing down choices to a manageable subset.</li>
<li><strong>Top-p (Nucleus) Sampling</strong>: Selects from the smallest set of tokens whose <strong>cumulative probability</strong> exceeds a threshold p, allowing for dynamic adjustment based on context.</li>
</ul>
</div>
</div>

{{% note %}}
- These are the knobs behind "why did it give me a different answer the second time?"
- For anything auditable — extraction, classification, compliance — use argmax or a very low temperature. Reproducibility is a requirement, not a preference.
- For drafting and ideation, sample. Different task, different setting.
{{% /note %}}

***

<!-- 052 — Sampling Temperature -->
{{< slide class="fs55" >}}

# Sampling Temperature

<div class="cols2">
<div>
<table>
<thead><tr><th style="width:22%">Temperature</th><th>Effect</th></tr></thead>
<tbody>
<tr><td><em>0</em></td><td><strong>Most likely token, no alternatives</strong>. Close to deterministic, repeated inferences will produce the same output.</td></tr>
<tr><td>0.1—0.4</td><td>Include alternative <strong>tokens slightly less likely</strong> than the front-runner. To generate small number of different solutions, to filter out the best one. More colorful, creative solution.</td></tr>
<tr><td>0.5—0.7</td><td><strong>Greater impact of chance</strong> on the solution, completions that are "inaccurate" i.e., other alternatives appear more likely. To obtain <strong>large number of independent solutions (10+)</strong>.</td></tr>
<tr><td>1</td><td>Token distribution to <strong>mirrors the statistical training set distribution</strong>. E.g., in training set the prefix <em>"One, Two,"</em> is followed by the token <em>Buck</em> in 51% of cases and by <em>Three</em> in 31% of cases; repeated inference produces <em>Buck</em> 51% of the time, and <em>Three</em> 31% of the time.</td></tr>
<tr><td>&gt; 1</td><td>Produce text that's <strong>"more random"</strong> than the training set. The model is less likely to pick the "standard" continuation than the typical document from the training set and more likely to pick a "particularly weird" continuation than the typical document from the training set.</td></tr>
</tbody>
</table>
</div>
<div>
<div style="font-size:0.78em">
<p>Alcohol consumption alters people's behaviour in myriad ways. For example: <em>(prompt)</em></p>
<p style="background:#cfe6dc; padding:0.5em 0.7em; border-radius:4px;">1. Increased alcohol consumption can lead to impaired judgement, resulting in people making decisions they would not normally make.<br><em>— sampled at temperature 0.0</em></p>
<p style="background:#fdebd0; padding:0.5em 0.7em; border-radius:4px;">2. Alcohol consumption can lead to increases in aggression and violence, particularly if someone has had too much to drink.<br><em>— sampled at temperature 1.0</em></p>
<p style="background:#f5c6cb; padding:0.5em 0.7em; border-radius:4px;">3. Impaired speech clarity may also 6e another unambiguous behavior like in mellonially reduces precision compared intentional people cleanily conservulled longer granule possord had depolar lngmen cared sentiment sentences line reasoning suffering effect containing on body ration impeggae.maunder followed persons it habit…<br><em>— sampled at temperature 2.0</em></p>
<p class="refs">Source: O'Reilly, <em>Prompt Engineering for Generative AI</em>, ch. 2 — patterns and repetitions.</p>
</div>
</div>
</div>

{{% note %}}
- The three samples make the abstract concrete: at 0.0 it is sober and predictable, at 1.0 it is natural, at 2.0 it disintegrates.
- Temperature 1 does not mean "normal" — it means matching the training distribution, which includes a lot of mediocre internet text.
- Practical default: 0 to 0.3 for anything factual, 0.7 to 1.0 for creative drafting. Above 1 is a demo, not a product.
{{% /note %}}

***

<!-- ===== DEPLOY ===== -->
<!-- 053 — Section divider: DEPLOY -->
{{< slide background-color="#1F4099" class="section" >}}

<h1><span class="de">DE</span> PLOY</h1>

{{% note %}}
Part three: putting it to work. From here on the questions are organizational, not mathematical.
{{% /note %}}

***

<!-- ===== PROMPT ENGINEERING ===== -->
<!-- 054 — Section divider: Prompt Engineering -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-054.png" >}}
<h1></h1>

{{% note %}}
The cheapest lever you have. No training, no infrastructure — just the input.
{{% /note %}}

***

<!-- 055 — Prompt Engineering -->
{{< slide class="fs66" >}}

# Prompt Engineering

<p class="lead">Prompt engineering in large language models (LLMs) refers to the strategic crafting of input prompts to guide the model's generation of outputs.</p>

<div class="cols2">
<div>
<p>This process is essential because LLMs, such as GPT-3 or BERT, are trained to predict the next word or sequence of words based on the input they receive. The quality and structure of the prompt can significantly influence the relevance, coherence, and accuracy of the model's response.</p>
<p>LLMs are dependent on prompts as they serve as the interface for human-model interaction, providing context and instruction that shape the model's behavior.</p>
</div>
<div>
<p>Without well-designed prompts, LLMs may generate outputs that are off-topic, factually incorrect, or fail to grasp the user's intent.</p>
<p>Effective prompt engineering can mitigate these issues by incorporating clear instructions, examples, or structured queries that align the model's responses with desired outcomes, making it a critical skill for leveraging the full potential of LLMs in various applications.</p>
</div>
</div>

{{% note %}}
- The prompt is the entire interface. No code change, no retraining — the leverage is disproportionate to the effort.
- Treat good prompts as organizational assets: version them, test them, and store them centrally rather than in individuals' heads.
- This is also the cheapest place to pilot. If a prompt cannot make the use case work, a fine-tune probably will not save it.
{{% /note %}}

***

<!-- 056 — Prompt Crafting: Why and What -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-056.png" >}}
<h1></h1>

{{% note %}}
- Results are genuinely sensitive to wording and order — a non-trivial problem, and an active research area.
- Different LLMs respond differently to the same prompt, so prompts are not portable between vendors without re-testing.
- Important distinction on the slide: prompt engineering is not model tuning. No code, no training data, the model stays frozen.
{{% /note %}}

***

<!-- 057 — Prompt Crafting: Anatomy of a Prompt -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-057.png" >}}
<h1></h1>

{{% note %}}
- Four blocks: context/background, instructions, task, refine.
- The refine step is the one people skip — prompting is iterative, not a single shot.
- Three reliable improvements when output is wrong: be more explicit, specify the output format, ask it to think step by step.
{{% /note %}}

***

<!-- 058 — Elements of a Prompt -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-058.png" >}}
<h1></h1>

{{% note %}}
- Seven elements: persona, instruction, context, format, audience, tone, data.
- **Format** matters most for automation — if you need to parse the output, specify the structure explicitly or you will be writing fragile string-handling code.
- **Audience** is the underused one. "For busy researchers" or "explain like I'm 5" changes the output more than most people expect.
{{% /note %}}

***

<!-- 059 — Providing Examples: zero-, one-, and few-shot -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-059.png" >}}
<h1></h1>

{{% note %}}
- Zero-shot asks; one-shot shows once; few-shot shows a pattern. Known as in-context learning.
- Nothing is being trained here — the examples live in the prompt and are forgotten the moment the call ends.
- Few-shot is the fastest fix for inconsistent output format. Show three examples and the model matches the shape.
{{% /note %}}

***

<!-- 060 — Chain-of-Thought: think before answering -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-060.png" >}}
<h1></h1>

{{% note %}}
- Same question, two prompts: the one-shot example answers 27 and is wrong; the chain-of-thought example works through it and gets 9.
- Showing the reasoning in the example makes the model produce reasoning, and the intermediate steps improve the answer.
- Trade-off: more tokens, more latency, more cost. Use it where correctness matters, not everywhere.
{{% /note %}}

***

<!-- 061 — Zero-Shot Chain-of-Thought -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-061.png" >}}
<h1></h1>

{{% note %}}
- You do not even need the worked example — "Let's think step-by-step" alone primes the reasoning.
- Five words, measurably better results on multi-step problems. Best effort-to-payoff ratio in the whole deck.
- Newer reasoning models do this internally, so the phrase matters less than it did — but knowing why it worked still matters.
{{% /note %}}

***

<!-- 062 — Self-Consistency -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-062.png" >}}
<h1></h1>

{{% note %}}
- Run the same prompt several times at non-zero temperature, then take the majority answer.
- Two of three paths reach 11, one reaches 6 — the vote discards the outlier.
- You are buying reliability with compute: three calls instead of one. Reasonable for high-stakes decisions, wasteful for routine ones.
{{% /note %}}

***

<!-- 063 — Tree of Thought -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-063.png" >}}
<h1></h1>

{{% note %}}
- Generalizes self-consistency: branch at each step, rate the branches, prune, continue.
- This is classic state-space search — Newell and Simon's idea from slide 19, now with an LLM generating and scoring the moves.
- The mechanism underneath most "deep research" and agentic planning features being sold today.
{{% /note %}}

***

<!-- 064 — More Prompts: computer vision and multi-modal -->
{{< slide class="fs66" >}}

# More Prompts

<div class="cols2">
<div>
<p class="sub">Computer Vision</p>
<ul>
<li>"Generate a high-resolution image of a cat."</li>
<li>"Create a new artistic rendering of a landscape."</li>
<li>"Translate this sketch into a realistic image."</li>
<li>"Enhance the resolution of this low-quality photograph."</li>
<li>"Remove the background from this image while preserving the foreground object."</li>
<li>"Generate a cartoon version of this portrait."</li>
<li>"Modify the lighting conditions in this image."</li>
<li>"Apply a specific artistic style to this photograph."</li>
<li>"Colorize this black and white image."</li>
<li>"Generate a realistic image of a car from a textual description."</li>
</ul>
</div>
<div>
<p class="sub">Multi-modal</p>
<ul>
<li>"Generate a descriptive caption for this image."</li>
<li>"Create a video sequence based on this textual storyline."</li>
<li>"Translate this English text into a corresponding image."</li>
<li>"Generate an audio description for this visual scene."</li>
<li>"Produce a video with synchronized audio based on this script."</li>
<li>"Generate a textual summary of this video clip."</li>
<li>"Create a slideshow presentation from this text document."</li>
<li>"Translate this image into a sequence of musical notes."</li>
<li>"Generate a storyboard based on this audio narration."</li>
<li>"Create a comic strip from this dialogue script and accompanying images."</li>
</ul>
</div>
</div>

{{% note %}}
- Text is the smallest part of the opportunity — most enterprise content is images, documents, audio and video.
- Scan these for shapes that match your own operations: damage assessment, document digitization, training material production.
- Each modality has its own accuracy profile and its own failure modes. Pilot them separately.
{{% /note %}}

***

<!-- ===== AI AGENTS ===== -->
<!-- 065 — Section divider: AI Agents -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-065.png" >}}
<h1></h1>

{{% note %}}
Where the technology stops answering questions and starts taking actions — and where governance becomes unavoidable.
{{% /note %}}

***

<!-- 066 — AI Agents -->
{{< slide class="fs66" >}}

# AI Agents

<p class="lead">AI agents in generative AI, particularly within the context of Large Language Models (LLMs), refer to advanced AI systems that leverage the generative capabilities of these models to perform a wide range of tasks autonomously.</p>

<div class="cols2">
<div>
<p class="sub">Human-like Interaction</p>
<ul>
<li>Understands and generates human-like text</li>
<li>Interacts with users and comprehends instructions</li>
<li>Executes tasks with complex reasoning and multi-step processes</li>
</ul>
<p class="sub">Foundation on LLMs</p>
<ul>
<li>Uses Large Language Models (LLMs) as a foundation</li>
<li>Learns from examples and improves over time</li>
</ul>
</div>
<div>
<p class="sub">Augmented Capabilities</p>
<ul>
<li>Accesses external databases and uses APIs</li>
<li>Incorporates updated information for dynamic environments</li>
<li>Adapts to new challenges continuously</li>
</ul>
<p class="sub">Versatile and Intelligent Systems</p>
<ul>
<li>Acts as personal assistants or customer service agents</li>
<li>Components of larger autonomous systems</li>
</ul>
</div>
</div>

{{% note %}}
- The word that changes everything: <em>autonomously</em>. A chatbot suggests; an agent acts.
- "Accesses external databases and uses APIs" is the governance boundary. The moment it can write, not just read, you need controls.
- Ask of any agent proposal: what can it do without asking, what is logged, and who is accountable when it is wrong?
{{% /note %}}

***

<!-- 067 — Agent anatomy: Profile, Memory, Planning, Action -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-067.png" >}}
<h1></h1>

{{% note %}}
- Four components: profile (who it is), memory (what it retains), planning (how it decides), action (what it can touch).
- Planning with feedback — environment, human or model — is what separates a real agent from a scripted chain of calls.
- Use this as a checklist when reviewing an architecture. Each box is a place where controls belong.
{{% /note %}}

***

<!-- 068 — Augmentation with External Knowledge (RAG) -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-068.png" >}}
<h1></h1>

{{% note %}}
- RAG: chunk your documents, embed them into a vector database, retrieve the relevant passages, and put them in the prompt.
- This is how the model gets access to your proprietary and current information without retraining anything.
- For most enterprise use cases this is the right answer — cheaper than fine-tuning, updatable instantly, and the citations make it auditable.
{{% /note %}}

***

<!-- ===== BUSINESS IMPLEMENTATION ===== -->
<!-- 069 — Section divider: Business Implementation -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-069.png" >}}
<h1></h1>

{{% note %}}
The last part: what it takes to actually run this in an organization — cost, skills, integration and ownership.
{{% /note %}}

***

<!-- 070 — Challenges when Implementing GenAI -->
{{< slide class="fs54" >}}

# Challenges when Implementing GenAI

<div class="cols3">
<div>
<p class="sub">Data Privacy and Security Concerns</p>
<p>One of the prime challenges is security and data privacy. Handling proprietary and sensitive data can pose serious risks.</p>
<p>For instance, the ChatGPT outage (March 2024) incident mentioned in the iplocation.net article underscores the vulnerabilities and privacy violations that can occur, emphasizing the need for robust security measures like encryption, access controls, and regular security audits to safeguard sensitive data.</p>
</div>
<div>
<p class="sub">Integration with Existing Workflows</p>
<p>The challenge of smoothly integrating generative AI into existing business workflows is significant.</p>
<p>For example, financial institutions considering the use of language model to determine fraud will likely find the integration challenging due to the difference in operational methodologies between legacy systems and generative AI technologies.</p>
<p>Legacy systems have a very specific way of operating, and introducing generative AI, necessitates finding new ways to either create integrations or adopt new capabilities that enable reaching the same outcomes more effectively and efficiently.</p>
</div>
<div>
<p class="sub">Expertise Requirements</p>
<p>High level of expertise is required to implement, customize, and maintain effectively, a barrier for businesses without this expertise in-house.</p>
<p>For instance, the limited talent pool challenge mentioned in the Neoteric article points out that the demand for engineers experienced in generative AI development is high, and the talent pool is limited.</p>
<p>This is further complicated by the rapid evolution of generative AI technologies, making it difficult to have extensive experience in using technology that was released only a short time ago.</p>
</div>
</div>

<p class="refs">Sources: techmango.net · iplocation.net · techtarget.com · neoteric.eu</p>

{{% note %}}
- Three blockers, and notice that none of them is model quality. The technology is rarely the constraint.
- Data privacy is the one that stops pilots becoming production — decide early what may leave your perimeter.
- The talent point is structural: nobody has ten years of experience in a three-year-old technology. Hire for judgment and adaptability, not for tool résumés.
{{% /note %}}

***

<!-- 071 — Buyers vs Builders -->
{{< slide class="fs66" >}}

# Buyers vs Builders

<p>When comparing "buyers" and "builders" within the context of generative AI, several key aspects emerge, including <span class="term">implementation time</span>, <span class="term">cost</span>, <span class="term">customization</span>, <span class="term">data privacy and security</span>, and <span class="term">skill requirements</span>. These factors play a significant role in determining whether an organization opts to buy off-the-shelf generative AI solutions or build their own in-house.</p>

<p>The decision between buying and building generative AI solutions hinges on an organization's specific needs, resources, and strategic goals. <span class="term">Buyers benefit from quicker implementation and lower initial costs</span> but may sacrifice customization and control over data privacy. <span class="term">Builders enjoy full customization and control</span> at the expense of higher costs and longer development times. Organizations often find themselves balancing these factors to choose the approach that best aligns with their objectives and capabilities.</p>

{{% note %}}
- The genuine strategic decision in this deck. Everything before it was background for this conversation.
- Framing that helps: build where it is your differentiator, buy where it is table stakes.
- Very few organizations should be training models. Most "building" in practice means building on top of someone else's model.
{{% /note %}}

***

<!-- 072 — Buyers vs Builders: side by side -->
{{< slide class="fs55" >}}

# Buyers vs Builders

<table>
<thead>
<tr><th style="width:14%; background:#003478;"></th><th style="width:43%; background:#003478; color:#fff;">Buyers</th><th style="width:43%; background:#003478; color:#fff;">Builders</th></tr>
</thead>
<tbody>
<tr>
<td><strong>Implementation Time</strong></td>
<td>Typically experience faster implementation times since they are acquiring pre-existing solutions that can be quickly integrated into their operations.</td>
<td>Face longer implementation times due to the need for developing the solution from scratch, which includes planning, development, testing, and deployment phases.</td>
</tr>
<tr>
<td><strong>Cost</strong></td>
<td>Incur upfront costs that are generally lower than building a solution. However, they may face ongoing costs for licenses, updates, and support.</td>
<td>Encounter higher initial costs related to development, including hiring skilled personnel, purchasing necessary tools, and allocating resources for ongoing maintenance and updates.</td>
</tr>
<tr>
<td><strong>Customization</strong></td>
<td>May have limited customization options, as off-the-shelf solutions are not specifically designed for their unique needs and may not integrate seamlessly with existing systems.</td>
<td>Gain the advantage of tailoring the solution precisely to their requirements, ensuring a perfect fit with their business processes and existing technological ecosystem.</td>
</tr>
<tr>
<td><strong>Data Privacy and Security</strong></td>
<td>Depend on the vendor's commitment to data privacy and security, which can be a concern if the vendor's policies do not align with the organization's standards.</td>
<td>Have complete control over data privacy and security measures, allowing them to implement the highest standards and comply with specific regulatory requirements.</td>
</tr>
<tr>
<td><strong>Skill Requirements</strong></td>
<td>Require less specialized in-house expertise since the solution is developed and maintained by the vendor. However, some level of skill is necessary to integrate and manage the solution effectively.</td>
<td>Need a team with a high level of expertise in generative AI, data science, and related technologies. This can be challenging and expensive due to the scarcity of such skilled professionals.</td>
</tr>
</tbody>
</table>

{{% note %}}
- Work down the rows and score your own organization honestly on each.
- Note the asymmetry in the cost row: buyers pay forever, builders pay up front. Model both over a five-year horizon, not one.
- Data privacy is usually the row that decides it — particularly in regulated industries where vendor policy cannot be delegated.
{{% /note %}}

***

<!-- 073 — Ownership of AI Solutions -->
<!-- {{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-073.png" >}}
<h1></h1>

{{% note %}}
- IDC: AI-centric spending reaching &#36;154 billion in 2023, 27% compound annual growth, past &#36;300 billion by 2026.
- The Forbes headline is the one to remember: a successful AI project costs roughly 15 times more than you think.
- The multiplier is not the model — it is integration into enterprise IT operations. Budget accordingly.
{{% /note %}} -->

***

<!-- 074 — Estimated training cost of select AI models -->
<!-- {{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-074.png" >}}
<h1></h1>

{{% note %}}
- The original Transformer cost about 930 dollars to train in 2017. Gemini Ultra cost about 191 million in 2023.
- Five orders of magnitude in six years. This chart alone settles the "should we train our own foundation model?" question for almost everyone.
- Note the log-scale intuition: these bars are not comparable at all on a linear axis.
{{% /note %}} -->

***

<!-- 075 — Accelerated Demand for Compute Resources -->
<!-- {{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-075.png" >}}
<h1></h1>

{{% note %}}
- Two distinct eras: until ~2012 compute tracked Moore's Law, doubling every two years. After, it doubles every 3.4 months.
- Complexity is now growing about 7 times faster than Moore's Law, and the price per Giga-FLOPS has not fallen since 2017.
- Which means capability gains are being bought, not discovered. That has direct implications for who can compete.
{{% /note %}} -->

***

<!-- 076 — Productionization of AI Solutions -->
{{< slide content-image="/imgs/intro-ai-hugo-slide-images/intro-ai-076.png" >}}
<h1></h1>

{{% note %}}
- Three zones: training, fine-tuning and maintenance, and the end-user application. Most organizations only own the third.
- Humans appear in two places — data labeling and RLHF ranking. Both are recurring operating costs, not one-off project costs.
- The right-hand column is the real menu of options: open-source or proprietary pre-trained, managed AI, or a third-party application.
{{% /note %}}

***

<!-- 077 — Implementation of Gen AI -->
{{< slide class="fs66" >}}

# Implementation of Gen AI

<div class="cols2">
<div>
<p class="sub">Enterprise-level</p>
<p>At the enterprise level, Gen AI solutions are integrated into the operations of a specific business function or across multiple functions, becoming a part of the organization's core processes and systems.</p>
<p>This approach is designed to enhance the overall efficiency, productivity, and innovation of teams and departments.</p>
</div>
<div>
<p class="sub">Personal/Individual</p>
<p>On the personal or individual level, Gen AI solutions are adopted by individual employees to enhance their own productivity and performance in their specific roles.</p>
<p>This approach allows for personalized use of Gen AI tools to meet unique job requirements and personal work styles.</p>
</div>
</div>

{{% note %}}
- Two adoption paths, and they are already both happening in your organization — the individual one usually without approval.
- Shadow adoption is the immediate risk: staff pasting proprietary data into consumer tools. Policy and a sanctioned alternative beat prohibition.
- Enterprise adoption delivers larger returns but requires integration work; individual adoption delivers fast returns but no institutional learning.
{{% /note %}}

***

<!-- 078 — Enterprise-level adoption -->
{{< slide class="fs63" >}}

# Enterprise-level

<div class="cols2">
<div>
<p class="sub">Characteristics</p>
<ul>
<li><strong>Broad Scope:</strong> Targets improvements in processes, services, or products that impact the entire organization or significant parts of it.</li>
<li><strong>Collaborative Use:</strong> The solution is accessible, used by multiple team members, facilitating collaboration and shared benefits.</li>
<li><strong>System Integration:</strong> Requires integration with existing IT infrastructure, databases, and applications to ensure seamless operation and data flow.</li>
</ul>
<p class="sub">Benefits</p>
<ul>
<li><strong>Efficiency Gains:</strong> Automates repetitive tasks and optimizes workflows, leading to significant time savings and operational efficiency at scale.</li>
<li><strong>Enhanced Decision-Making:</strong> Provides valuable insights and data analysis, supporting better-informed decision-making across departments.</li>
<li><strong>Innovation Acceleration:</strong> Enables rapid prototyping, content generation, and idea exploration, fostering a culture of innovation.</li>
</ul>
</div>
<div>
<p class="sub">Challenges</p>
<ul>
<li><strong>Complex Integration:</strong> May involve significant challenges in integrating with existing systems and ensuring compatibility and scalability.</li>
<li><strong>Change Management:</strong> Requires effective change management strategies to address resistance, train employees, and ensure adoption.</li>
<li><strong>Data Privacy and Security:</strong> Must address concerns related to data privacy and security, especially when handling sensitive information.</li>
</ul>
</div>
</div>

{{% note %}}
- Change management appears as a challenge, not a footnote — and it is usually the one that sinks these programs.
- The benefits are real but they are second-order: they require the integration work in the characteristics column to happen first.
- Budget rule of thumb from the IDC slide: whatever the model and licenses cost, the integration and adoption work costs considerably more.
{{% /note %}}

***

<!-- 079 — Personal or Individual-Level adoption -->
{{< slide class="fs66" >}}

# Personal or Individual-Level

<div class="cols2">
<div>
<p class="sub">Characteristics</p>
<ul>
<li><strong>Focused Application:</strong> Tailored to address specific tasks or challenges faced by an individual, such as content creation, data analysis, or coding.</li>
<li><strong>Personal Productivity:</strong> Directly impacts the efficiency and output of individual employees, enabling them to accomplish more in less time.</li>
<li><strong>Ease of Adoption</strong>: Often involves standalone applications or plugins that are easier to adopt and require minimal integration efforts.</li>
</ul>
<p class="sub">Benefits</p>
<ul>
<li><strong>Customization:</strong> Allows for customization and personalization of the Gen AI tool to fit the individual's needs and preferences.</li>
<li><strong>Skill Enhancement</strong>: Empowers employees to enhance their capabilities and tackle more complex tasks with AI assistance.</li>
<li><strong>Immediate Impact:</strong> Provides immediate productivity gains and benefits to the individual, contributing to job satisfaction and performance.</li>
</ul>
</div>
<div>
<p class="sub">Challenges</p>
<ul>
<li><strong>Varied User Experience:</strong> The effectiveness can vary significantly between individuals based on their ability to leverage the tool.</li>
<li><strong>Lack of Standardization:</strong> May lead to inconsistencies in work quality or processes if different tools are used by employees within the same team.</li>
<li><strong>Knowledge Gaps:</strong> Requires individuals to have or develop an understanding of how to effectively use Gen AI tools for their specific needs.</li>
</ul>
</div>
</div>

{{% note %}}
- Immediate impact and easy adoption is why this path happens with or without a strategy.
- The cost is in the challenges column: inconsistent quality, no shared standards, and capability that walks out the door with the employee.
- Practical middle path — sanction a small set of tools, publish a shared prompt library, and capture what individuals learn as an institutional asset.
- That sets up the next session: De-risk. Governance of exactly this.
{{% /note %}}

***

<!-- ===== DEVELOP ===== -->
<!-- Section divider: DEVELOP -->
{{< slide background-color="#1F4099" class="section" >}}

<h1><span class="de">DE</span> VELOP</h1>

{{% note %}}
Last part: where this is heading. Shorter, and deliberately more speculative than everything before it.
{{% /note %}}

***

<!-- pptx 97 — beyond today's models (Gartner framing + three research directions) -->
{{< slide class="fs66" >}}

# Beyond Today's Models

<p class="lead">Generative AI sat on the <strong>Peak of Inflated Expectations</strong> in Gartner's Hype Cycle for Emerging Technologies &mdash; 2023.</p>

<div class="cols3">
<div>
<p class="sub">Agents at scale</p>
<p>Multi-agent simulations, social agents, digital twins.</p>
</div>
<div>
<p class="sub">Neuro-symbolic</p>
<p>Combine logical reasoning, problem solving and rule-based systems with the &ldquo;flexibility&rdquo; and scalability of neural models.</p>
</div>
<div>
<p class="sub">Structured knowledge</p>
<p>Graph databases, Graph Neural Networks, reasoning.</p>
</div>
</div>

<p class="refs">Source: Gartner, Inc. Hype Cycle for Emerging Technologies, 2023.</p>

{{% note %}}
- The 2023 positioning is history now — use it to ask the room where they think it sits today, and whether their own organization is still on the peak.
- All three directions are reactions to the same limitation: a next-token predictor has no explicit model of truth or of rules.
- Neuro-symbolic is the oldest idea in this deck coming back — it is Newell and Simon's symbolic reasoning bolted onto a neural model.
{{% /note %}}

***

<!-- pptx 98 — generative AI trends -->
{{< slide class="fs66" >}}

# Where the Technology Is Heading

<div class="cols2">
<div>
<p class="sub">Multimodal AI Models</p>
<p>The emergence of multimodal AI models that can understand and generate content across different forms of media, such as text, images, audio, and video, is a significant trend. These models are expected to become more intuitive and dynamic, allowing for more natural interactions with AI systems.</p>
<p class="sub">Small Language Models (SLMs)</p>
<p>While large language models have been the focus, there is a growing trend towards developing powerful SLMs that require less computational power and can be fine-tuned for specific tasks or industries, meeting legal and regulatory requirements.</p>
</div>
<div>
<p class="sub">Autonomous Agents</p>
<p>The development of autonomous agents, which are software programs designed to accomplish specific objectives without human intervention, is on the rise. These agents are expected to improve customer experiences by providing highly contextualized interactions in various sectors.</p>
<p class="sub">Open Models vs. Proprietary Models</p>
<p>There is an ongoing debate and development regarding open models, which are expected to become comparable to proprietary models in terms of capabilities. This trend is likely to democratize access to generative AI technologies.</p>
</div>
</div>

{{% note %}}
- Small language models are the one to watch for regulated industries — cheap enough to run in your own environment, which resolves most data-residency objections.
- Open versus proprietary is a procurement question as much as a technical one: it decides whether you can switch vendors later.
- Autonomous agents bring us back to the governance boundary from the Agents section — capability is arriving faster than the controls.
{{% /note %}}

***

<!-- pptx 99 — trends in academia -->
{{< slide class="fs60" >}}

# Trends in Academia

<div class="cols2">
<div>
<p class="sub">Education</p>
<p>Generative AI is being used to create <strong>personalized lesson plans and learning materials</strong> that cater to individual student needs and learning styles. AI-powered systems analyze student data to generate customized curriculum.</p>
<p><strong>AI tools</strong> assist educators in creating comprehensive and customized course materials, including lesson plans, lecture notes, and educational content, saving significant time and effort.</p>
<p>Generative AI is used for <strong>automating grading, generating quizzes, and providing feedback</strong>, as well as creating virtual simulations for immersive learning experiences.</p>
<p>AI-based tutoring systems offer clarification on various topics and recommend study plan adjustments, providing interactive learning content and instant feedback.</p>
</div>
<div>
<p class="sub">Research</p>
<p>Tools like <strong>ResearchRabbit</strong> and <strong>Genei</strong> are being used to notify researchers about new publications, visualize networks of papers, and summarize existing literature. These tools help researchers identify relevant studies and key insights, particularly useful for comprehensive literature reviews.</p>
<p>Generative AI is being employed to <strong>draft and revise academic papers</strong>, submissions, and presentations. Grammarly and Microsoft's Editor and Designer assist in writing, while other tools help aggregate and organize literature.</p>
<p>Researchers are encouraged to <strong>disclose the use of AI</strong> in their work, and professional organizations and publishers are releasing guidelines for the acceptable use of AI during publication and review.</p>
</div>
</div>

{{% note %}}
- Closest to home for this audience — and the disclosure norm in the last line is the one that generalizes: expect it to reach your industry's professional bodies too.
- The education column is a template for corporate training: personalized material, automated assessment, always-available tutoring.
- Worth asking the room what their own organization's disclosure policy is. Most do not have one yet.
{{% /note %}}
