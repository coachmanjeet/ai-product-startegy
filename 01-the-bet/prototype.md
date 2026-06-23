
***

# The Prototype Bet

## What I Built

I built a **service copilot agent** that sits in front of a support queue and:  
- Understands a customer’s request (email or chat).  
- Summarizes context from past cases and account data.  
- Proposes an answer or next action, and decides when to escalate with full context.  

Think of it as “Agentforce for Tier‑1 service” that can deflect simple tickets and prep humans for the harder ones.

***

## Tool Used

- Salesforce Service Cloud (cases, knowledge base, routing).  
- Agentforce / Einstein bots for orchestration.  
- OpenAI / Anthropic‑style LLM for reasoning and natural language.  
- Simple eval and logging layer (resolution quality, escalation quality, guardrail checks).

***

## Prototype Link

- Internal demo: “Agentforce Service Agent — Tier‑1 Deflection and Agent Assist” (video / clickable flow).  
- Flow includes: customer asks a question → agent proposes response → evaluates risk → either auto‑responds or escalates with a one‑shot summary.

(You can drop in the actual Loom / URL here.)

***

## AI Value Archetype

This prototype is a mix of two archetypes:  
- **Co‑pilot / assist:** Drafts responses and summaries for human agents.  
- **Automation / workflow agent:** Safely auto‑resolves low‑risk, policy‑bounded requests (status checks, simple updates).

***

## The Bet in One Sentence

If we put Agentforce in front of our service queues, we can resolve a large chunk of customer issues automatically and make human agents dramatically faster, without breaking trust or governance.

***

## Kill Criteria

We should kill or radically pivot this bet if:  
- Containment and CSAT don’t beat today’s baseline for at least a few core intents.  
- Guardrail violations (wrong refunds, bad account changes) exceed an agreed safety threshold.  
- Adoption stalls: service teams don’t use the agent, or route meaningful work through it.  
- Platform vendors ship native features that do the same thing and customers prefer those out of the box.

If you share your actual demo flow, I can tighten “What I Built” and the archetype language to match exactly what’s implemented.
