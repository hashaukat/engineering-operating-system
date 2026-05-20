# Productivity & Value Measurement

> Productivity is not lines of code. Productivity is not commits. Productivity is the **rate at which the organization converts intent into customer value, safely and sustainably.** Everything we measure rolls up to that definition.

This doc unifies the three measurement systems an AI-first engineering org needs:

1. **Engineering productivity** — are engineers (with their AI collaborators) producing more, faster, with less friction?
2. **Time-to-market** — how quickly do ideas become value in customers' hands?
3. **Customer value & satisfaction** — is the value actually landing?

The [scorecard](metrics-scorecard.md) is the visual; this doc is the *theory of measurement*.

---

## Part 1 — Engineering productivity

We use a hybrid of **DORA**, **SPACE**, and **DX Core 4**, instrumented for an AI-augmented team.

### DORA (the throughput floor)
| Metric | What it tells us |
|---|---|
| Deployment frequency | Are we shipping in small batches? |
| Lead time for changes | How long does intent take to become production? |
| Change failure rate | Are we shipping safely? |
| Mean time to restore | When we break it, how fast do we fix it? |

DORA is a *floor*. An elite-DORA team can still be unproductive (shipping the wrong thing fast). It is necessary, not sufficient.

### SPACE (the human dimension)
SPACE reminds us that productivity is multi-dimensional. We sample, not score:

- **S**atisfaction & well-being — quarterly [team health survey](../templates/team-health-survey.md).
- **P**erformance — outcomes (see Part 3), not output.
- **A**ctivity — measured at the team level only.
- **C**ommunication & collaboration — review latency, cross-team PR throughput.
- **E**fficiency & flow — uninterrupted time, meeting load, context-switch frequency.

### The DX Core 4 (developer experience)
Four engineer-perceived metrics, surveyed quarterly, used as leading indicators:

1. **Speed** — "I can ship a small change to production in less than a day."
2. **Effectiveness** — "I am working on the right things."
3. **Quality** — "I trust the code I am asked to change."
4. **Impact** — "My work matters to customers."

These predict attrition and outcomes far better than any system metric.

### AI productivity instrumentation (new in an AI-first org)

The questions an AI-first org must be able to answer:

| Question | Metric | Where measured |
|---|---|---|
| Are engineers actually using AI? | Active AI users / week (team-level, never individual) | IDE telemetry |
| Is AI-generated code making it to prod? | % of merged PRs with AI-generated content | PR metadata |
| Is AI-generated code as good? | Defect rate of AI-touched vs human-only PRs | Defect tracker |
| Is AI saving time? | Self-reported time saved per task (quarterly survey) | DX survey |
| Is AI suggestion quality improving? | Suggestion acceptance rate trend | IDE telemetry |
| Are agents doing useful work? | % of agent PRs merged without revert | PR metadata |
| What does AI cost per merged PR? | $ AI tooling / merged PRs | Finance + PR data |

**Critical guardrails:**
- These metrics are *team-level*, not individual.
- "AI usage rate" is **never** a performance metric for an individual ([AI policy](ai-assisted-development-policy.md)). Doing so corrupts the metric instantly.
- We measure *outcomes* (defects, lead time, satisfaction), and ask "is AI helping?" — not "is this engineer using enough AI?"

### Spec-driven productivity metrics
For [spec-driven](spec-driven-development.md) teams, two additional metrics matter:

| Metric | What it tells us | Target |
|---|---|---|
| Specs-shipped per quarter (team) | Throughput of *intent fulfilled*, not just code merged | Trend up |
| Spec → prod cycle time | From intent spec accepted → acceptance spec passing in prod | < 2 weeks median |
| Spec rework rate | % of specs requiring material change mid-build | < 25% |

Specs-shipped is the single best AI-era replacement for "story points completed."

---

## Part 2 — Time-to-market

Engineering productivity that doesn't reach customers faster is theatrical. We instrument the **full TTM funnel**, end to end:

```
Idea → Validated Problem → Spec → Build → Ship → Adoption → Outcome
```

