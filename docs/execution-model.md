# Execution Model

> How a piece of work travels from "someone has an idea" to "it is running in production and creating value." A clear execution model is the difference between an organization that ships and one that holds meetings about shipping.

In an AI-first org, this model is **spec-driven** end-to-end. See [spec-driven development](spec-driven-development.md) for the why; this doc is the operational flow.

## The work pipeline

```
   Intent        →   Discovery   →   Spec        →   Build       →   Ship        →   Operate     →   Learn
   (Strategy)        (Research)      (Spec-driven)   (AI-assisted)   (Flag+deploy)   (SLO/Run)        (Retro)
```

Every stage has an owner, a definition of done, and a written artifact. **The spec is the spine** — it is the artifact that survives even when the code is regenerated.

| Stage | Owner | Artifact |
|---|---|---|
| Intent | Director + PM Lead | Strategic bet recorded in [strategy](engineering-strategy.md) |
| Discovery | PM + Staff Engineer | Discovery doc (problem, evidence, options) |
| Spec | Tech Lead | [Spec](../templates/spec-template.md): intent + technical + acceptance |
| Build | Team | Implementation (AI-assisted) + tests passing acceptance spec |
| Ship | Team | Deployment + feature flag plan + telemetry |
| Operate | On-call rotation | SLOs, dashboards, runbooks |
| Learn | Team / Eng Ops | Retro, postmortem, scorecard update |

## Flow principles

### 1. Small batches
Default branch lifetime: <2 days. PRs <400 lines unless explicitly justified. Trunk-based development with feature flags.

### 2. Continuous delivery, not continuous deployment for everything
Every change reaches production-ready state on every merge. Whether it is *released* to customers is a product decision controlled by flags, not by deploy timing.

### 3. The deploy is not the event
Deploys are boring. The customer-facing release is the event. Decoupling these two lets us ship 50× a day without 50 release meetings.

### 4. Definition of done includes "operable"
A feature is not done until:
- It has a dashboard.
- It has an SLO if it is on a critical path.
- It has a runbook entry (even if the entry says "this never fails because X").
- The on-call team has been told it exists.

### 5. Feature flags are infrastructure
Flags require:
- An owner.
- An expiration date (default 90 days).
- A rollback plan.
- Automated cleanup of stale flags.

## How AI fits into the pipeline

AI assistance is allowed (and expected) at every stage. The *accountability gates* are unchanged. See [AI policy](ai-assisted-development-policy.md) for detail.

| Stage | AI usage | Gate |
|---|---|---|
| Discovery | Summarize prior art, draft research questions | Human review |
| Spec | Draft intent spec, generate alternatives, draft acceptance criteria | Tech lead is author of record |
| Build | Generate the majority of code from the spec; generate tests | Same code review bar; acceptance spec is the merge gate |
| Ship | Generate release notes, deploy checklists | Owner approves |
| Operate | First-line incident triage, runbook suggestion | Human on-call confirms |
| Learn | Draft postmortem timeline from logs | Author owns final write-up |

**The cardinal rule:** the spec is the AI agent's primary context, and the acceptance spec is the AI agent's grading rubric. No spec → AI gets vague instructions → low-quality output. The leverage in this model comes from spec quality, not from "more AI."

## How blockers are escalated

A blocker is anything that has stopped progress for >24 hours and the team cannot resolve unilaterally.

**Escalation path:**
1. Raise in team channel + tag EM.
2. If unresolved in 24h: EM escalates to Group EM / Director.
3. If unresolved in 48h: Director escalates to Head of Engineering and the blocker appears on the leadership Monday agenda.

This path exists so that engineers *know* there is a system. Heroics happen when no system exists.

## How we handle interruptions

Two patterns:
- **Interrupt rotation** — within each team, one engineer per sprint owns inbound interruptions (support escalations, ad-hoc requests, small bug fixes). Rotates fairly.
- **Goalie weeks** — for platform teams, one engineer per week is the "goalie" for internal customer requests.

Either pattern beats the failure mode where senior engineers absorb all interruptions silently and then burn out.
