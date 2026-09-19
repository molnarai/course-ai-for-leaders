+++
title = "Retrieval Augmented Generation (RAG)"
description = "Grounding language models in your own documents — embeddings, vector search, reranking, evaluation, and the decisions leaders actually own"
weight = 20
outputs = ["Reveal"]
math = true
thumbnail = "/imgs/slide-20-rag-imgs/Slide21.png"


[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"

+++

<!--
    Slide deck on Retrieval Augmented Generation.

    Two kinds of slides are used here:
      1. Image slides — the figures exported from the source deck.
         Format: {{</* slide content-image="/imgs/slide-20-rag-imgs/Slide2.png" */>}}
         Source images live in www/static/imgs/slide-20-rag-imgs
      2. Native slides — section dividers, framing and discussion questions,
         written as markdown + HTML so the text stays selectable and editable.
         They use the helper classes defined in the style block below.

    Every content slide carries speaker notes in a {{%/* note */%}} block.
-->

<style>
/* Helper classes for this deck. Palette follows reveal-robinson.css —
   GSU Blue #003478, GSU Crimson #CC0000. */

/* reveal-robinson.css pads sections by 50px with box-sizing: content-box, which
   makes every section 1060px wide on a 960px stage and clips text off the right
   edge. Scoped correction so the native slides fit. */
.reveal .slides section { box-sizing: border-box; }

/* Body scale — each native slide is set to the largest step that still fits. */
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

/* Title slide — white type over the dark embedding-space background. The
   panel guarantees contrast regardless of what sits behind it. */
.reveal .slides section.title { text-align: center; }
.reveal .slides section.title .titlebox { background: rgba(0, 18, 42, 0.62);
                border-radius: 10px; padding: 1.1em 1.4em 1.3em 1.4em; }
.reveal .slides section.title h1 { color: #fff; font-size: 1.95em; margin-bottom: 0.15em;
                text-shadow: 0 2px 10px rgba(0,0,0,0.45); }
.reveal .slides section.title h2 { color: #9FC5E8; font-size: 0.9em; font-weight: 600;
                margin-top: 0; text-shadow: 0 2px 8px rgba(0,0,0,0.45); }
.reveal .slides section.title .byline { font-size: 0.58em; color: #d5dfea; margin: 1.4em 0 0 0; }

/* Section dividers — flat GSU Blue panel. */
.reveal .slides section.section { text-align: center; }
.reveal .slides section.section h1 { color: #fff; font-size: 2.3em; margin: 0; }
.reveal .slides section.section p { color: #c9d6e8; font-size: 0.66em; margin-top: 0.7em; }

/* The theme's footer branding and slide number are dark, drawn for white
   slides. Reverse them to white while a dark divider is on screen. */
.reveal:has(.slides section.section.present) .slide-footer img,
.reveal:has(.slides section.title.present) .slide-footer img { filter: brightness(0) invert(1); }
.reveal:has(.slides section.section.present) .slide-number,
.reveal:has(.slides section.title.present) .slide-number { color: #EDEEEF; }

/* Discussion question slides */
.reveal .slides section.dq h3 { color: #CC0000; font-size: 0.75em; margin-bottom: 0.15em; }
.reveal .slides section.dq h1 { font-size: 1.6em; }
.reveal .slides section.dq .q { color: #003478; font-weight: 700; margin-top: 0.9em; }
</style>

<!-- ===== TITLE ===== -->
{{< slide background-image="/imgs/slide-20-rag-imgs/rag-title.png" class="title" >}}

<div class="titlebox">

# Retrieval Augmented Generation
## Grounding the model in *your* knowledge, not just its own

<p class="byline">EMBA 8160 &mdash; AI for Leaders<br>J. Mack Robinson College of Business, Georgia State University</p>

</div>

{{% note %}}
- RAG is the single most common enterprise AI architecture — most "we built a chatbot on our documents" projects are RAG projects.
- The goal today is not to make you build one. It is to let you read a design, ask the three or four questions that actually determine whether it works, and recognise a vendor claim that cannot be true.
- Structure: what problem retrieval solves, how documents become a searchable index, what "similarity" really means, how to make retrieval better, how to measure it, and how the answer finally gets generated.
{{% /note %}}

***

<!-- ===== OUTLINE ===== -->
{{< slide class="fs66" >}}

# Outline

<ol>
<li><span class="term">Why retrieval</span> &mdash; the problem RAG solves, and the alternatives</li>
<li><span class="term">Building the index</span> &mdash; chunking, embeddings, vector databases</li>
<li><span class="term">How similarity works</span> &mdash; feature spaces, distance, nearest neighbors</li>
<li><span class="term">Making retrieval better</span> &mdash; fine-tuned embeddings and reranking</li>
<li><span class="term">Measuring quality</span> &mdash; precision, recall, and what to hold your team to</li>
<li><span class="term">From retrieval to answers</span> &mdash; grounded generation and the prompt</li>
</ol>

{{% note %}}
- Sections 2 and 3 are the machinery. Section 3 in particular is the one most executives skip — and it is where most of the quality problems live.
- Keep one question in the back of your mind the whole session: *if this system gives a wrong answer, how would we find out?*
{{% /note %}}

***

<!-- ===== SECTION 1 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Why Retrieval?

<p>The problem RAG solves &mdash; and the two alternatives</p>

{{% note %}}
Part one: why not just ask the model, and why not just train it on our data?
{{% /note %}}

***

<!-- Why RAG — the three options -->
{{< slide class="fs55" >}}

# Three ways to give a model your knowledge

<div class="cols3">
<div>
<p class="sub">1. Put it in the prompt</p>
<p>Paste the documents in every time. Simple, immediate, always current.</p>
<p><strong>Breaks when:</strong> the corpus is bigger than the context window, or you pay for the same 200 pages on every question.</p>
</div>
<div>
<p class="sub">2. Fine-tune the model</p>
<p>Continue training on your material so the knowledge is "in the weights."</p>
<p><strong>Breaks when:</strong> facts change. Fine-tuning is excellent at teaching <em>form</em> &mdash; tone, format, task behaviour &mdash; and unreliable at teaching <em>facts</em>. It cannot cite, and it cannot forget on request.</p>
</div>
<div>
<p class="sub">3. Retrieve it on demand</p>
<p>Search your documents at question time and hand the model only the relevant passages.</p>
<p><strong>Why it wins:</strong> current, citable, permission-aware, and updated by re-indexing a document rather than retraining a model.</p>
</div>
</div>

<p class="refs">These are not mutually exclusive. Production systems routinely retrieve <em>and</em> fine-tune &mdash; retrieval for the facts, fine-tuning for the behaviour.</p>

{{% note %}}
- The governance argument is the one that usually settles it: with retrieval you can answer "where did that come from?" and you can delete a document and have it actually disappear from answers. Neither is true of fine-tuning.
- Long context windows have not made RAG obsolete. They have raised the ceiling on option 1 — you still pay per token, latency grows, and models still lose material buried in the middle of a very long context.
- A reasonable rule of thumb: **retrieval for what the model should know, fine-tuning for how it should behave.**
{{% /note %}}

***

<!-- Slide2 — Semantic search, reranking, RAG -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide2.png" >}}
<h1></h1>

{{% note %}}
- This is the whole session on one slide — three ideas stacked.
- **Dense retrieval** (top left): the query and the documents are both turned into vectors; you return the documents whose vectors sit closest to the query's. This is "semantic" search — it matches meaning, so "how do I take time off?" finds the PTO policy even though neither word appears in it.
- **Reranking** (top right): first-stage retrieval is fast and approximate. A reranker takes the shortlist and reorders it with a slower, much more accurate model. Note what happened in the figure — result #3 became #1. That reordering is often the single largest quality gain in the pipeline.
- **RAG** (bottom): retrieval plus generation. The model writes the answer *and* cites which retrieved passages it used.
- Ask the room: which of the three is the part most vendors demo? Usually the generation. The quality lives in the first two.
{{% /note %}}

***

<!-- ===== SECTION 2 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Building the Index

<p>From a pile of documents to something you can search by meaning</p>

{{% note %}}
Part two: the offline half of the system. Everything here happens before anyone asks a question.
{{% /note %}}

***

<!-- Slide3 — knowledge base to vector database -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide3.png" >}}
<h1></h1>

{{% note %}}
- The ingestion pipeline in three steps: take the external knowledge, **chunk** it into passages, run each chunk through an **embedding model**, and store the resulting vectors in a **vector database**.
- Note what is being stored: not the words, but a list of numbers per chunk. The original text is kept alongside so it can be shown and cited.
- This runs on a schedule, not on every question. That raises the first governance question: **how stale is the index allowed to be?** A policy chatbot refreshed weekly will confidently quote last week's policy.
- Cost note for the budget conversation: embedding a corpus is a one-time-per-document cost and it is small. Re-embedding the entire corpus because you switched embedding models is not.
{{% /note %}}

***

<!-- Slide4 — Bag-of-words vs Word2Vec -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide4.png" >}}
<h1></h1>

{{% note %}}
- Two generations of "text as numbers."
- **Bag-of-words** (left): count the words. "My cat is cute" becomes a vector of counts over the vocabulary. It works, and keyword search still uses a refined version of it — but it has no idea that *cat* and *kitten* are related. Every word is its own unrelated dimension.
- **Word2Vec** (right): train a small network on the task "are these two words neighbors?" and the vectors it learns place related words near each other. The table is the intuition — *cats* and *puppy* both score high on "animal," *baby* scores high on "newborn" and "human."
- The caveat on the slide matters: the dimensions do **not** actually correspond to human concepts like "animal" or "fruit." That is a teaching fiction. The dimensions are learned and individually uninterpretable — which is exactly why you cannot audit an embedding by reading it.
{{% /note %}}

***

<!-- Slide5 — Dense retrieval -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide5.png" >}}
<h1></h1>

{{% note %}}
- Left: the embedding space, drawn in two dimensions. Related words cluster — *cats*, *dog*, *puppy* in one region; *apple*, *banana* in another; *houses*, *building* in a third.
- Right: retrieval is the same picture with documents instead of words. Embed the query, drop it into the same space, return the nearest texts.
- The real space has hundreds or thousands of dimensions, not two. Everything you will see plotted is a projection for human benefit.
- The critical dependency: the query and the documents **must be embedded by the same model**. Mixing embedding models produces two incompatible spaces and retrieval silently returns noise. This is a real and common production failure.
{{% /note %}}

***

<!-- Slide6 — Embeddings of different types of input -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide6.png" >}}
<h1></h1>

{{% note %}}
- The same representation model produces embeddings at different granularities: **token**, **word**, **sentence**, and **document**.
- RAG normally works at the chunk level — roughly the "sentence/passage" scale — because that is the unit you want to retrieve and show to a user.
- Granularity is a trade-off. Embed a whole 40-page document into one vector and it becomes an average of everything it discusses, matching nothing specific. Embed single sentences and you retrieve fragments with no context.
- Note "##ization" in the figure: models split text into sub-word tokens, not words. That is why token counts never match word counts on your invoice.
{{% /note %}}

***

<!-- Slide7 — Document chunking -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide7.png" >}}
<h1></h1>

{{% note %}}
- Chunking is the most consequential, least discussed decision in the entire pipeline.
- Options shown: one chunk per sentence, one per paragraph, or a sliding **overlapping window**. On the right, the same choice at the character and token level, with and without overlap.
- Why overlap: a sentence that begins "It must be approved by the CFO" is useless if the previous sentence — the one that says what *it* is — landed in a different chunk. Overlap buys back some of that lost context.
- The failure this causes in practice: a clause is split across a boundary, so no single chunk contains the full rule, so the retriever never surfaces it and the model answers from a partial one. The answer looks fluent and is wrong.
- Structure beats arbitrary length. Chunking on real document structure — sections, clauses, table rows — outperforms "every 500 tokens" in nearly every serious system.
{{% /note %}}

***

<!-- Slide8 — Nearest neighbor retrieval -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide8.png" >}}
<h1></h1>

{{% note %}}
- The full query path: documents are chunked and embedded into the vector database ahead of time; at question time the query goes through the **same** embedding model and is compared against the stored vectors; the most similar chunks come back.
- The orange callout is the part leaders should hear: vector databases also store **metadata**, and you can filter on it. Department, document type, effective date, and — critically — **access control**.
- That metadata filter is your permissions boundary. If retrieval ignores who is asking, a RAG assistant becomes an extremely efficient way to leak documents to people who should not see them. "Filter before you retrieve, not after" is the design rule.
- Ask the room: who owns the access-control list for the index? In most failed pilots the answer is "nobody thought about it."
{{% /note %}}

***

<!-- Index design decisions -->
{{< slide class="fs55" >}}

# The index is a set of decisions, not a database

<div class="cols2">
<div>
<div class="card"><span class="hd">Chunk size &amp; overlap</span>Too big retrieves noise, too small loses context. Drive it from document structure.</div>
<div class="card"><span class="hd">Embedding model</span>Fixes the geometry of your search space. Changing it means re-embedding everything.</div>
<div class="card"><span class="hd">Metadata schema</span>What you can filter on later — source, date, owner, department, sensitivity.</div>
</div>
<div>
<div class="card"><span class="hd">Refresh cadence</span>How stale answers are allowed to be, and what happens when a document is withdrawn.</div>
<div class="card"><span class="hd">Access control</span>Enforced at retrieval time, inherited from the source system &mdash; not re-invented in the chatbot.</div>
<div class="card"><span class="hd">What stays out</span>Drafts, superseded policy, personal data. The index is a publication decision.</div>
</div>
</div>

{{% note %}}
- Every one of these is a business decision with a technical implementation, not the reverse. They are the right things to ask about in a design review.
- "What stays out" is the one teams forget. If the shared drive contains three versions of the travel policy and two are obsolete, the retriever cannot tell which is current — it has no concept of authority, only of similarity. Someone has to curate.
- Deletion is a compliance question. If a document must be purged, purging it from the source system is not enough; the chunks and vectors are separate copies.
{{% /note %}}

***

<!-- ===== SECTION 3 ===== -->
{{< slide background-color="#003478" class="section" >}}

# How Similarity Works

<p>Feature spaces, distance metrics, and nearest neighbors</p>

{{% note %}}
Part three: we have said "closest" and "most similar" a dozen times. Now we define them. This is the classical machine-learning foundation that vector search is built on — it predates LLMs by decades.
{{% /note %}}

***

<!-- Slide9 — Draft based athletes' ratings -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide9.png" >}}
<h1></h1>

{{% note %}}
- A deliberately small, non-text example so the geometry is visible: twenty athletes, two measurements each — speed and agility — and a yes/no draft decision.
- Plotted on the right, each athlete is a **point**. Triangles were not drafted, crosses were.
- The question — should we draft someone at speed 6.75, agility 3.0 — is structurally identical to "which document chunk is most relevant to this query." Both are: *place a new point in a space and look at what is near it.*
- Two dimensions here; an embedding has hundreds. The algorithm does not change, only our ability to draw it.
{{% /note %}}

***

<!-- Slide10 — Feature space and similarity metric -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide10.png" >}}
<h1></h1>

{{% note %}}
- **Feature space**: take each descriptive feature as an axis and every instance becomes a point. Speed and agility here; the learned dimensions of an embedding in a RAG system.
- **Similarity metric**: a function that measures how close two points are. The four criteria are worth a moment because they are what make a metric well-behaved — non-negativity, identity, symmetry, and the triangle inequality.
- The triangle inequality is the one that earns its keep in practice: it is what lets a vector database prune most of the corpus without checking it. Without it, every query would have to compare against every chunk.
- Terminology note: similarity and distance run in opposite directions. Small distance, high similarity. Vendors quote whichever sounds better.
{{% /note %}}

***

<!-- Slide11 — Distance metrics -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide11.png" >}}
<h1></h1>

{{% note %}}
- **Euclidean**: straight-line distance — the length of the diagonal.
- **Manhattan**: the taxi-cab route, summing the distance along each axis separately.
- Same two points, two different numbers. The choice is not cosmetic: it decides which neighbors are "nearest," and therefore which documents get retrieved.
- Euclidean is sensitive to magnitude in every dimension at once, which is why it behaves badly in very high-dimensional spaces — an issue we come back to with cosine similarity.
{{% /note %}}

***

<!-- Slide12 — Metric choice changes the answer -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide12.png" >}}
<h1></h1>

{{% note %}}
- The punchline of the section, made concrete. From the query point, athlete 5 and athlete 17 are **both** at Manhattan distance 7.25 — a tie. Under Euclidean distance they are not tied at all: 5.58 versus 8.25.
- One metric says "these are equally similar." The other picks a clear winner. And they have different draft labels, so the *prediction flips* with the metric.
- Manhattan and Euclidean are both special cases of Minkowski distance; the parameter interpolates between them.
- The leadership translation: "most relevant" is not a property of your documents. It is a property of your documents **plus** a modelling choice someone made. When retrieval quality is disappointing, this is one of the knobs.
{{% /note %}}

***

<!-- Slide13 — Nearest neighbor algorithm -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide13.png" >}}
<h1></h1>

{{% note %}}
- The algorithm in full: store the instances, measure the distance from the query to each one, take the closest, return its label.
- Notice there is no training step. Nearest neighbor is *lazy* — it memorises the data and does the work at query time. Vector search is exactly this, scaled, with approximate indexes so it does not have to scan every point.
- That is also why adding a document to a RAG system is cheap. There is no model to retrain; you add a point to the space.
{{% /note %}}

***

<!-- Slide14 — Voronoi tessellation -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide14.png" >}}
<h1></h1>

{{% note %}}
- Left: the **Voronoi tessellation** — each cell is the region of space closer to that one instance than to any other. The boundaries are the points of equal distance between two neighbors.
- Right: merge the cells by label and you get the **decision boundary**. Our query lands in the "draft" region.
- Look at how jagged that boundary is. Every single training point carves out its own territory, so one unusual instance creates its own little island — the model memorises noise.
- In retrieval terms: with a single nearest neighbor, one badly written or mis-chunked document can dominate a whole neighbourhood of queries. That is the argument for the next slide.
{{% /note %}}

***

<!-- Slide15 — k-Nearest Neighbors -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide15.png" >}}
<h1></h1>

{{% note %}}
- Instead of one neighbor, take the nearest $k$ and let them vote. Odd values avoid ties.
- Watch the boundary smooth as $k$ goes 1, 3, 5, 15 — and then look at $k=15$, where whole regions have been swallowed by the majority class. Larger neighbourhoods suppress noise and dilute genuine local signal.
- The weighted variant lets closer neighbors count for more, which recovers some of that detail.
- This is the same dial as "how many chunks do we retrieve?" Retrieve 3 and you may miss the passage that mattered; retrieve 20 and you bury the right answer in loosely related text the model then has to ignore. There is no universally correct $k$ — it is tuned against real questions.
{{% /note %}}

***

<!-- Slide16 — Pre-processing features -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide16.png" >}}
<h1></h1>

{{% note %}}
- Distance only means something if the axes are commensurable. The table is the standard treatment per feature type — binary, categorical (one-hot), interval, numeric, ordinal, and text.
- The bottom-right plots show why **scaling** is not optional. Salary runs to 75,000 and age to 60, so before normalisation the distance is essentially "difference in salary" and age contributes nothing. After range normalisation both features count. The nearest neighbor changes.
- Note the last row: "text → convert to categorical or vector embedding." That is the bridge from this classical picture to everything in the first half of the deck. An embedding is a pre-processing step that turns text into numeric features.
{{% /note %}}

***

<!-- Slide17 — Cosine similarity -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide17.png" >}}
<h1></h1>

{{% note %}}
- **Cosine similarity** measures the angle between two vectors and ignores their length.
- Why that matters for text: a two-page memo and a two-paragraph summary of the same policy point in nearly the same direction but have very different magnitudes. Under Euclidean distance the length difference dominates; under cosine they are correctly judged similar.
- The figure makes the reverse case too — in Case 2, cosine gets it wrong and Euclidean gets it right. Neither metric is universally correct.
- In practice cosine similarity (or the closely related dot product on normalised vectors) is the default for text embeddings, for the two reasons on the slide: small magnitude differences and very high dimensionality.
- If someone tells you their similarity score is 0.87, the right follow-up is "0.87 of what, and is that good?" Cosine scores are not probabilities and they are not comparable across embedding models.
{{% /note %}}

***

<!-- ===== SECTION 4 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Making Retrieval Better

<p>Fine-tuned embeddings and reranking</p>

{{% note %}}
Part four: the two highest-leverage improvements once a baseline pipeline exists.
{{% /note %}}

***

<!-- Slide18 — Fine-tuning embeddings -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide18.png" >}}
<h1></h1>

{{% note %}}
- A general-purpose embedding model has never seen your vocabulary. In an insurance corpus, "claim," "loss" and "exposure" carry specific meanings that a general model places only approximately.
- Fine-tuning the **embedding model** fixes the geometry: it pulls relevant queries closer to the document and pushes irrelevant ones away. Look at the before/after — "Interstellar cast" is moved away, the two release-date queries are moved in.
- What this costs you: labelled examples of "this query should match this passage." Query logs plus a few hundred human judgements is a normal starting point.
- What it costs you operationally: a new embedding model means re-embedding the entire corpus and rebuilding the index. Budget for it as a migration, not a tweak.
{{% /note %}}

***

<!-- Slide19 — Reranking -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide19.png" >}}
<h1></h1>

{{% note %}}
- The standard two-stage architecture. **First stage:** search millions of documents fast and imprecisely, returning maybe 50 candidates. **Second stage:** a reranker reads the query and each candidate *together* and scores relevance properly.
- The distinction that matters: first-stage retrieval compares two vectors that were computed independently. A reranker is a **cross-encoder** — it sees the query and the document at the same time, so it can judge whether this passage actually answers *this* question. Much more accurate, far too slow to run over the whole corpus.
- This is usually the cheapest large quality win available. If a pilot is "retrieving the right document but not at the top," reranking is the first thing to try — no re-indexing required.
- The cost is latency and per-query spend. It is a per-question cost, unlike embedding, which is a per-document cost.
{{% /note %}}

***

<!-- ===== SECTION 5 ===== -->
{{< slide background-color="#003478" class="section" >}}

# Does It Work?

<p>Measuring a retrieval system honestly</p>

{{% note %}}
Part five: the section that separates pilots that ship from pilots that demo well and quietly die.
{{% /note %}}

***

<!-- Slide20 — Evaluation / mean average precision -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide20.png" >}}
<h1></h1>

{{% note %}}
- **Precision at k** asks: of the top $k$ results, how many were actually relevant? Compute it at each position, average over the positions where a relevant document appeared, and you have **average precision** for one query. Average that across a test suite of queries and you have **mean average precision (MAP)** — one number to compare two search systems.
- The middle example is the important one: the system found the relevant document, but it placed two irrelevant ones above it, and the score fell from 1.0 to 0.3. **Rank is penalised, not just presence.** That is correct behaviour — an answer buried at position 8 is an answer nobody reads, and a model handed three irrelevant passages first is a model primed to answer from them.
- Note the prerequisite hiding in the phrase "for query in the test suite": someone had to decide which documents are relevant for each test query. That labelled set is the real deliverable. Without it you are not measuring, you are guessing.
{{% /note %}}

***

<!-- What leaders should measure -->
{{< slide class="fs60" >}}

# What to hold the team to

<table class="plain">
<tr><th>Question</th><th>Metric</th><th>Failure it catches</th></tr>
<tr><td>Did we find the right passage at all?</td><td><span class="term">Recall@k</span></td><td>Chunking and indexing problems &mdash; the answer is not in the shortlist</td></tr>
<tr><td>Did we put it near the top?</td><td><span class="term">MAP / MRR</span></td><td>Ranking problems &mdash; fixable with reranking</td></tr>
<tr><td>Is the answer supported by what we retrieved?</td><td><span class="term">Groundedness</span></td><td>The model inventing detail the sources do not contain</td></tr>
<tr><td>Do the citations point at the right place?</td><td><span class="term">Citation accuracy</span></td><td>Plausible-looking references to the wrong document</td></tr>
<tr><td>Does it answer what was asked?</td><td><span class="term">Answer relevance</span></td><td>Correct, well-sourced, off-topic responses</td></tr>
<tr><td>Can we afford it at volume?</td><td><span class="term">Latency &amp; cost / query</span></td><td>A pilot that cannot survive its own success</td></tr>
</table>

<p class="refs">The first two measure <strong>retrieval</strong>; the next three measure <strong>generation</strong>. A system can fail either half, and the fixes are completely different &mdash; so insist on both being reported separately.</p>

{{% note %}}
- The practical ask: a **golden set** of 50–100 real questions from real users, with the correct source passage identified by someone who knows the domain. It takes a subject-matter expert a day or two and it is the difference between engineering and hoping.
- Insist that retrieval and generation are scored separately. "The chatbot is 85% accurate" is not a number that tells you what to fix.
- Re-run the golden set on every change — new embedding model, new chunking, new base LLM. Retrieval quality regresses silently; nothing crashes, answers just get worse.
{{% /note %}}

***

<!-- ===== SECTION 6 ===== -->
{{< slide background-color="#003478" class="section" >}}

# From Retrieval to Answers

<p>Grounded generation and the prompt</p>

{{% note %}}
Part six: we finally get to the language model — and it arrives last on purpose. It is the smallest part of the problem.
{{% /note %}}

***

<!-- Slide21 — RAG pipeline -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide21.png" >}}
<h1></h1>

{{% note %}}
- The complete pipeline, and it is only two steps: **retrieval**, then **grounded generation**.
- Look at the prompt on the right — that is the entire mechanism. The retrieved passages are pasted in as `{context}`, the user's question as `{question}`, and the instruction says to answer *using the relevant information provided above*.
- "Grounded" is doing real work in that sentence. The instruction constrains the model to the supplied passages instead of its own parameters. It reduces hallucination substantially; it does not eliminate it, because nothing stops a model from blending what it read with what it already believed.
- The uncomfortable implication: **if retrieval returns the wrong passages, a better language model makes things worse, not better.** It will write a more convincing wrong answer. Garbage in, eloquent garbage out.
- This is also where "I don't know" has to be engineered. A system that cannot decline when retrieval comes back empty will fabricate, every time.
{{% /note %}}

***

<!-- Slide22 — Elements of a prompt -->
{{< slide content-image="/imgs/slide-20-rag-imgs/Slide22.png" >}}
<h1></h1>

{{% note %}}
- The anatomy of the instruction wrapped around the retrieved context: **persona**, **instruction**, **context**, **format**, **audience**, **tone**, and the **data** itself.
- In a RAG system most of these are written once by the team and reused for every query. Only the data and the question change. So the prompt is a piece of software — it should be version-controlled, reviewed, and tested like any other.
- **Format** is the one with operational consequences: if a downstream system parses the output, an unspecified format will eventually break it.
- **Audience** is the one with reputational consequences: the same retrieved policy needs a different answer for an employee than for a regulator.
- This is also where your guardrails live — instructions to cite sources, to decline when the context is insufficient, and to stay within scope.
{{% /note %}}

***

<!-- Where RAG breaks -->
{{< slide class="fs55" >}}

# Where RAG actually breaks

<div class="cols2">
<div>
<div class="card warn"><span class="hd">The passage was never retrieved</span>Split across a chunk boundary, or phrased so differently from the query that the embedding missed it. The model answers from second-best sources and sounds fine.</div>
<div class="card warn"><span class="hd">The index is stale</span>The policy changed on Monday; the index refreshed on Friday. Confidently current, factually obsolete.</div>
<div class="card warn"><span class="hd">Conflicting sources</span>Three versions of the same document, all retrievable. Similarity has no notion of authority &mdash; it cannot tell you which one is in force.</div>
</div>
<div>
<div class="card warn"><span class="hd">Permission leakage</span>Retrieval that ignores who is asking turns a chatbot into a very efficient document exfiltration tool.</div>
<div class="card warn"><span class="hd">Citations that do not check out</span>The answer is right, the reference points somewhere else. Erodes trust faster than being wrong.</div>
<div class="card warn"><span class="hd">No graceful "I don't know"</span>When retrieval returns nothing useful, an unconstrained model fills the gap from memory &mdash; the single most damaging failure mode.</div>
</div>
</div>

{{% note %}}
- Every one of these is a design and governance failure, not a model failure. Swapping in a better LLM fixes none of them.
- The one to watch hardest is the first, because it is invisible. Nothing errors, no alert fires — the answer is simply built on the wrong evidence. Only a golden set catches it.
- Conflicting sources is the most common cause of "the pilot worked, production didn't." Curated demo corpus, uncurated shared drive.
{{% /note %}}

***

<!-- Questions to ask -->
{{< slide class="fs55" >}}

# Six questions for your next design review

<ol>
<li>What is <span class="term">in the index</span>, who decided, and what was deliberately left out?</li>
<li>How does retrieval know <span class="term">who is asking</span>, and where is that enforced?</li>
<li>How <span class="term">fresh</span> is the index, and what happens when a document is withdrawn?</li>
<li>Show me the <span class="term">golden set</span> &mdash; and retrieval and generation scored separately.</li>
<li>What does the system do when it <span class="term">cannot find</span> a good answer?</li>
<li>What is the <span class="term">cost and latency</span> per query at ten times this volume?</li>
</ol>

{{% note %}}
- These six separate a team that has built a system from a team that has built a demo. None of them requires you to read code.
- If question 4 gets a hand-wave, nothing else in the review means much — you have no evidence about quality, only anecdotes.
- Question 5 is the cheapest insurance in the whole architecture and it is routinely skipped because it makes the demo look less impressive.
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
# Retrieve, Fine-tune, or Both?

Your firm wants an assistant that answers client questions about your service agreements. The agreements are renegotiated constantly, and the answers must sound like your firm's house style.

<p class="q">Which knowledge goes in the index and which goes in the model &mdash; and how would you justify the split to a skeptical CFO?</p>

{{% note %}}
- Looking for: facts and contract terms retrieved, house style and response behaviour fine-tuned or prompted.
- Push on the CFO framing: retrieval is an operating cost per query, fine-tuning is a capital-ish project cost that must be repeated whenever the base model changes.
- Good answer also mentions that only retrieval can cite the specific clause — often a requirement, not a nicety, in client-facing work.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 2
# The Chunking Decision

A compliance manual contains numbered clauses, many with exceptions that appear two or three paragraphs after the rule itself. Your vendor proposes chunking every 500 tokens with no overlap.

<p class="q">What goes wrong, how would you detect it before go-live, and what would you propose instead?</p>

{{% note %}}
- What goes wrong: rules and their exceptions land in different chunks. The system retrieves the rule, never the exception, and states it absolutely. In compliance that is a serious answer to get wrong.
- Detection: a golden set built specifically from rule-with-exception cases — the hard questions, not the easy ones.
- Better proposal: chunk on document structure (clause boundaries), keep the clause number and section as metadata, and overlap.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 3

# Similarity Is Not Authority

Your shared drive holds the 2023, 2024 and 2025 travel policies. All three are indexed. A user asks what the mileage reimbursement rate is, and the system returns the 2023 rate with a confident citation.

<p class="q">Whose failure is this, and what are three different places in the architecture where it could be fixed?</p>

{{% note %}}
- Not a model failure — the retriever did exactly what it was built to do. Similarity has no concept of "current."
- Three fixes at three layers: (1) curation — only the in-force policy enters the index; (2) metadata — effective dates stored and filtered at retrieval; (3) generation — the prompt requires the answer to state the effective date, which at least surfaces the problem to the user.
- Press on ownership: this is a records-management responsibility that the AI project has just inherited without being told.
{{% /note %}}

***

{{< slide class="dq fs66" >}}

### Discussion Question 4
# Proving It Works

A vendor demos a RAG assistant on your documents. Every question they ask it is answered beautifully. They quote "92% accuracy."

<p class="q">What do you ask them before signing, and what would you require in a pilot to generate evidence you would actually trust?</p>

{{% note %}}
- First question: 92% of what, measured on which questions, chosen by whom? Almost always the vendor's own curated set.
- Require: your questions, your documents, retrieval and generation scored separately, and the failures shown — not just the wins.
- Strong answers propose adversarial cases: questions with no answer in the corpus, questions whose answer changed recently, questions spanning two documents.
{{% /note %}}

***

{{< slide class="dq fs60" >}}

### Discussion Question 5
# Synthesis

You are sponsoring a RAG assistant over HR policies, benefits documents, and the employee handbook, available to all 4,000 employees. Legal is nervous, HR is enthusiastic, and IT has a vector database licence already.

<p class="q">Identify the three biggest risks, name one concrete mitigation for each, and state the single metric you would put in front of the steering committee each month. What would make you stop the project?</p>

{{% note %}}
- Expected risks: permission leakage (some HR documents are not for everyone), stale or superseded policy, and fabricated answers on benefits questions with real financial consequences for employees.
- Push for one metric, not a dashboard — forces prioritisation. Groundedness or citation accuracy on the golden set are defensible choices.
- The stop condition is the real test of whether they have thought about governance. Most groups have no answer prepared.
{{% /note %}}

***

{{< slide class="fs60" >}}

# Takeaways

<div class="card"><span class="hd">RAG is a search problem wearing an AI costume</span>The language model is the last and smallest step. Quality is decided in chunking, embedding, and ranking.</div>
<div class="card"><span class="hd">"Similar" is a modelling choice</span>Metric, chunk size, and $k$ all change which evidence reaches the model &mdash; and therefore the answer.</div>
<div class="card"><span class="hd">A better model cannot fix bad retrieval</span>It only makes the wrong answer more persuasive.</div>
<div class="card"><span class="hd">Without a golden set, you have no evidence</span>You have demos. Insist on retrieval and generation measured separately, and re-measured on every change.</div>

{{% note %}}
- If one sentence survives the session: **the model is not the system.**
- The work that determines success — curation, permissions, chunking, evaluation — is organisational work with a technical surface. It is exactly the kind of work that has no owner unless a leader assigns one.
{{% /note %}}

***

<!-- ===== CREDITS ===== -->
{{< slide class="fs50" >}}

# Figure Credits

<div class="card"><span class="hd">Jay Alammar &amp; Maarten Grootendorst, <em>Hands-On Large Language Models</em> (O'Reilly, 2024)</span>
Semantic search and reranking overview; document&nbsp;&rarr;&nbsp;chunk&nbsp;&rarr;&nbsp;vector-database pipeline; bag-of-words and word2vec; dense retrieval; token, word, sentence and document embeddings; chunking strategies; nearest-neighbor retrieval; embedding fine-tuning; two-stage reranking; mean average precision; the RAG pipeline; and the elements of a prompt.</div>

<div class="card"><span class="hd">John D. Kelleher, Brian Mac Namee &amp; Aoife D'Arcy, <em>Fundamentals of Machine Learning for Predictive Data Analytics</em> (MIT Press)</span>
The athlete draft dataset; feature space and similarity metrics; Euclidean and Manhattan distance; the nearest-neighbor algorithm; Voronoi tessellation and decision boundaries; <em>k</em>-nearest-neighbors; and feature pre-processing and normalisation.</div>

<div class="card"><span class="hd">Cosine similarity worked example</span>
Sasi Kumar, &ldquo;Cosine Similarity vs Euclidean Distance,&rdquo; <em>Medium</em> &mdash; credited on the figure itself.</div>

<p class="refs">Figures are reproduced for classroom instruction. Titles and captions were adapted for this deck; please verify each citation against your own copy before redistributing the slides.</p>

{{% note %}}
- Worth naming the two books out loud: *Hands-On Large Language Models* is the practical reference if anyone wants to go deeper on the retrieval half, and Kelleher et al. is the standard textbook treatment of the similarity and nearest-neighbor material in section three.
{{% /note %}}
