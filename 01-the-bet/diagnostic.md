
***

# Three-Axis Vulnerability Diagnostic

## Product

**Product:** Agentforce Service Agent  
**Your Role:** Product Lead, AI Service Agents  

***

## Scores

### Contextual Moat — 3/5

Workflow depth × switching cost. Would users leave in a weekend if a competitor showed up? [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)

**Score rationale:**  
Agentforce is tightly embedded in Salesforce service workflows, case objects, and knowledge base, which creates real friction to rip‑and‑replace. [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)
But most surface‑level agent use cases (FAQ, simple flows) are still relatively easy for a customer to try with a horizontal bot vendor.  

**Named attacker (from partner challenge):**  
Zendesk + OpenAI‑powered bot for service, or an independent “AI helpdesk” startup that promises fast plug‑and‑play deflection.

***

### Data Advantage — 3/5

Proprietary signal that compounds with usage. What do you see that OpenAI doesn't? [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)

**Score rationale:**  
We sit on high‑volume, labeled service interactions (cases, chats, resolution outcomes) that can power better intent routing, escalation, and policy‑safe action. [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)
However, most of this data is still underused, and generic models can do “good enough” without deep Salesforce‑level signal unless we invest heavily in evals and learning loops.  

**Named attacker (from partner challenge):**  
Horizontal LLM platforms (OpenAI, Anthropic, Google) plus a thin integration partner that taps the same case logs without building a true Salesforce‑native data advantage.

***

### Platform Exposure — 4/5

Encroachment risk × pivot speed. If Apple/Google/OpenAI ships your hero feature native — then what? [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)

**Score rationale:**  
We are exposed: platform players can ship native “service copilot” features (answer suggestion, summarization, simple triage) directly inside CRMs or communication tools. [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)
Our hero features are at risk if we stay at the generic “chatbot in front of support” layer instead of going deeper into workflows, actions, and governance.  

**Named attacker (from partner challenge):**  
OpenAI or Anthropic partner with a major CRM (including Salesforce) to offer a first‑party “AI service assistant” as part of the platform license.

***

## Top Vulnerability

Our top vulnerability is **platform exposure**: if core agent capabilities (assist, triage, simple automation) become table stakes native features, Agentforce risks being seen as redundant. [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)
To win, we must differentiate on **deep workflow ownership**, **policy‑safe actions**, and **eval/guardrail/monitoring** that the generic platform tools don’t prioritize.  

***

## Confidence Level

Medium–high confidence.  
We see clear platform pressure and overlapping feature sets already, but the exact pace and shape of native “service copilot” offerings is still evolving. [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/01-the-bet/diagnostic.md)
