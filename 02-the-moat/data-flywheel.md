# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | What It Measures | Score 1 | Score 5 | Score |
|------|------------------|---------|---------|-------|
| **Correction** | Do users fix AI outputs? Is that signal captured and reused? | No capture | Automated retraining | 3/5 |
| **Preference** | Does the product learn individual / team preferences over time? | Stateless | Deep personalization | 2/5 |
| **Domain Context** | Does usage in one area improve quality in adjacent areas? | Siloed | Cross-domain transfer | 3/5 |
| **Network** | Does each new user / team make the product better for everyone? | Isolated | Strong network effects | 3/5 |

**Correction Loop** - 3/5
What you capture today:
We capture user thumbs up/down. We capture edit signal for input, number of turns, escalation/abandonment, and full session traces (STDM) plus structured Feedback DMOs. Capture is rich and surfaced through Agent Analytics and Agent Optimization.
How it compounds:
Thumbs = positive signal, but today it compounds through a human. Signal flows into Optimization recommendations that an admin acts on (tune instructions, topics, actions) — capture → reuse is semi-manual, not automated retraining. Unrealized upside: auto-tune behavior from feedback DMOs, and ground the correction signal in the CRM outcome (did the case resolve, did the deal close), not just the trace.
**Preference Loop - 2/5**
What you capture today:
Personalization is retrieval-driven, not learned. The agent is grounded in Data 360 / CRM (account history, prior cases, entitlements) so context is rich, but the agent is largely stateless across sessions — it pulls preferences, it doesn't learn and adapt them per user or team over time.
How it compounds:
Weakly. Data 360 grounding is a head start pure-play CX agents must rebuild, but there's no durable memory layer that gets sharper at "how this account/rep likes to work" with use. This is the most exploitable gap — competitors make per-customer learning their core pitch.
**Domain Context Loop - 3/5**
What you capture today:
Shared Data 360 fabric, shared metadata, a shared library of topics/actions across the org, the Atlas Reasoning Engine, and Context Graph for AI. Usage in Service can inform Sales because they sit on the same data graph and action library.
How it compounds:
Structurally advantaged — one platform, one data fabric, one action library means transfer happens by construction. But it's transfer via shared data, not yet learned cross-domain improvement. Context Graph for AI is the lever to push this from 3 toward 5.
**Network Loop - 2/5**
What you capture today:
Within a tenant, more teams = more shared knowledge/library reuse. Across the ecosystem: AppExchange actions, MCP ecosystem, shared templates. Cross-tenant data learning is blocked by the multi-tenant trust boundary by design — one customer's data cannot improve another's agent.
How it compounds:
Capped at the data level on purpose. Network effects live at the ecosystem/marketplace layer and in aggregated, anonymized benchmarks. Low for everyone in enterprise (Microsoft and the vertical players hit the same wall), so it's a weak loop but not a unique vulnerability. Federated/aggregate benchmarking is the only trust-safe path to lift it.
Total Flywheel Score: 10/20
Weakest Loop: Preference (2/5). Network ties numerically but is capped industry-wide; Preference is where Agentforce is uniquely exposed, since deep per-customer/brand learning is the vertical attackers' entire wedge.
Fix for weakest loop: Ship a durable agent memory + preference-learning layer on top of Data 360 — per-rep, per-account, per-team adaptation that compounds with use, governed inside the trust boundary. Position it as "the agent that gets to know your business," contesting Sierra/Decagon's brand-intelligence pitch with the system-of-record advantage they can't match.

**Encroachment Threat Assessment**
1. Platform Encroachment
Attacker: Microsoft (Agent 365 + Azure AI Foundry + Copilot Studio)
Vector: Commoditize the agent operational layer and make it framework-agnostic. Agent 365, Evaluation APIs with custom graders, the open Agent Control Specification, ASSERT, and OTel-native ingestion turn observability/evals/governance into a horizontal utility bundled into the M365/Azure footprint — positioned as the neutral control plane above every agent vendor, including Agentforce. Targets the Correction loop + the whole ADLC operational layer.
Time-to-threat: Near — 6-12 months; much is already GA.
% of value at risk: ~30-40% of the operational-layer (eval/observability) value prop; lower for the full platform.
2. Vertical Competitor
Attacker: Sierra ($15.8B) and Decagon ($4.5B), in CX.
Vector: Win the Preference loop. Deep per-brand/per-customer learning (Sierra's "Agent OS," Decagon's plain-English Agent Operating Procedures) lands in CX — Agentforce's flagship use case — with personalization depth Agentforce doesn't yet match. Sierra is led by an ex-Salesforce co-CEO who knows the GTM and the gaps.
Time-to-threat: Already here; both winning enterprise CX deals now.
% of value at risk: ~20-30% of the CX segment specifically.
3. Adjacent Expansion
Attacker: Eval/observability pure-plays (Arize, Braintrust, Galileo/Cisco, LangSmith) + OpenAI moving down-stack.
Vector: Best-of-breed, model- and framework-agnostic eval/observability tooling expanding from dev tooling into enterprise agent ops — pulling eval/obs spend onto a separate budget line, out of the bundle. OpenAI expands from the model layer down into the agent platform.
Time-to-threat: Medium — 12-18 months to encroach meaningfully into Salesforce accounts.
% of value at risk: ~15-20%, concentrated in the eval/observability line item.

**90-Day Encroachment Plan**
Your partner played the Big Tech attacker. What was their plan to kill you?
Attacker: Microsoft (Agent 365 + Azure AI Foundry)
Attack vector (target the weakest loop): "Your observability and evals shouldn't be locked to your agent vendor." Free/bundled, framework-agnostic observability + evals that ingest any agent's OTel traces — including Agentforce's, since it now emits OTel — relegating Agentforce to one runtime among many feeding Microsoft's control plane.
Weeks 1-4 - what they ship: GA framework-agnostic agent observability + Evaluation APIs at no incremental cost on existing M365 E5 / Copilot licenses. OTel-native ingestion of any agent's telemetry. Push the Agent Control Specification as the open governance standard to fragment vendor-specific governance.
Weeks 5-8 - how they poach users: Sell IT/admins on a single pane of glass across all agents in a multi-vendor reality — zero new procurement, lands on the existing footprint. Co-opt the OpenTelemetry community narrative and claim the neutral-standard high ground before Salesforce can.
Weeks 9-12 - why users don't come back: Once telemetry, eval history, and cross-agent benchmarks live in Agent 365, leaving means losing the operational record and comparative baselines. The control plane becomes the sticky layer; the agent runtime becomes swappable.
Your defense: (1) Outcome-grounded evals — tie correction/eval signal to the business result in Data 360, not generic OTel spans; Microsoft sees the trace, only the system of record sees the outcome. (2) Close the loop in-platform — automate Correction → Improve via feedback DMOs so value lives in the loop, not the dashboard. (3) Own the standard first — ship the joint OpenTelemetry announcement and be the reference implementation so Microsoft can't claim neutrality. (4) Don't fight on dashboards; compete on outcome-grounded, data-grounded optimization only a system of record can do.
