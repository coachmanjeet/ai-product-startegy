# Agentforce Service Agent

> If we put Agentforce in front of our service queues, we can resolve a large chunk of customer issues automatically and make human agents dramatically faster, without breaking trust or governance.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [x] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [x] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** Agentforce Service Agent
- **AI Value Archetype:** This prototype is a mix of two archetypes:
- **Vulnerability Scores:** Moat 3/5 · Data 3/5 · Platform 4/5
- **Top Risk:** Our top vulnerability is **platform exposure**: if core agent capabilities (assist, triage, simple automation) become table stakes native features, Agentforce risks being seen as redundant.…
- **Confidence:** _(add: H / M / L)_
- **Prototype:** Internal demo: “Agentforce Service Agent — Tier‑1 Deflection and Agent Assist” (video / clickable flow).
- **Kill Criteria:** We should kill or radically pivot this bet if: - Containment and CSAT don’t beat today’s baseline for at least a few core intents. - Guardrail violations (wrong refunds, bad account changes) exceed an agreed safety threshold.…

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:**
- **Weakest Loop:**
- **Top Encroachment Threat:**
- **Encroachment Defense:**
- **Vendor Portability:** Qualitative score: Medium.

→ Details: [`02-the-moat/`](02-the-moat/)

---

## The Margin (M3)

**Will this make money or bleed it?**

- **Gross Margin (current):** 80%
- **Gross Margin (AI-adjusted):** 90%
- **Pricing Model:** Hybrid – base seat uplift plus usage‑based overages for the heaviest users. Seat uplift captures the bulk of value, while metering prevents a small group of power users from eroding margins.
- **Pricing Today → Tomorrow:** Core product priced at ~$50 per seat per month, with ~80% gross margin, and AI not separately priced today. → Introduce an “AI Pro” tier at $70 per seat per month that includes the AI agent, with soft limits (for example, 200 AI tasks/seat/month) and optional metered overages for heavy users. For enterprise, offer AI as a bundled capability in upper tiers with committed volumes and discounts.
- **Total AI COGS / unit:**
- **Cascading Strategy:** Triage: Use a cheaper, fast model (GPT‑4o‑mini‑class) for default queries, low‑risk actions, summarization, and basic Q&A.; frontier: Use a frontier model (GPT‑4.1‑class) for complex reasoning, multi‑step workflows, security‑sensitive or policy‑impacting actions, and high‑stakes outbound communication.; ratio Target 70–90% of requests on the triage model and 10–30% on the frontier model. Continuously monitor quality and adjust thresholds to protect margin without hurting user experience.
- **Net Margin Shift:** AI turns the product from pure seat‑based SaaS into a hybrid seat + usage business with high incremental margins.…
- **Break-even at:**

→ Details: [`03-the-margin/`](03-the-margin/)

---

## The Contract (M4)

**Why users will trust a probabilistic system.**

- **Reliability Target:**
- **Golden Dataset:** 5 rows, __ adversarial
- **Confidence UX:** show uncertainty, use tiered confidence bands, and trigger human‑in‑the‑loop when the agent is unsure or risk is high.
- **HITL Architecture:** - Agentforce proposes responses and actions but routes through a **human review layer** for medium‑confidence or high‑risk flows.…
- **Failure Mode Coverage:** What failure mode did your partner find that you missed? - Example: Agentforce tried to “help” by guessing a policy that wasn’t documented, effectively hallucinating a refund rule.…

→ Details: [`04-the-contract/`](04-the-contract/)

---

## The Guardrails (M5)

**What breaks when this scales — and what compounds.**

- **Compounding System:** | Loop | Input | Output | Compounds? | Status | |------|-------|--------|-----------|--------| | **Recursive Learning** — corrections feed the model | Agent edits to drafted replies + thumbs-down + "Wrong/unsafe answer" …
- **Governance Posture:** All Agentforce Service Agent interactions in customer-facing channels (case replies, chat, email drafts) and internal-facing actions on Salesforce records (read, summarize, suggest, draft).…
- **Autonomy Boundaries:** - *Allowed without human approval:* read Salesforce records the user already has access to; summarize cases/threads; suggest next steps; draft (not send) customer-facing replies; create internal notes flagged "AI-drafted".
- **Escalation Triggers:** - Confidence <70% → "Draft for review" only, route to AI-escalation queue with evidence links.
- **Audit Cadence:** - *Daily:* automated golden-dataset run + Trust Layer log scan for policy violations.
- **Shadow AI Audit (user-side):** 6 workarounds found · 4 governed, 2 killed (this cohort); pending re-scan in 30 days. build candidates · adjacent spend ~$180k/yr across personal SaaS subs, surprise OpenAI usage, and unmanaged seats — recoverable as Agentforce expansion ARR once flows are migrated.
- **Agent Boundaries:** | Agent | Can do | Cannot do | Approves what | Approver | |------|--------|-----------|---------------|----------| | **Service Triage Agent** | Read case + history; classify intent; route to queue; suggest KB | Send messages; modify case fi…
- **Regulatory Exposure:** - **EU AI Act:** Service Agent is a *limited-risk* system (transparency obligations) for general case handling; *high-risk* when used in HR/credit/insurance customer flows — those require conformity assessment, logging, …

→ Details: [`05-the-guardrails/`](05-the-guardrails/)

---

## The Pitch (M6)

**How you get this funded, shipped, and adopted.**

- **Horizon 1 (Now):** Launch Agentforce service agent for top 3 support queues (billing, login, order status) to deflect Tier‑1 tickets. · Build eval and guardrail layer (coverage, hallucination, escalation quality) for all agent interactions. · Integrate with existing Salesforce case flows and knowledge base, no schema changes. · Stand up monitoring dashboard for CSAT, containment, and agent failure modes.
- **Horizon 2 (Next):** Expand to omni‑channel (web, mobile, email, chat) with a single agent brain and shared memory. · Introduce workflow‑driven agents that can **act** (refunds, plan changes, address updates) under policy constraints. · Launch agent‑assist for human agents (response suggestions, next‑best‑action, summarization). · Roll out continuous eval framework (offline sims + online shadow mode) across top 10 intents.
- **Horizon 3 (Bet):** Autonomous “service pods” for specific products/segments where Agentforce owns end‑to‑end resolution, routing, and feedback loops. · Closed‑loop learning from service data into product/ops (auto issue detection, playbook generation, backlog prioritization). · Marketplace of reusable agent skills and templates for partners/customers built on Agentforce.
- **Board Narrative:** Agentforce turns our service organization into an AI‑powered, always‑on, low‑latency front door that resolves customer problems faster, cheaper, and with better insight than human‑only support.…
- **Ask:** - Fund 12–18 months of Agentforce Service Agent build‑out (team, infra, eval tooling).
- **Key Strategic Change:**

→ Details: [`06-the-pitch/`](06-the-pitch/)
