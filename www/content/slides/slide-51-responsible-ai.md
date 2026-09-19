+++
title = "Responsible AI"
description = "How to govern Agentic AI systems"
weight = 51
outputs = ["Reveal"]
math = true
thumbnail = "/imgs/slides/responsible_ai_3.png"

[reveal_hugo]
custom_theme = "css/reveal-robinson.css"
slide_number = true
transition = "none"

+++

{{< slide background-image="/imgs/slides/responsible_ai_3.png" >}}
<div style="min-height: 15em;"></div>
<div style="margin:0; padding: 50; background-color: rgba(0,0,0,0.5); min-hight:100%; min-width:100%" >
    <h1 style="color:white; text-shadow: 2px 2px 4px rgba(0,0,0,0.7);" >Responsible AI</h1>
    <p style="color:white; text-shadow: 2px 2px 4px rgba(0,0,0,0.7);" > EMBA 8160 — Session 5</p>
</div>

{{% note %}}


{{% /note %}}



***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_00.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_01.png" >}}
<h1></h1>

***
### Core Principles

<p style="font-size: small; text-align: right">as established in the EU's Ethics Guidelines for Trustworthy AI
</p>

<div style="display: flex; flex-direction: column; gap: 12px; font-size: 0.55em;">

<div style="background: rgba(255,255,255,0.07); border: 1px solid rgba(255,255,255,0.15); border-radius: 10px; padding: 12px 18px; text-align: left;">
<h3 style="margin:0 0 4px 0;">Beneficence</h3>
AI should actively benefit people and society — not merely avoid harm. The obligation is positive: to do good, not just to refrain from doing harm.
</div>

<div style="background: rgba(255,255,255,0.07); border: 1px solid rgba(255,255,255,0.15); border-radius: 10px; padding: 12px 18px; text-align: left;">
<h3 style="margin:0 0 4px 0;">Non-maleficence</h3>
AI must not cause harm, including through inaction, unintended side effects, or emergent behavior. This is the classical medical principle "do no harm" extended to autonomous systems.
</div>

<div style="background: rgba(255,255,255,0.07); border: 1px solid rgba(255,255,255,0.15); border-radius: 10px; padding: 12px 18px; text-align: left;">
<h3 style="margin:0 0 4px 0;">Autonomy</h3>
Respect for people's ability to understand, contest, and override AI decisions that affect them. This operationalizes as informed consent, explainability, and meaningful override mechanisms — the right not just to be informed but to actually exercise control.
</div>

<div style="background: rgba(255,255,255,0.07); border: 1px solid rgba(255,255,255,0.15); border-radius: 10px; padding: 12px 18px; text-align: left;">
<h3 style="margin:0 0 4px 0;">Justice</h3>
The benefits and burdens of AI should be distributed fairly across groups and geographies. This covers both procedural justice (fair process) and distributive justice (fair outcomes) — and directly motivates bias and fairness requirements in system design.
</div>

<div style="background: rgba(255,255,255,0.07); border: 1px solid rgba(255,255,255,0.15); border-radius: 10px; padding: 12px 18px; text-align: left;">
<h3 style="margin:0 0 4px 0;">Explicability</h3>
AI behavior must be understandable and auditable by the relevant stakeholders — at the appropriate level of abstraction for each audience. A patient, a clinician, and a regulator need different explanations of the same decision; all three are legitimate.
</div>

</div>

*** 

{{< slide content-image="/imgs/Engineering_Agentic_Governance_02.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_03.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_04.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_05.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_06.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_07.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_08.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_09.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_10.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_11.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_12.png" >}}
<h1></h1>

***

{{< slide content-image="/imgs/Engineering_Agentic_Governance_13.png" >}}
<h1></h1>

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
</style>

### The Regulatory Landscape
# US State-Level AI Legislation

<div style="display:grid; grid-template-columns:1fr 1fr; gap:0 1.6em; font-size:0.52em; align-items:start;">
<div>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;">New York &mdash; Advanced AI Licensing Act (A 8195):</strong> Requires developers and operators of certain &ldquo;high-risk advanced AI&rdquo; to obtain a licence. Related bills, such as an amendment in the Illinois legislature (HB 1002), require state certification for the use of diagnostic algorithms.</p>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;">Rhode Island (H 6286):</strong> Mandates a &ldquo;distinctive watermark&rdquo; to authenticate content generated by generative AI.</p>
<p style="margin:0;"><strong style="color:#CC0000;">District of Columbia &mdash; Stop Discrimination by Algorithms Act (B 114):</strong> Requires notice about how AI is used in employment, including the source of information, and a separate notice to individuals affected by algorithmic eligibility determinations.</p>
</div>
<div>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;">Massachusetts &mdash; Act Preventing a Dystopian Work Environment (HB 1873):</strong> Requires employers or vendors using AI to provide specific notices.</p>
<p style="margin:0 0 0.7em 0;"><strong style="color:#CC0000;">Washington (HB 1951):</strong> Requires developers of automated decision tools to disclose to deployers the types of data used to program or train the tool, and how the tool was evaluated for validity.</p>
<p style="margin:0;"><strong style="color:#CC0000;">California (AB 331) and New York (AB 7859):</strong> Bills that would require AI deployers to allow individuals to opt out of decisions based on automated decision-making.</p>
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

# Class Discussion



***

### Discussion Question 1
# Foundations of AI Ethics

An agentic AI system deployed in a hospital autonomously schedules and cancels patient appointments based on resource optimization. A patient misses a critical follow-up and suffers a worsening condition.

How do the five core ethical principles map onto this scenario, and which principle do you consider most violated?

***

### Discussion Question 2
# Bias &amp; Fairness

Your team is building a loan-decision agentic system for a regional bank. You discover that historical lending data reflects decades of discriminatory lending practices.

You have three options: (A) train on the data as-is, (B) remove protected attributes from features, or (C) apply fairness-aware re-weighting. What is your recommendation and why? What fairness metric would you use to validate it?

***

### Discussion Question 3
# Accountability &amp; Oversight

You are designing an agentic customer service system for a financial services firm. The system can autonomously resolve disputes, issue refunds up to $\$500$, and escalate to human agents.

A proposal is made to raise the autonomous refund threshold to $\$5,000$ to reduce human workload by 80%. What autonomy level would you recommend for this new threshold, and what safeguards would you require before approval?


***

### Discussion Question 4
# Governance

Your organization wants to deploy an agentic AI system that monitors employee communications (Slack, email, documents) to detect IP theft and policy violations. The system will flag suspicious behavior to HR.

What governance structures, consent mechanisms, and technical safeguards would you require before approving this deployment, and are there conditions under which you would refuse to build it?

*** 

### Discussion Question 5
# Synthesis

You have been hired as the AI Ethics Lead at a startup deploying a multi-agent system to autonomously manage a portfolio of real estate investments — identifying properties, negotiating purchase terms, managing tenants, and initiating legal proceedings when necessary.

Using any frameworks discussed today, identify the three most significant ethical risks and design one concrete mitigation for each. Would you take this job?
