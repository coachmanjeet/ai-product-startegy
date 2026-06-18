# Compounding System Design

> Product: **Agentforce Service Agent** (Salesforce) — case triage, summarization, draft replies, status lookup, deflection.
> Test: freeze 3 months (≈ one frontier cycle) — does the product still win? If yes, it's not compounding, it's scaling.

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| **Recursive Learning** — corrections feed the model | Agent edits to drafted replies + thumbs-down + "Wrong/unsafe answer" reports + golden-dataset failures | Per-org fine-tunes & prompt updates; failed rows promoted into the eval set so the same miss can't ship twice | Y | active (capture wired; retraining cadence still weekly-manual) |
| **Cross-Domain Transfer** — a win in one cloud lifts the next | Resolution patterns learned in Service Cloud (case + entitlement + KB) | Better grounding for Sales Cloud (renewal risk on stuck opps), Field Service (dispatch summaries), Marketing Cloud (journey churn signals) — same Data Cloud spine | Y | broken (signal captured, but cross-cloud prompt grounding not yet enabled — siloed by cloud team) |
| **Network Intelligence** — fleet patterns, privacy-gated | Anonymized intent → resolution paths across all customer orgs (with explicit opt-in via Trust Layer) | Industry-vertical packs (SaaS, FSI, Healthcare) of intents, deflection plays, refusal templates that ship to every tenant | Y | missing (Trust Layer privacy gate exists; no aggregation pipeline or vertical pack release process yet) |

**Broken loop identified by partner:** Cross-Domain Transfer. Corrections logged in Service Cloud do not improve grounding for the same customer's Sales/Field Service agents — each cloud's agent re-learns from scratch. Partner's attack: a vertical competitor (e.g., ServiceTitan-style stack) ships one agent that shares context across the whole workflow and out-learns us inside 6 months.

**Fix plan:**
1. Land a single Data Cloud–backed "customer context object" that all Agentforce agents read/write (Q3).
2. Promote correction events from Service into a shared eval set keyed by *customer + intent*, not by cloud (Q3).
3. Quarterly cross-cloud regression: run Service-trained corrections against Sales/FS golden rows; block release if cross-domain accuracy drops >3% (Q4).

## Context Connectivity
<!-- How does knowledge flow across teams and domains? Where does it silo? -->

- **Flows today:** Case → KB article suggestion (one-way); rep edits → eval backlog (one-way, manual triage); Trust Layer audit log → security team.
- **Silos today:**
  - Service Cloud corrections never reach Sales/Field Service prompt grounding (the broken loop above).
  - "Report a wrong answer" feedback lives in a CSAT table; not joined to the golden dataset until a human PM triages it weekly.
  - Admin-level overrides (queue disables, action lockouts) are not surfaced back to model owners as a quality signal.
- **Target connectivity:** every correction, override, and escalation lands as a typed event on Data Cloud within 24h, queryable by intent × cloud × segment, with a closed-loop ticket to the responsible model owner.

## Governance Policy

**Scope:** All Agentforce Service Agent interactions in customer-facing channels (case replies, chat, email drafts) and internal-facing actions on Salesforce records (read, summarize, suggest, draft). Excludes: any record mutation classified destructive (delete, mass update, contract cancellation, refund issuance) — those remain human-only.

**Autonomy boundaries:**
- *Allowed without human approval:* read Salesforce records the user already has access to; summarize cases/threads; suggest next steps; draft (not send) customer-facing replies; create internal notes flagged "AI-drafted".
- *Requires human approval:* sending any customer-facing message; creating/closing cases; updating entitlements, opportunities, or contracts; cross-object writes.
- *Hard-blocked (no override):* delete operations, bulk updates, PII extraction, policy exceptions outside published rules, anything triggering a SOX-/HIPAA-tagged field.

**Escalation triggers:**
- Confidence <70% → "Draft for review" only, route to AI-escalation queue with evidence links.
- Policy/PII detector fires → block + log + human review.
- 3 consecutive thumbs-down on the same intent in one org → auto-disable that intent for that org and page the model owner.
- Hallucination rate >5% in any 7-day window on golden dataset → freeze release, page on-call.

