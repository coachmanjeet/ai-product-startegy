# **Your Role:**

> A living strategy built across 6 sessions. Each module adds one component. By Module 6, this repo IS the strategy — version-controlled, board-ready, portable.

---

## Strategy at a Glance

| Component | Module | Status | Key Artifact |
|-----------|--------|--------|-------------|
| **The Bet** | M1 | [x] | `01-the-bet/` |
| **The Moat** | M2 | [ ] | `02-the-moat/` |
| **The Margin** | M3 | [x] | `03-the-margin/` |
| **The Contract** | M4 | [x] | `04-the-contract/` |
| **The Guardrails** | M5 | [x] | `05-the-guardrails/` |
| **The Pitch** | M6 | [x] | `06-the-pitch/` |

---

## The Bet (M1)

**What we're building, for whom, why now.**

- **Product:** **Your Role:**
- **AI Value Archetype:** _(add: Automator / Copilot / Oracle / Creator / Orchestrator)_
- **Vulnerability Scores:** _(add: Moat _/5 · Data _/5 · Platform _/5)_
- **Top Risk:**
- **Confidence:** _(add: H / M / L)_
- **Prototype:**
- **Kill Criteria:**

→ Details: [`01-the-bet/`](01-the-bet/)

---

## The Moat (M2)

**Why this won't get copied in 6 months.**

- **Data Flywheel Score:**
- **Weakest Loop:**
- **Top Encroachment Threat:**
- **Encroachment Defense:**
- **Vendor Portability:** _(add: Ready / Partial / Locked)_

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
- **Confidence UX:** show uncertainty / tiered confidence / human-in-loop trigger
- **HITL Architecture:**
- **Failure Mode Coverage:** *What failure mode did your partner find that you missed?*

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

- **Horizon 1 (Now):**
- **Horizon 2 (Next):**
- **Horizon 3 (Bet):**
- **Board Narrative:** **The case:**
- **Ask:** ## M1 Baseline vs. Now
- **Key Strategic Change:**

→ Details: [`06-the-pitch/`](06-the-pitch/)
