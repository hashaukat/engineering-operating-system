# Release Engineering & Progressive Delivery

> If you can't deploy in minutes, you can't recover in minutes. Release velocity and incident velocity are the same muscle.

This doc defines how changes get from `main` to all production users — safely, observably, reversibly — in an org that ships continuously and uses AI-generated code at scale.

---

## The four claims

1. **Deployment is decoupled from release.** Code reaching production ≠ users seeing the behavior. Decoupling is what makes safe progressive delivery possible.
2. **Every release is reversible within minutes.** If a release can't be rolled back automatically, it isn't a release — it's a bet.
3. **Progressive delivery is the default.** Big-bang releases are an exception that requires justification, not the norm.
4. **Production telemetry decides, not the release engineer.** Health signals advance or roll back a release; humans intervene on exceptions.

---

## The deployment pipeline

A standard pipeline every team uses, exposed via the [internal developer platform](developer-experience.md):

```
PR → CI gates ([quality-engineering.md]) → merge to main
   → build + sign artifact (SBOM, provenance) ([security-and-supply-chain.md])
   → deploy to staging (auto)
   → smoke + integration eval (auto)
   → progressive rollout to prod (canary → 1% → 10% → 50% → 100%)
   → SLO + error-budget + eval-pass watch at every stage
   → auto-rollback on regression; auto-promote on green
```

- **Time-to-production from green PR** target: < 60 minutes for stream-aligned services.
- **No manual deploy steps** for standard services. Manual steps are the source of weekend incidents.

---

## Progressive delivery techniques

Pick the right tool for the change:

| Technique | When to use | Notes |
|---|---|---|
| **Canary** | Any non-trivial change | 1% → 10% → 50% → 100%, with auto-rollback on SLO regression |
| **Blue/green** | DB migrations with schema changes, infra-level cutovers | Two environments live; flip traffic; old environment kept warm for rapid rollback |
| **Feature flags** | Behavior changes that must be reversible per user/segment | Default. See flag discipline below |
| **Dark launch** | New code path; want production-shaped data before exposing to users | Run new path in parallel; compare outputs; do not return them |
| **Shadow traffic** | Performance / correctness check at prod scale | Mirror real traffic to new system; compare; discard responses |
| **Ring deployment** | Multi-tenant SaaS, regulated customers | Internal → low-risk customers → general |
| **Kill switches** | High-blast-radius features (AI features, payments, ML models) | One-flip global disable; tested quarterly |

---

## Feature flags — the discipline

Feature flags are a power tool. Misused, they become a permanent maintenance tax and a quality liability.

**Standing rules:**

- **Every flag has an owner and an expiration date.** No expiration = no flag.
- **Flag types are distinguished:**
  - **Release flags** — short-lived, removed after rollout.
  - **Experiment flags** — bounded duration tied to an experiment; removed after decision.
  - **Permission flags** — long-lived; treated as configuration, not flags.
  - **Operational flags / kill switches** — long-lived, tested quarterly.
- **Flags do not nest deeply.** A code path guarded by 4 nested flags is unreviewable.
- **Default state matches old behavior** until the flag is explicitly enabled.
- **Flag changes are audited.** Who flipped what, when, and why.
- **Stale-flag cleanup** is on every team's quarterly backlog.

---

## Rollback discipline

- **Rollback is a first-class plan**, written before launch, not invented at 3am.
- **Every spec** includes a "rollback plan" section ([spec-template.md](../templates/spec-template.md)).
- **Schema-incompatible changes** use expand/contract (add column → backfill → switch reads → remove old column), each step independently reversible.
- **Forward-fix vs rollback decision** is the IC's call during incidents, written into [incident-management.md](incident-management.md).
- **"We can't roll back" is a finding**, not an excuse. The next iteration adds the reversibility.

---

## SLOs and error budgets gate release velocity

- Each service has SLOs ([metrics-scorecard.md](metrics-scorecard.md), reliability lens).
- Each SLO has an **error budget** (the allowed unreliability).
- **Burn rate > 2× → release rate slows.** Team stops shipping risky features and invests in reliability.
- **Burn rate < 50% → release rate accelerates.** Team takes more risk, ships more.

This is the only mechanism that prevents the perennial "ship fast vs ship safe" debate from becoming a meeting. The numbers decide.

