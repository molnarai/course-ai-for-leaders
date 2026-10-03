# Agentic AI business solutions by industry

This mapping uses six business-solution groups from `SIX_BUSINESS_SOLUTIONS.md`. A filled matrix cell means a cited product description or customer story explicitly connects the solution and industry; a blank cell means **not evidenced by the references here**, not that the use case is impossible. Product marketing describes capabilities, whereas customer stories report use in a named organization. [web:17][web:52][web:31]

## Reference mapping

| Business solution | Industry | Reference and evidence type | What it supports |
|---|---|---|---|
| Customer-service resolution | Banking; insurance | [Salesforce Agentforce for Financial Services](https://www.salesforce.com/news/stories/agentforce-for-financial-services-announcement/) — product announcement [web:17] | Agents for lost-card reports, fee reversals, insurance coverage questions, and escalation. |
| Enterprise knowledge and research | Construction | [McCarthy Holdings / Glean](https://www.glean.com/resources/customer-stories/mccarthy-holdings-inc) — vendor-published customer story [web:52] | Search across company knowledge and agents for policy, project, and operational questions. Reported benefits are vendor/customer claims. |
| Software engineering and modernization | Banking | [Saxo Bank / Microsoft](https://www.microsoft.com/en/customers/story/24389-saxo-bank-github-copilot) — vendor-published customer story [web:16]; [GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent) — product documentation [web:44] | Saxo evidences AI-assisted coding in banking; GitHub separately documents an agent that takes an issue and prepares a pull request. **Do not infer that Saxo deployed that autonomous agent.** |
| IT service and incident operations | Telecommunications | [ServiceNow network-incident workflow](https://www.servicenow.com/docs/r/zurich/telecom-media-technology/now-assist-for-telecom-media-and-technology/network-incident-analysis-usecase.html) — product documentation [web:34] | Agentic analysis and coordination of telecommunications network incidents; not a named-customer result. |
| Sales and marketing execution | Retail | [Salesforce retail Agentforce presentation](https://www.salesforce.com/plus/experience/connections_2026/series/connections_2026_highlights/episode/episode-s1e32) — vendor presentation [web:33] | Campaign/content agents and segmented retail campaigns; the page's brand mentions do not establish deployment of every described agent by every brand. |
| Supply-chain and procurement orchestration | Retail; manufacturing; logistics | [Blue Yonder AI agents](https://blueyonder.com/why-blue-yonder/ai-and-machine-learning/ai-agents) — product page [web:31] | Supply-chain agents for planning, warehouse, transportation, and retail workflows. Evidence here is strongest for supply-chain orchestration, not every procurement subtask. |

## Business solution × industry

**Legend:** P = product documentation or advertisement; C = vendor-published customer story; A = AI-assistance story plus separate agent product documentation; — = no direct evidence in the references above. A cell establishes an *illustrative fit*, not adoption prevalence or proven ROI.

| Business solution | Banking | Insurance | Construction | Telecommunications | Retail | Manufacturing | Logistics |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Customer-service resolution | P [web:17] | P [web:17] | — | — | — | — | — |
| Enterprise knowledge and research | — | — | C [web:52] | — | — | — | — |
| Software engineering and modernization | A [web:16][web:44] | — | — | — | — | — | — |
| IT service and incident operations | — | — | — | P [web:34] | — | — | — |
| Sales and marketing execution | — | — | — | — | P [web:33] | — | — |
| Supply-chain and procurement orchestration | — | — | — | — | P [web:31] | P [web:31] | P [web:31] |

**Interpretation:** This is an evidence map of the selected references, not a survey of all industries. In particular, “A” is not proof of autonomous coding-agent deployment at Saxo Bank. [web:16][web:44]

## Independent research (evidence type I)

Added 2026-10-01. **I** = research with a stated method (experiment, benchmark, or tribunal record), not published by a vendor selling the product. Full citations and caveats are in `REFERENCES.md`. A "Tech and services" column is added because most of these studies were run at software, cloud and consulting firms.

| Business solution | Banking | Insurance | Construction | Telecommunications | Retail | Manufacturing | Logistics | Tech and services |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Enterprise knowledge and research | — | — | C | — | — | — | — | I (Dell'Acqua et al.; consulting) |
| Software engineering and modernization | A | — | — | — | — | — | — | I (Cui et al.; METR) |
| IT service and incident operations | — | — | — | P | — | — | — | I (Roy et al.; cloud) |
| Supply-chain and procurement orchestration | — | — | — | — | P, I (Yin et al.; JD.com) | P | P | — |
| Customer-service resolution | P | P | — | — | I (Fang et al.) | — | — | I (Brynjolfsson et al.; software firm) |
| Sales and marketing execution | — | — | — | — | P, I (Fang et al.) | — | — | — |

Not placed in the matrix: *Moffatt v. Air Canada* (airline; customer service) and the two benchmarks (TheAgentCompany, τ-bench), which are not industry-specific.

**Interpretation:** most I entries measure AI *assistance* to people rather than autonomous agents, and several report on the authors' own firm. They strengthen the evidence that the tools affect work; they do not establish return on an autonomous deployment.
