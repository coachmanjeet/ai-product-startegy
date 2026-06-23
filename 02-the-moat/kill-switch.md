Let’s wire this to Agentforce and make it feel real but still simple. [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/02-the-moat/kill-switch.md)

You can paste the following into `kill-switch.md` and adjust labels if you change vendors later.

***

# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State (Agentforce Service Agent) | Risk Level | 48-Hour Action |
|---|---|---|---|
| **Provider** | Primary LLM provider: OpenAI/Anthropic for core reasoning; Salesforce platform for orchestration and data. | M | Identify at least one backup LLM (e.g., Claude vs. GPT) and validate that key prompts run acceptably on both. |
| **Abstraction** | Thin abstraction: prompts and orchestration partially hard‑coded to one provider’s APIs and response format. | H | Wrap LLM calls in a provider‑agnostic interface and store prompts/versioning in config, not application code. |
| **Routing** | Most traffic goes to a single LLM; routing is static, not cost/latency/quality aware. | M | Add a simple router that can switch between providers per intent/tenant, and a manual override “switch” in config. |
| **Eval** | Eval stack (quality, safety, cost) is partially tied to one provider’s telemetry and tools. | M | Export eval metrics to our own store (e.g., Data Cloud/Snowflake) and ensure we can run them regardless of provider. |

***

## Portability Score

**Qualitative score:** Medium.  
We can move off our primary LLM with work, but not in a weekend; orchestration and evals still assume that provider’s shape of responses and tools. [github](https://github.com/coachmanjeet/ai-product-startegy/blob/main/02-the-moat/kill-switch.md)

***

## If [primary vendor] doubles pricing tomorrow:

- Immediately route low‑value, low‑risk intents to a cheaper backup model using the abstraction layer.  
- Freeze new use cases on the expensive provider; prioritize optimization of prompt length, context windows, and caching.  
- Kick off a 30‑day migration plan for at least one major queue to the backup provider to prove portability in practice.

***

## If [primary vendor] ships a competing product:

- Assume they will bundle a “service copilot” that overlaps with Agentforce’s surface features.  
- Double‑down on Salesforce‑native data, workflow depth, and eval/guardrail/monitoring as our differentiation.  
- Prepare a narrative and pricing strategy that positions Agentforce as the **trusted, governed** layer on top of any foundation model, not just one vendor.