---

## Releasing AI features — additions

AI features have failure modes traditional services don't, so they get extra ceremony:

- **Eval suite must be green** at every progressive stage ([ai-feature-eval-template.md](../templates/ai-feature-eval-template.md)).
- **Drift monitors** in production: output distribution, latency, cost-per-call, refusal rate, sentiment.
- **Model version is part of the release.** Same code + new model = new release. Goes through the same pipeline.
- **Prompt changes are code changes.** Versioned, reviewed, deployable, rollback-able.
- **Kill switch is mandatory** for any customer-facing AI feature.
- **Quality regression triggers rollback** the same as latency regression.
- **Cost regression triggers a page.** Inference cost spikes are an incident class. See [engineering-finops.md](engineering-finops.md).

---

## Change management — the right amount

The DORA research is consistent across years: **lightweight, automated, peer-reviewed change approval correlates with both higher throughput and higher stability**. Heavyweight CABs correlate with neither.

Our model:

- **Default change:** PR review + automated gates + progressive delivery + observability. No CAB.
- **High-blast-radius change** (auth, payments, data deletion, regulated paths): two-human review + an ADR + a named rollback owner.
- **Emergency change:** documented break-glass path, automatic incident review after.
- **Maintenance windows:** for things that genuinely require them (cutovers, DB migrations) — communicated, scheduled, rehearsed.

---

## Release metrics

On the [scorecard](metrics-scorecard.md):

| Metric | Target |
|---|---|
| **Deployment frequency** | Multiple per day per service (elite per DORA) |
| **Change lead time** (commit → production) | < 1 day |
| **Change failure rate** | < 15% |
| **Mean time to restore** | < 1 hour |
| **% of services with auto-rollback configured** | > 90% |
| **% of releases via paved-road pipeline** | > 90% |
| **% of feature flags with expiration date** | 100% |
| **Stale flag count per team** | trending down |

---

## Anti-patterns to name and kill

- **Friday deploy freezes that hide the real problem** — the real problem is that deploys aren't safe enough to do anytime. Fix the safety, not the schedule.
- **"Big bang" releases.** Quarter-long batched changes shipped at once. Maximum risk, minimum learning.
- **Manual approval queues.** Slow without adding safety. Replace with automation + after-the-fact review for high-risk changes only.
- **Feature flags that became architecture.** A six-month-old flag is technical debt, not a release mechanism.
- **Rollback as theory.** Untested rollback paths fail when you need them. Rehearse quarterly.
- **AI feature ships without a kill switch.** When (not if) the model misbehaves, you have no off button.
- **Telemetry as an afterthought.** Releasing without the dashboards needed to detect regression = flying blind.

---

## How this connects

| When you... | Use with |
|---|---|
| Plan a launch | [spec-template.md](../templates/spec-template.md) (with rollback section), [decision-making.md](decision-making.md) |
| Build the pipeline | [developer-experience.md](developer-experience.md), [security-and-supply-chain.md](security-and-supply-chain.md), [quality-engineering.md](quality-engineering.md) |
| Ship an AI feature | [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md), [ai-assisted-development-policy.md](ai-assisted-development-policy.md), [ai-agent-governance.md](ai-agent-governance.md) |
| Run an incident | [incident-management.md](incident-management.md), [postmortem-template.md](../templates/postmortem-template.md) |

---

## Further reading

- **Humble & Farley** — *Continuous Delivery* — the canonical reference; still correct.
- **Forsgren, Humble, Kim** — *Accelerate* + [DORA Research](https://dora.dev/research/) — the four key metrics and what predicts them.
- **Google SRE** — [Release Engineering](https://sre.google/sre-book/release-engineering/), [Canarying Releases](https://sre.google/workbook/canarying-releases/).
- **Pete Hodgson** — [Feature Toggles](https://martinfowler.com/articles/feature-toggles.html) (Martin Fowler's site) — the definitive taxonomy.
- **Charity Majors** — [Test in production](https://charity.wtf/2021/06/16/test-in-production-you-must/) — the philosophical case.
- **CNCF App Delivery TAG** — [Operator Best Practices](https://github.com/cncf/tag-app-delivery) — progressive delivery patterns at scale.
