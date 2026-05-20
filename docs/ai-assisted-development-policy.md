# AI-Assisted Development Policy

> AI assistance is now part of how software gets built. The question is not whether engineers use it — they will — but whether the organization channels that usage into safer, faster, higher-quality outcomes. This policy is how I do that.

## Core stance

**Every engineer is expected to use AI assistance.** It is part of the job, like an IDE or version control. *And* every engineer is fully accountable for what they ship. The tool does not absorb accountability.

## The four rules

1. **You are the author of record.** No exceptions. AI-generated code carries your name on the PR.
2. **AI-generated code passes the same gates as human code.** Review, tests, security scanning, dependency policy, license check.
3. **Sensitive data does not leave approved tools.** Customer data, secrets, PII, and unreleased financials are only sent to AI tools on the approved list, configured per our data agreement.
4. **High-stakes systems require dual control.** Changes to auth, payments, data deletion, infra security, and model training pipelines require a human-authored review *and* a second human approver, regardless of how the code was generated.

## What is encouraged

- **Code generation, refactors, scaffolding.** Yes.
- **Test generation.** Yes — and we measure whether AI-generated tests actually catch regressions, not just whether they pass.
- **Code review assistance** (draft suggestions for the reviewer). Yes.
- **Documentation, ADR drafts, postmortem timelines.** Yes — author of record is still human.
- **Triage assistance during incidents.** Yes, with a human IC ([incident management](incident-management.md)).
- **AI agents that take actions** (open PRs, file tickets, run scripts). Yes — sandboxed, with audit logs, with a human approval step for any production change.

## What requires explicit approval

- **Autonomous agents acting on production systems.** Approved via the [architecture review process](architecture-review-process.md).
- **Training or fine-tuning on customer data.** Approved by Security + Legal + the relevant product lead.
- **AI features customers see** (model-backed product features). Treated as products: have SLOs, evals, and rollback plans.
- **New AI vendors or models.** Approved by the AI Adoption enabling team and Security, then added to the allowlist.

## What is prohibited

- Pasting customer data, secrets, or unreleased material into non-approved tools.
- Shipping AI-generated code without reading it.
- Using AI to generate evidence for performance reviews, leveling, or hiring decisions.
- Bypassing security review on the grounds that the code "came from a model."
- Using AI usage rates as an individual performance metric. (See [scorecard](metrics-scorecard.md).)

## Evals: how we know AI features work

Any customer-facing AI feature has an **eval suite** before launch and a **continuous eval pipeline** after.

| Eval type | Purpose | When |
|---|---|---|
| Offline benchmark | Known-answer regression set | Every model or prompt change |
| LLM-as-judge | Subjective quality at scale | Nightly on sample of prod traffic |
| Human review | Ground truth on edge cases | Weekly on a sampled set |
| Safety / red-team | Adversarial inputs | Pre-launch and quarterly |

Evals are *first-class* artifacts: stored in the repo, versioned, with owners. An AI feature without evals is treated like a service without tests — it doesn't ship.

## Operational guardrails

- **Cost.** AI tooling costs are budgeted per team and reported monthly. Run-away cost is treated like any infra cost runaway: it pages the team.
- **Latency.** AI calls in user-facing paths must have a timeout and a graceful fallback.
- **Provenance.** Every AI call to a production system is logged with: model, prompt template version, input hash, output hash, caller.
- **Prompt management.** Prompts that affect production behavior are version-controlled like code, reviewed like code, and rolled back like code.

## Org structures that make this work

- An **AI Adoption enabling team** ([team topologies](team-topologies.md)) — time-boxed, helps product teams adopt safely, then disbands or rotates.
- An **Applied AI / model serving team** for shared infrastructure (gateway, evals harness, prompt registry, vector stores).
- **Staff+ engineers** are expected to teach and govern AI usage on their teams — this shows up in the [career ladder](career-ladders.md).

## How this policy evolves

This is the policy that goes *stale fastest*. Owner: Director of AI Engineering with the Head of Engineering. Reviewed quarterly, not annually. Every change is recorded with the reason.