| Stage | Metric | Target (mature team) |
|---|---|---|
| Idea → Validated Problem | Discovery cycle time | < 2 weeks |
| Validated Problem → Spec accepted | Spec authoring time | < 1 week |
| Spec → First merge in prod (behind flag) | Build cycle time | < 2 weeks for feature-sized work |
| First merge → GA to all customers | Rollout cycle time | < 2 weeks |
| GA → Measurable adoption | Time-to-adoption | < 30 days for in-product features |
| GA → Measurable outcome | Time-to-impact | < 90 days |

**End-to-end TTM (median, by feature size):**
| Feature size | Target TTM (idea → measurable impact) |
|---|---|
| Micro (≤ 1 sprint) | < 30 days |
| Feature (1–4 sprints) | < 90 days |
| System (multi-quarter) | < 180 days |

Stretching TTM beyond these without explicit reason is a red flag, regardless of how busy teams look.

---

## Part 3 — Customer value & satisfaction

Engineering owns the contribution, not the outcome — but we *measure* the outcome.

### The four customer-value metrics every product engineering org should track

| Metric | Definition | Owned by | Engineering's contribution |
|---|---|---|---|
| **CSAT** (per feature) | "How satisfied are you with X?" sampled in-product | Product | Reliability, latency, UX quality |
| **NPS** (overall product) | Net Promoter Score, sampled quarterly | Product | Long-term trust, performance, fewer incidents |
| **Time-to-Value** (TTV) | Sign-up → customer hits their first defined success event | Product + Eng | Onboarding friction, performance |
| **Customer Effort Score** (CES) | "How easy was it to accomplish X?" | Product + Eng | Latency, UI responsiveness, error-handling clarity |

### Engineering-specific customer-impact metrics

Things engineering directly owns that customers feel:

| Metric | Target | Where it lives |
|---|---|---|
| User-perceived latency (p75 critical journeys) | < 1s | RUM / front-end telemetry |
| Customer-visible error rate | < 0.1% | API gateway + error tracker |
| Customer-reported reliability incidents per quarter | trend down | Support + status page |
| Support tickets tagged "broken" / MAU | trend down | Support tooling |
| Time from customer report → fix in prod (median) | < 5 business days | Issue tracker |

### For customer-facing AI features

A separate lens, because AI failures are visible to customers in new ways:

| Metric | Definition | Target |
|---|---|---|
| AI feature acceptance rate | % of AI suggestions/outputs the user keeps | Trend up |
| AI feature trust score | In-product "was this helpful?" sampled | ≥ 4/5 |
| Hallucination / wrongness rate | % of outputs failing offline eval | < 2% for production features |
| Cost per successful interaction | $ AI cost / successful task completion | Within product margin target |
| Safety incidents | Outputs flagged for policy/safety | 0 reaching customer in critical paths |

These live in the [AI policy](ai-assisted-development-policy.md) eval framework.

---

## How leadership uses these measurements

The Head of Engineering reviews **three rolled-up indicators monthly**:

1. **Throughput Index** — composite of DORA + spec-shipping rate, normalized.
2. **TTM Index** — median idea-to-impact time, by feature size.
3. **Customer Value Index** — composite of CSAT, NPS, TTV (weighted by what the product strategy emphasizes that quarter).

A **red on any index for two consecutive months** triggers a written response from the responsible director with a 30-day plan. A **green across all three for two consecutive quarters** is the bar for declaring the operating system "working."

---

## What I refuse to measure

- **Individual AI usage rates** as a performance scorecard item.
- **Lines of code, commits, or PR counts** per engineer.
- **Story-point velocity** across teams.
- **"Hours worked"** in any form.
- **Activity dashboards** that watch engineers in real time.

These metrics corrupt judgment, punish the wrong behaviors, and damage trust. The first time a Director asks for one of them, the answer is no, with this document attached.

---

## Why this matters for AI-first orgs specifically

In a pre-AI org, throughput, TTM, and customer value were largely independent levers. In an AI-augmented org, **AI compresses throughput and TTM dramatically, which exposes the customer-value question with new force.**

Translation: it is now trivially easy to ship the wrong thing very fast. The job of the operating system is to make sure the speed lands on the right targets — and that is what this measurement framework is built to do.