**Audit cadence:**
- *Daily:* automated golden-dataset run + Trust Layer log scan for policy violations.
- *Weekly:* eval review (accuracy, hallucination, drift) with model owner; promote new failed rows into the eval set.
- *Monthly:* governance review with Legal + Security covering refusals, overrides, escalations, and Shadow AI inventory delta.
- *Quarterly:* third-party red team + EU AI Act conformity check.

**Regulatory exposure (EU AI Act / other):**
- **EU AI Act:** Service Agent is a *limited-risk* system (transparency obligations) for general case handling; *high-risk* when used in HR/credit/insurance customer flows — those require conformity assessment, logging, and human oversight documentation. Action: tag deployments by industry; high-risk tenants get the gated config (mandatory pre-send review, full audit log retention 6+ months).
- **GDPR / CCPA:** Trust Layer must mask PII before model call; right-to-erasure must propagate to fine-tune sets within 30 days.
- **SOC 2 / ISO 27001:** every prompt/response logged with user, role, record IDs; retained per customer DPA.
- **HIPAA (Healthcare tenants):** BAA required; PHI never leaves the customer's tenant boundary; refusals enforced for PII summarization.
- **Sector overlays to flag:** NYDFS Part 500 (FSI), FDA SaMD (rare, but Healthcare cohorts ask), India DPDP Act (2026 enforcement underway).

## Agent Topology
<!-- If using agents: what can each agent do? What can't it do? Who approves what? -->

| Agent | Can do | Cannot do | Approves what | Approver |
|------|--------|-----------|---------------|----------|
| **Service Triage Agent** | Read case + history; classify intent; route to queue; suggest KB | Send messages; modify case fields beyond status | Auto-approves routing under high confidence | Service Cloud admin (config only) |
| **Case Reply Drafter** | Draft customer reply with cited evidence; surface confidence badge | Send the reply; promise dates/refunds; extract PII | Drafts go to rep for pre-send review | Human rep (always, in early rollout) |
| **Resolution Suggester** | Suggest next steps grounded in similar resolved cases | Take action on the case; write to entitlement | Suggestions only; rep takes action | Human rep |
| **SLA / Entitlement Checker** | Read-only mapping case → SLA; Y/N + explanation | Modify entitlement; grant exceptions | Read-only; no approval needed | n/a |
| **Escalation Router** | Open AI-escalation tickets with evidence; tag severity | Close cases; contact customers | Auto-files under threshold | On-call lead reviews daily |
| **Admin Override Console** (human, not agent) | Disable any agent per queue/region; lock destructive actions | — | Approves all topology changes | Service ops + Security |

Topology principle: **drafts, never sends; reads broadly, writes narrowly; every write is reversible or human-approved.**

## Shadow AI Audit

| Tool | Owner | Risk Level | Decision |
|------|-------|-----------|----------|
| ChatGPT Plus seats used by individual reps to rewrite customer replies | Unowned (personal accounts) | H — customer data into a non-DPA tool, no audit log | **govern** — replace with Agentforce drafter; block paste-to-web of case content via DLP; SSO-enforce approved AI tools |
| Grammarly Business on rep workstations | IT (procured) | M — limited customer-data exposure on tone/grammar | **govern** — keep, but restrict to no-content-retention tier; add to AI inventory |
| Notion AI in CS knowledge wiki | CS Ops | M — internal KB drafts, no customer PII, but ungoverned model usage | **govern** — keep, document data flow, exclude PII fields |
| Custom Zapier + OpenAI flow auto-summarizing tickets to Slack | A team lead | H — bypasses Trust Layer, raw case text to OpenAI, no audit | **kill** — replace with Agentforce summary action posted via approved Slack app |
| Internal "ask-the-docs" RAG built by an SE on a personal API key | Solo engineer | H — uncontrolled key, no review, exposes internal runbooks | **kill** — migrate to sanctioned Einstein Trust Layer endpoint |
| Otter.ai on customer calls | Sales (some reps) | M — recordings + transcripts of customer calls outside of Salesforce | **govern** — mandate Einstein Conversation Insights; Otter blocked on managed devices |

**Total tools found:** 6 (initial sweep — expect 12–20 after expense + browser-extension audit completes).
**Tools after triage:** 4 governed, 2 killed (this cohort); pending re-scan in 30 days.
**Estimated hidden spend:** ~$180k/yr across personal SaaS subs, surprise OpenAI usage, and unmanaged seats — recoverable as Agentforce expansion ARR once flows are migrated.
