# Cost Curve & Pricing Strategy

## Cost Model

| Cost Category              | Per-User/Month | Notes |
|---------------------------|----------------|-------|
| Inference (primary model) | ~$0.18         | Frontier model (GPT‑4.1‑class). Avg 30 queries/user/month. 2K input + 2K output tokens each. 4K tokens * $0.0015 per 1K * 30 ≈ $0.18. |
| Inference (cascading/triage) | ~$0.04      | Cheaper model (GPT‑4o‑mini‑class). Handles ~80% of queries. 1K tokens/request * 30 queries * $0.0005 per 1K ≈ $0.04. |
| Infrastructure            | ~$0.05         | Shared infra for this feature (API gateway, vector DB, observability, logging). Assume $5K/month spread over 100K active users → ~$0.05/user. |
| Data/storage              | ~$0.02         | Conversation history, embeddings, and logs. ~2 GB per 1K users. Storage + retrieval ≈ $20/month per 1K users → ~$0.02/user. |
| Human-in-the-loop         | ~$0.03         | Quality review and escalation. 1 FTE at $150K covering 50K users → ~$0.25/user/year ≈ $0.02/month. Add buffer → $0.03. |
| **Total AI COGS**         | **~$0.32**     | Target: keep AI COGS ≤ 10–15% of ARPU for this feature. At $20+ AI uplift per seat, margin is very healthy. |

## Cascading Strategy

<!-- Cheap model → frontier model routing logic -->

**Triage model:**  
Use a cheaper, fast model (GPT‑4o‑mini‑class) for default queries, low‑risk actions, summarization, and basic Q&A.

**Frontier model:**  
Use a frontier model (GPT‑4.1‑class) for complex reasoning, multi‑step workflows, security‑sensitive or policy‑impacting actions, and high‑stakes outbound communication.

**Routing rule:**  
Start every request on the triage model. Escalate to the frontier model when any of these are true:  
- Confidence score or internal quality score < 0.7.  
- Task type in {“customer‑visible email or proposal”, “security or compliance‑sensitive action”, “large multi‑step workflow”}.  
- User explicitly turns on “High accuracy mode” for a given task.

**Expected cascade ratio:**  
Target 70–90% of requests on the triage model and 10–30% on the frontier model. Continuously monitor quality and adjust thresholds to protect margin without hurting user experience.

## Pricing Model

**Current pricing:**  
Core product priced at ~$50 per seat per month, with ~80% gross margin, and AI not separately priced today.

**Proposed AI pricing:**  
Introduce an “AI Pro” tier at $70 per seat per month that includes the AI agent, with soft limits (for example, 200 AI tasks/seat/month) and optional metered overages for heavy users. For enterprise, offer AI as a bundled capability in upper tiers with committed volumes and discounts.

**Model:**  
Hybrid – base seat uplift plus usage‑based overages for the heaviest users. Seat uplift captures the bulk of value, while metering prevents a small group of power users from eroding margins.

## Stress Tests

| Scenario                                  | Impact on Margin                                                                 | Response                                                                                          |
|-------------------------------------------|----------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| Inference costs 3x                        | AI COGS per user jumps from ~$0.32 to roughly ~$0.80. Gross margin on AI uplift compresses by several points. | Tighten routing to push >90% of traffic to triage model, reduce tokens per request by ~30%, and adjust overage rates for very heavy users. |
| Heaviest segment doubles usage           | Top 10–20% of users drive 2x–3x more tokens, increasing blended COGS and lowering margins for that cohort.    | Introduce clearer fair‑use limits, enforce overages beyond included volume, and add caching/reuse of prior context to avoid recomputing. |
| Model provider raises prices 50%         | Frontier model COGS increase materially; total AI COGS/user rises by ~$0.10–0.15.                                | Shift more traffic to triage, renegotiate enterprise commitments, experiment with alternative providers, and revisit list prices for new contracts. |

## Board One-Pager

<!-- Before/After: Old SaaS revenue vs. AI usage revenue for your product -->

**Before (traditional SaaS):**  
Revenue and margin tied almost entirely to seats and tiers (for example, $50/seat/month, ~80% gross margin). Limited upside from power users once a seat is sold.

**After (AI-enabled):**  
Seat‑based revenue remains, but AI introduces a second growth lever: value‑based AI tiers and usage‑linked overages. AI COGS per seat are low (~$0.32/user/month) relative to the incremental AI price uplift (for example, +$20/seat/month), creating room for >90% gross margin on the AI portion while still protecting affordability and competitiveness.

**Net margin shift:**  
AI turns the product from pure seat‑based SaaS into a hybrid seat + usage business with high incremental margins. As AI adoption grows, a larger share of revenue comes from high‑margin AI features, improving overall gross margin and giving more flexibility for discounts, bundles, and expansion in enterprise deals.
