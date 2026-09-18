+++
title = "Engineering Robust RAG Systems"
description = "From query stratification to failure mitigation — why one RAG architecture cannot serve every question, and the seven places these pipelines break"
weight = 21
outputs = ["Reveal"]
math = true
thumbnail = "/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-0.png"


[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"

+++

<!--
    Slide deck: Engineering Robust RAG Systems.

    Follows slide-20-rag (the RAG fundamentals deck) and assumes it. Built on
    two papers, synthesised in the blueprint figures:
      1. Zhao et al. (Microsoft Research Asia) — the four-level stratification
         of query intent.
      2. Barnett et al. (Deakin University) — the seven failure points observed
         when engineering RAG systems.

    Two kinds of slides are used here:
      1. Image slides — the blueprint figures.
         Format: {{</* slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-0.png" */>}}
         Source images live in www/static/imgs/slide-21-engineering-robust-rag
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
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-0.png" >}}
<h1></h1>

{{% note %}}
- The two panels are the session in one image. On the left, the architecture as it is drawn in the design review. On the right, the same architecture under load, with every joint lit up orange.
- Nothing on the right is a *model* failure. The model is one box out of seven, and most of the fires are upstream of it.
- This session is built on two papers: a Microsoft Research Asia survey on how to make LLMs use external data wisely, which gives us a way to classify what is being asked; and a Deakin University field study of RAG systems in production, which gives us a catalogue of where they break.
- Audience note: the figures in this deck were generated with NotebookLM from those two papers. Treat them as well-drawn summaries, not as the papers themselves — which is itself a lesson about grounded generation.
{{% /note %}}

***

<!-- ===== WHERE WE PICK UP ===== -->
{{< slide class="fs60" >}}

# Where this session picks up

<p class="lead">EMBA 8160 &mdash; AI for Leaders. Prerequisite: the RAG fundamentals session.</p>

<div class="cols2">
<div>
<p class="sub">You already know</p>
<p>Documents are chunked, embedded, and retrieved by similarity; a reranker reorders the shortlist; the model answers from what it was handed.</p>
<p>That pipeline answers <em>&ldquo;what is the mileage rate?&rdquo;</em> very well.</p>
</div>
<div>
<p class="sub">Today's two questions</p>
<p><span class="term">1.</span> What happens when the question is harder than lookup &mdash; when it needs aggregation, a rulebook, or judgement learned from experience?</p>
<p><span class="term">2.</span> When the system gives a bad answer, <em>which</em> of the seven things that can go wrong actually went wrong?</p>
</div>
</div>

{{% note %}}
- The fundamentals session described one architecture. This session's argument is that one architecture is not enough, and that a system which cannot tell you *where* it failed cannot be improved.
- Frame the payoff for the room: by the end you should be able to hear a user complaint — "it makes stuff up," "it's too vague," "it misses things" — and translate it into a specific, named engineering problem with a known fix.
{{% /note %}}

***

<!-- ===== SECTION 1 ===== -->
{{< slide background-color="#003478" class="section" >}}

# One Architecture, Every Question

<p>The assumption that quietly breaks most deployments</p>

{{% note %}}
Part one: why the standard pipeline disappoints as soon as it leaves the demo corpus.
{{% /note %}}

***

<!-- 1 — The one-size-fits-all trap -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-1.png" >}}
<h1></h1>

{{% note %}}
- The core problem stated formally: most teams build RAG as a single function from a query and a document set to an answer, and assume every query is a needle-in-a-haystack lookup.
- The reality in expert domains is entangled. A finance question may depend on a high-dimensional time series; a legal question on a dependency that spans fifty pages; a clinical question on judgement nobody wrote down.
- The &ldquo;leaking house&rdquo; is the metaphor to carry: the structure is sound in the drawing, but water comes through at every joint, because the architecture was never matched to the difficulty of what is being asked.
- Business translation: when the pilot works and the rollout disappoints, it is usually because the pilot's questions were all Level 1 and the rollout's questions were not.
{{% /note %}}

***

<!-- ===== SECTION 2 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Stratifying the Query

<p>Four levels of intent &mdash; and four different architectures</p>

{{% note %}}
Part two: the Zhao framework. This is the organising idea of the whole session.
{{% /note %}}

***

<!-- 2 — The stratification of user intent -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-2.png" >}}
<h1></h1>

{{% note %}}
- Four levels, climbing in difficulty: **explicit facts**, **implicit facts**, **interpretable rationales**, **hidden rationales**.
- Level 1 is stated in the text. Level 2 must be assembled from several places. Level 3 requires applying a documented rule. Level 4 requires inferring a rule nobody ever wrote down.
- The insight in the right-hand panel is the one to hold onto: as you climb, the system stops retrieving *data* and starts needing *rationales*. Retrieval alone runs out of road somewhere between Level 2 and Level 3.
- Practical use of this framework: before scoping any RAG project, take fifty real questions from the intended users and sort them into these four buckets. The distribution tells you what you are actually being asked to build — and it is rarely what the sponsor assumed.
{{% /note %}}

***

<!-- 3 — Level 1 -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-3.png" >}}
<h1></h1>

{{% note %}}
- **Level 1 — explicit facts.** The answer exists in plain text in one place. &ldquo;Where will the 2024 Summer Olympics be held?&rdquo;
- Three retrieval strategies: **sparse** (BM25/TF-IDF, keyword matching — the classic search engine), **dense** (embeddings, semantic meaning), and **hybrid**, which combines them.
- Hybrid is the practical default, and worth knowing as a leader for one reason: dense retrieval alone is bad at exact identifiers. Part numbers, policy codes, account numbers, surnames — these are keyword problems, and a purely semantic system will miss them. If your corpus is full of codes, ask specifically whether retrieval is hybrid.
- The processing note matters for real corpora: charts and tables need table-to-text conversion or multi-modal embeddings, or they are effectively invisible to retrieval. Most enterprise documents are full of tables.
{{% /note %}}

***

<!-- 4 — Level 2 -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-4.png" >}}
<h1></h1>

{{% note %}}
- **Level 2 — implicit facts.** The answer exists, but scattered: it has to be assembled. &ldquo;What is the majority party in the country where Canberra is located?&rdquo; requires linking Canberra to Australia and then Australia to its current government.
- One retrieval pass cannot do this, because the second hop depends on the result of the first.
- Three engineering answers: **iterative RAG** (retrieve, reason, retrieve again); **graph or tree RAG**, which organises chunks into structures — RAPTOR builds a recursive summary tree, GraphRAG builds a graph and detects communities in it; and **SQL integration**, where a natural-language question is translated into a database query.
- The business version of this level is the one everyone actually wants: &ldquo;how many of our contracts include this clause?&rdquo; That is an aggregation over documents, not a lookup in one. Standard RAG will answer it confidently from the three chunks it happened to retrieve, and the number will be wrong.
- The cost note: every extra hop is another model call. Level 2 systems are multiples more expensive and slower per question than Level 1.
{{% /note %}}

***

<!-- 5 — Level 3 -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-5.png" >}}
<h1></h1>

{{% note %}}
- **Level 3 — interpretable rationales.** The rule exists and is written down — in a handbook, a guideline, a documented workflow — and the job is to apply it correctly. &ldquo;How should a patient with acute chest pain be managed?&rdquo; under a specific clinical guidance.
- The figure models this as a state machine: check guidelines, apply the rule set, produce a compliant answer. That framing is the figure's own metaphor, but it is a useful one, because it says the system's job is *procedure-following*, not recall.
- Techniques: prompt tuning to enforce rule adherence, chain-of-thought to mimic the guideline's logic, and agent workflows with planning and memory.
- This is where most regulated-industry use cases actually sit, and it is the level where RAG stops being a search problem and starts being a workflow problem. Note the governance consequence: at this level the system is effectively giving procedural advice, and someone has to own whether that advice is correct.
{{% /note %}}

***

<!-- 6 — Level 4 -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-6.png" >}}
<h1></h1>

{{% note %}}
- **Level 4 — hidden rationales.** No one wrote the rule down. It has to be inferred from patterns in what the organisation did before. Debugging a server crash from past incident logs; pricing a deal the way this firm prices deals.
- The key line is the last one in the definition: **logical congruence matters more than semantic similarity**. The most useful past case is not the one that reads most like the current one — it is the one that had the same underlying structure. Similarity search actively misleads here.
- Three approaches: **offline learning** (mine the corpus for principles in advance), **in-context learning** (retrieve past *examples* rather than documents), and **fine-tuning**, when the reasoning style is too complex to fit in a prompt.
- This is the level where &ldquo;we have twenty years of institutional knowledge in this drive&rdquo; meets reality. The knowledge is in there, but not in a form retrieval can reach. Expect a data-labelling project, not a search project.
{{% /note %}}

***

<!-- Four levels, business view -->
{{< slide class="fs55" >}}

# The four levels, in your language

<table class="plain">
<tr><th>Level</th><th>A question from your business</th><th>What it needs</th><th>Relative cost</th></tr>
<tr><td class="lv">L1 &middot; Explicit facts</td><td>&ldquo;What is our parental leave entitlement?&rdquo;</td><td>Hybrid retrieval over a curated index</td><td>Low</td></tr>
<tr><td class="lv">L2 &middot; Implicit facts</td><td>&ldquo;How many active contracts include a change-of-control clause?&rdquo;</td><td>Iterative retrieval, graph/tree structure, or SQL</td><td>Medium &mdash; multiple model calls per question</td></tr>
<tr><td class="lv">L3 &middot; Interpretable rationales</td><td>&ldquo;Does this transaction require enhanced due diligence?&rdquo;</td><td>Agent workflow that follows a documented procedure</td><td>High &mdash; plus a named owner for the procedure</td></tr>
<tr><td class="lv">L4 &middot; Hidden rationales</td><td>&ldquo;How would we normally price this deal?&rdquo;</td><td>Examples mined from history; possibly fine-tuning</td><td>Highest &mdash; a data project before a build project</td></tr>
</table>

<p class="refs">The distribution of your users' real questions across these four rows <em>is</em> the scope of the project. Sorting fifty of them costs an afternoon and routinely changes the plan.</p>

{{% note %}}
- Run the room's own examples through this table if there is time. The useful surprise is how many "simple chatbot" requests are actually L2 or L3 in disguise.
- The cost column is the one to take to a steering committee. A sponsor who budgeted for L1 and was handed an L3 problem has not been given a technology problem; they have been given a scoping failure.
- Notice that L3 and L4 both require something no vendor can supply: someone inside the business who will say what the correct answer is.
{{% /note %}}

***

<!-- ===== SECTION 3 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Where Pipelines Break

<p>Seven failure points, observed in the field</p>

{{% note %}}
Part three: the Barnett analysis. This is the diagnostic half of the session.
{{% /note %}}

***

<!-- 7 — The stress test -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-7.png" >}}
<h1></h1>

{{% note %}}
- The pipeline laid out end to end — data source, indexer, retriever, context window, generator, output — with the seven failure points pinned to where they occur. One at the indexer, two at the retriever, four at the generator.
- The study behind this ran a substantial experiment — on the order of fifteen thousand documents and a thousand questions — and reports that automated evaluation was **more pessimistic than human raters**. Useful when someone waves an automated score at you: it is a signal, not a verdict, and it can be wrong in both directions.
- The key insight is the sentence bottom right, and it is the one worth arguing about: **robustness cannot be designed in at the start; it evolves through validation.** You cannot specify your way to a reliable RAG system. You discover the failures by running it against real questions and fixing what breaks.
- Which has a budget implication: if the plan has no post-launch iteration budget, the plan is wrong.
{{% /note %}}

***

<!-- 8 — Pre-generation failures -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-8.png" >}}
<h1></h1>

{{% note %}}
- The three failures that happen **before the model ever sees the prompt**.
- **FP1 — Missing content.** The answer simply is not in the index. The risk is not the miss; it is that the system hallucinates instead of saying &ldquo;I don't know.&rdquo;
- **FP2 — Missed top rank.** The right passage is in there, ranked eighth, and you retrieve the top three. Exactly the failure a reranker exists to fix, and exactly what recall@k versus precision@k measures. Note the fix can be as blunt as raising $k$ — at the cost of more noise.
- **FP3 — Not in context.** Retrieved, then dropped during consolidation before reaching the model. Mitigation is better metadata and smarter consolidation.
- All three look identical to the user: the system did not know something it should have known. They have completely different fixes, which is why a system that cannot show you its retrieved passages cannot be debugged.
{{% /note %}}

***

<!-- 9 — Generation failures -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-9.png" >}}
<h1></h1>

{{% note %}}
- The four failures that happen **after** the right material has been retrieved — so no amount of retrieval tuning will help.
- **FP4 — Not extracted.** The answer was in the context and the model did not use it. Causes: noise, contradictory passages, or &ldquo;lost in the middle&rdquo; — the well-documented tendency of models to attend less to material buried in the centre of a long context. This is the direct argument against &ldquo;just retrieve twenty chunks to be safe.&rdquo;
- **FP5 — Wrong format.** Asked for a table, got prose. Breaks anything downstream that parses the output.
- **FP6 — Incorrect specificity.** Too vague or too precise. Often caused by the *user's* question being general — worth saying out loud, because it means some failures are fixed by interface design, not model work.
- **FP7 — Incomplete.** Asked for A, B and C; got A and B. The most dangerous of the four, because the answer looks complete and nothing signals the gap.
- Ask the room which of these seven their own teams have reported without naming it. FP6 and FP7 are usually in the pile labelled &ldquo;the AI isn't very good.&rdquo;
{{% /note %}}

***

<!-- Symptom to diagnosis -->
{{< slide class="fs55" >}}

# From complaint to diagnosis

<table class="plain">
<tr><th>What the user says</th><th>Likely failure point</th><th>Where to look first</th></tr>
<tr><td>&ldquo;It made that up.&rdquo;</td><td class="lv">FP1</td><td>Is the document even in the index? Does the system ever say &ldquo;I don't know&rdquo;?</td></tr>
<tr><td>&ldquo;It missed the obvious document.&rdquo;</td><td class="lv">FP2</td><td>Retrieval depth $k$, and whether a reranker exists at all</td></tr>
<tr><td>&ldquo;It found it yesterday, not today.&rdquo;</td><td class="lv">FP3</td><td>Consolidation and filtering between retrieval and prompt</td></tr>
<tr><td>&ldquo;The answer was right there in the source.&rdquo;</td><td class="lv">FP4</td><td>Too many chunks, contradictory sources, long-context dilution</td></tr>
<tr><td>&ldquo;It won't give me a table.&rdquo;</td><td class="lv">FP5</td><td>The prompt's format instruction, and output validation</td></tr>
<tr><td>&ldquo;It's too vague to use.&rdquo;</td><td class="lv">FP6</td><td>The <em>question</em> as much as the system &mdash; interface and query rewriting</td></tr>
<tr><td>&ldquo;It only answered half.&rdquo;</td><td class="lv">FP7</td><td>Multi-part questions; decomposition before answering</td></tr>
</table>

{{% note %}}
- This is the slide to photograph. It turns an unfalsifiable complaint — "the AI is bad" — into a triage step someone can act on.
- The discipline to insist on: no fix is approved without first naming which failure point it addresses. Otherwise teams tune whatever is most fun to tune, which is usually the prompt.
- Note how many rows point upstream of the model. Of seven, only four are the generator's fault, and two of those are prompt and interface issues rather than model quality.
{{% /note %}}

***

<!-- ===== SECTION 4 ===== -->
{{< slide background-color="#003478" class="section" >}}

# The Design Decisions

<p>Chunking, and the choice between context and weights</p>

{{% note %}}
Part four: the two decisions that a sponsor will be asked to approve without being told they are decisions.
{{% /note %}}

***

<!-- 10 — Chunking and embedding dilemma -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-10.png" >}}
<h1></h1>

{{% note %}}
- The trade-off drawn as a balance, and now tied to specific failure points: **small chunks** give precise retrieval but strip context, which produces FP4 — the model has the fragment and cannot use it. **Large chunks** preserve meaning but add noise and cost, which produces FP3 — good material crowded out during consolidation.
- Strategies: **heuristic** chunking (fixed size or punctuation — simple and risky) versus **semantic** chunking on meaning-based boundaries, which performs better.
- The embedding note is a genuinely useful procurement point: open-source embedding models often perform comparably to closed commercial ones on short text. Embeddings are frequently the cheapest place to avoid vendor lock-in, and the one teams are least likely to question.
- There is no correct chunk size in the abstract. It is found by testing against your own golden set — which is the validation loop from the previous section, again.
{{% /note %}}

***

<!-- 11 — Three paths to knowledge injection -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-11.png" >}}
<h1></h1>

{{% note %}}
- Three ways to get organisational knowledge into a model: put it in the **context** (RAG), train a **small proxy model** to guide retrieval, or **fine-tune** the base model so the knowledge lives in the weights.
- Each maps to a level: context for L1 and L2 facts; a small proxy where a specific task needs to be fast and cheap; fine-tuning for L4, where the reasoning pattern itself is the thing to learn.
- The middle path is the one most people have never heard of and is worth flagging: a small trained model that guides retrieval can cut latency and cost substantially without touching the large model.
- The strategic note in orange is the single most actionable line in this deck: **do not fine-tune for explicit facts.** It is expensive, it goes stale, it cannot cite, and it hallucinates around the edges. Facts belong in the index.
{{% /note %}}

***

<!-- 12 — To fine-tune or not -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-12.png" >}}
<h1></h1>

{{% note %}}
- The decision matrix, and the sentence at the bottom is the one to remember: **RAG is for facts, fine-tuning is for form.**
- Top left: facts plus retrieval — high suitability. Bottom left: facts plus fine-tuning — avoid, because of hallucination and catastrophic forgetting. Top middle: reasoning patterns and style plus fine-tuning — recommended.
- Then the box nobody expects on a slide about accuracy: **fine-tuning carries a security risk.** Research indicates that fine-tuning — including lightweight methods such as LoRA — can erode or reverse a model's safety training, and that fine-tuned models can be more vulnerable to adversarial attack.
- That moves the decision out of engineering. &ldquo;We'll fine-tune it on our data&rdquo; is a statement with a security review attached, and it is very rarely treated that way. If your firm fine-tunes, the safety evaluation has to be re-run afterwards — the base model's assurances no longer transfer.
- Tie back: this is the same governance principle as the Responsible AI session. Every capability decision is also a risk decision.
{{% /note %}}

***

<!-- ===== SECTION 5 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Operating It

<p>What robustness looks like after launch</p>

{{% note %}}
Part five: the half of the lifecycle that never appears in the business case.
{{% /note %}}

***

<!-- 13 — Lessons from the field -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-13.png" >}}
<h1></h1>

{{% note %}}
- Three operational practices.
- **Continuous calibration.** A RAG system receives inputs nobody anticipated. Latency, cost and accuracy can only really be validated *in operation* — which is the argument for running a small, permanent evaluation harness in production rather than a one-off acceptance test.
- **Semantic caching.** Pre-populate a cache with known FAQs. It cuts cost and latency, and it directly mitigates FP1: for questions you know are common, you can guarantee a correct answer rather than hoping retrieval finds it.
- **The routing pipeline.** This is the punchline of the whole session. Real applications get a mix of levels, so route each question to the architecture that fits it: L1 and L2 to vector search, L3 to agent workflows, L4 to fine-tuned models.
- That is the resolution of the one-size-fits-all trap from the opening: not one architecture, but a router in front of several. Worth stating plainly — the deliverable is a portfolio of retrieval strategies with a classifier in front, not a chatbot.
{{% /note %}}

***

<!-- 14 — The engineer's checklist -->
{{< slide content-image="/imgs/slide-21-engineering-robust-rag/Robust_RAG_Engineering_Blueprint-14.png" >}}
<h1></h1>

{{% note %}}
- The whole session as three phases. **Stratify:** audit the queries, are they facts or rationales, and pick the strategy per level. **Implement:** test heuristic against semantic chunking, and inject filenames and chunk IDs as metadata so answers can cite. **Stress test:** check FP1–FP3 at the retriever and FP4–FP7 at the generator.
- Note the metadata item in phase two. Citation is not a feature you add later; it depends on identifiers being carried through the index from the beginning. Retrofitting it is expensive.
- The closing quote is the line to leave with the room: **build for observability, not just accuracy.** A system that is 90% accurate and tells you which 10% failed and why will overtake a 95% black box within two release cycles.
{{% /note %}}

***

<!-- Governance gates -->
{{< slide class="fs55" >}}

# The same checklist, as governance gates

<div class="cols3">
<div>
<p class="sub">Gate 1 &mdash; Scope</p>
<p>Fifty real user questions, sorted into the four levels. Sponsor signs off on the distribution, not on a demo.</p>
<p><em>Fails if:</em> nobody can produce fifty real questions.</p>
</div>
<div>
<p class="sub">Gate 2 &mdash; Build</p>
<p>Chunking tested, not assumed. Metadata and citation identifiers carried end to end. Access control enforced at retrieval.</p>
<p><em>Fails if:</em> citations cannot be traced to a source document.</p>
</div>
<div>
<p class="sub">Gate 3 &mdash; Validate</p>
<p>Failures reported by failure point, split retrieval versus generation. Post-launch iteration budget committed.</p>
<p><em>Fails if:</em> quality is reported as a single accuracy number.</p>
</div>
</div>

<p class="refs">Three gates, three refusals. Each one costs days at the start and saves quarters later.</p>

{{% note %}}
- This is the leader's version of the engineer's checklist — same content, expressed as things you can decline to approve.
- Gate 1 is the highest-leverage. Most failed RAG projects were mis-scoped before a line of code was written, and the fifty-question audit catches it in an afternoon.
- The failure conditions are deliberately concrete. "We'll get to evaluation later" is the most expensive sentence in this field.
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
# Sorting the Queries

Your operations team asks for &ldquo;a chatbot over our SOPs.&rdquo; Their example questions include: &ldquo;What is the escalation threshold?&rdquo;, &ldquo;How many incidents last quarter breached it?&rdquo;, and &ldquo;Should we escalate this one?&rdquo;

<p class="q">Sort these into levels. What does the mix tell you about scope, cost, and who from the business has to be on the project?</p>

{{% note %}}
- L1, L2, L3 respectively — one request, three architectures. That is the point.
- The third question is the trap: it asks the system to apply a procedure and effectively make a call. That needs an owner for the procedure and a decision about whether the system recommends or decides.
- Good groups notice that the L2 question needs data the SOP documents do not contain at all — it needs the incident system.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 2
# Diagnosing the Complaint

Three months after launch, your HR assistant gets these complaints in the same week: &ldquo;it invented a policy,&rdquo; &ldquo;it gave me half the answer,&rdquo; and &ldquo;the right document was in there but it used an old one.&rdquo;

<p class="q">Name the likely failure point for each. What evidence would you ask for to confirm the diagnosis &mdash; and which of the three worries you most?</p>

{{% note %}}
- FP1, FP7, and a retrieval/curation problem that presents as FP2 or FP3 (the old document outranked the current one).
- Evidence in every case: the retrieved passages for that specific question. If the team cannot produce them, the real finding is that the system is not observable.
- The third should worry them most — it is silently wrong and looks correct. It is also a records-management failure, not a model failure.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 3
# The Fine-Tuning Proposal

A vendor proposes fine-tuning an open model on ten years of your claims files, arguing it will &ldquo;learn how we assess claims&rdquo; and remove the need for a retrieval system entirely.

<p class="q">Which part of that proposal is defensible and which is not? What would you require before approving it &mdash; and what would you still keep in an index?</p>

{{% note %}}
- Defensible: learning the assessment *reasoning style* is a genuine Level 4 problem, and fine-tuning is a legitimate tool for it.
- Not defensible: "remove the need for retrieval." Policy terms, limits and current rules are explicit facts — they belong in an index, they change, and they must be citable.
- Requirements: a re-run of safety evaluation after fine-tuning, given the jailbreak finding; a plan for what happens when the base model is deprecated; and an answer to how a fine-tuned model forgets a claim it must not retain.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 4
# Buying Observability

Two vendors bid. Vendor A reports 94% accuracy on your documents. Vendor B reports 89%, broken out by retrieval and generation, with the failure points named and a dashboard showing which questions failed.

<p class="q">Which do you pick, and how do you defend that choice to a procurement committee that sees 94 &gt; 89?</p>

{{% note %}}
- The intended answer is B, and the defence is the improvement rate: B can be debugged, A can only be replaced.
- Push further — A's 94% is on questions of unknown difficulty. Without the level breakdown, a high score may simply mean an easy test set.
- The procurement framing that works: you are not buying today's accuracy, you are buying the ability to raise it.
{{% /note %}}

***

{{< slide class="dq fs60" >}}

### Discussion Question 5
# Synthesis

You are the executive sponsor of a knowledge assistant for a 2,000-person professional services firm. Users will ask for policy facts, cross-document counts, procedural guidance, and &ldquo;how do we usually handle this?&rdquo; &mdash; all four levels, on day one.

<p class="q">Design the phased plan. Which level do you ship first and why? What do you deliberately refuse to build in phase one, and how do you explain that refusal to the partners who asked for all four?</p>

{{% note %}}
- Strong answers ship L1 first — it is cheap, it is measurable, and it earns the trust needed to fund the rest.
- The refusal to look for: L4 in phase one. "How do we usually handle this?" needs curated historical examples that almost certainly do not exist yet in usable form, and shipping it badly poisons adoption for everything else.
- Best answers add a router from the start, even a crude one, so that out-of-scope questions are declined explicitly rather than answered badly.
{{% /note %}}

***

<!-- ===== TAKEAWAYS ===== -->
{{< slide class="fs60" >}}

# Takeaways

<div class="card"><span class="hd">Classify the question before choosing the architecture</span>Four levels, four designs. The mix of levels in your users' real questions is the scope of the project.</div>
<div class="card"><span class="hd">&ldquo;It gave a bad answer&rdquo; is seven different problems</span>Three happen before the model sees the prompt. Insist that failures are named, not averaged.</div>
<div class="card"><span class="hd">RAG is for facts, fine-tuning is for form</span>And fine-tuning is a security decision as well as a quality one.</div>
<div class="card"><span class="hd">Robustness is discovered, not specified</span>Budget for the iteration after launch, and build for observability rather than for a single accuracy number.</div>

{{% note %}}
- If one sentence survives: **the deliverable is a router in front of several architectures, not a chatbot.**
- The through-line from the fundamentals session holds — the model is not the system — and this session adds the corollary: the system is not one system.
{{% /note %}}

***

<!-- ===== CREDITS ===== -->
{{< slide class="fs55" >}}

# Sources &amp; Figure Credits

<div class="card"><span class="hd">Query stratification &mdash; Levels 1&ndash;4</span>
Siyun Zhao et al., Microsoft Research Asia, <em>Retrieval Augmented Generation (RAG) and Beyond: A Comprehensive Survey on How to Make Your LLMs Use External Data More Wisely</em> (2024).</div>

<div class="card"><span class="hd">The seven failure points</span>
Scott Barnett et al., Applied Artificial Intelligence Institute, Deakin University, <em>Seven Failure Points When Engineering a Retrieval Augmented Generation System</em> (2024).</div>

<div class="card warn"><span class="hd">About these figures</span>
The blueprint illustrations in this deck were generated with <strong>NotebookLM</strong> from the two papers above &mdash; they are a synthesis, not an excerpt. Wording, emphasis and framing (the &ldquo;leaking house,&rdquo; the state machine, the balance scale) are the tool's, not the authors'. Read the papers before citing any specific figure or number.</div>

{{% note %}}
- Say the last card out loud rather than skipping it. A deck about grounded generation, illustrated by generated summaries of two papers, is the lesson in miniature: the synthesis is useful, legible and fast — and it is not the source.
- Both papers are short and readable; point anyone who wants to go further at Barnett first, since the failure catalogue is immediately usable.
{{% /note %}}

***
