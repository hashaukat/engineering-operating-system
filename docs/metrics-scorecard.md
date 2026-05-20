# Metrics & Scorecard

> Metrics are how the organization sees itself. The wrong metrics turn smart teams into actors. The right metrics turn the org into a learning system.

> **Note:** This doc is the *visual scorecard* — the one-pager leadership reviews. The full theory of measurement (DORA + SPACE + DX + AI productivity + TTM + customer value, and what we refuse to measure) lives in [productivity-measurement.md](productivity-measurement.md). Read that first if you want the *why*; read this for the *what*.

## Principles for metrics

1. **Measure outcomes, govern through metrics.** Outcomes are for accountability; metrics are for diagnosis.
2. **Every metric has a question.** If you cannot state the question a metric answers, retire it.
3. **No single team is judged on a single number.** Goodhart's law is real.
4. **Trends over snapshots.** A direction matters more than a point.
5. **Publish the scorecard.** Engineers should see what leadership sees.

## The five lenses

I run a balanced scorecard across five lenses. Each lens answers one question. (Lens 5 — Customer Value — is the scoreboard the rest of engineering rolls up to.)

### Lens 1 — Throughput (DORA + spec velocity)
*Are we shipping?*

| Metric | Definition | Target (mature team) |
|---|---|---|
| Deployment Frequency | Median deploys per service per day | ≥ 1/day |
| Lead Time for Changes | PR open → prod deploy, p50 | < 1 day |
| Change Failure Rate | % of deploys causing rollback or incident | < 15% |
| Mean Time to Restore | Time from incident start → resolved | < 1 hour |
| Specs shipped per quarter | Count of specs whose acceptance criteria passed in prod | Trend up |
| Spec → prod cycle time | Intent-spec accepted → acceptance-spec passing in prod | < 2 weeks median |

### Lens 2 — Trust (Reliability & Security)
*Can the business and our customers count on us?*

| Metric | Definition | Target |
|---|---|---|
| SLO attainment | % of critical user journeys meeting SLO over 28 days | ≥ 99% |
| Error budget burn rate | Multiple of allowed burn | < 2× for >24h triggers freeze |
| Sev1/Sev2 incidents | Count per quarter | Trend down |
| Time to patch critical CVE | Hours from disclosure → patched in prod | < 24h |
| Secret leak detections | Per quarter | 0 reaching production |

### Lens 3 — Leverage (Developer Experience + AI)
*Is each engineer getting more powerful?*

| Metric | Source | Target |
|---|---|---|
| DX Core 4 (Speed/Effectiveness/Quality/Impact) | Quarterly survey | ≥ 4/5 on each |
| Engineer-reported flow score | [Team health survey](../templates/team-health-survey.md) | ≥ 4/5 |
| Time from commit to CI signal | Build/test pipeline | < 10 min p75 |
| Time from new-hire start → first prod merge | Onboarding tracker | < 14 days |
| Platform NPS (internal customers) | Quarterly survey | ≥ +30 |
| AI-assisted PRs accepted vs reverted (team) | Code review tooling | Acceptance ≥ 90% |
| AI suggestion acceptance rate trend (team) | IDE telemetry | Trending up |
| Cost per merged PR (AI tooling spend) | Finance + PR data | Within budget |

### Lens 4 — Time-to-Market
*Are ideas reaching customers fast enough to matter?*

| Metric | Definition | Target |
|---|---|---|
| Idea → measurable impact (micro feature) | End-to-end TTM, ≤1 sprint scope | < 30 days |
| Idea → measurable impact (feature, 1–4 sprints) | End-to-end TTM | < 90 days |
| Idea → measurable impact (system, multi-quarter) | End-to-end TTM | < 180 days |
| Discovery cycle time | Problem raised → spec accepted | < 2 weeks |
| Rollout cycle time | First prod merge → GA to all customers | < 2 weeks |
| Time-to-adoption | GA → measurable adoption | < 30 days |

### Lens 5 — Customer Value (the scoreboard)
*Are we creating value the company and our customers care about?*

| Metric | Definition | Target |
|---|---|---|
| **CSAT** (per major feature) | In-product post-interaction survey | ≥ 4.3/5 |
| **NPS** (overall product) | Quarterly survey | Improving YoY |
| **Time-to-Value** (TTV) | New customer sign-up → first defined success event | < product target |
| **Customer Effort Score** (CES) | "How easy was it to …" | ≥ 5/7 |
| User-perceived latency (p75 critical journeys) | RUM / front-end telemetry | < 1s |
| Customer-visible error rate | API gateway + error tracker | < 0.1% |
| Customer-reported incidents per quarter | Support + status page | Trend down |
| AI-feature trust score (when applicable) | In-product "was this helpful?" | ≥ 4/5 |
| AI-feature hallucination/wrongness rate | Offline eval | < 2% production |

## The leadership scorecard (one page)

The Head of Engineering reviews this monthly with leadership:

```
┌──────────────────────────────────────────────────────────────────────┐
│ ENGINEERING SCORECARD — <Month> <Year>                               │
├──────────────────────┬──────────┬──────────┬──────────┬─────────────┤
│ Lens                 │ Now      │ 90d trend│ Target   │ Status      │
├──────────────────────┼──────────┼──────────┼──────────┼─────────────┤
│ Throughput           │ Elite    │   →      │ Elite    │  Green      │
│ Trust  (SLO+Sec)     │ 99.92%   │   ↑      │ 99.95%   │  Yellow     │
│ Leverage (DX+AI)     │ 3.8/5    │   ↑      │ 4.2/5    │  Yellow     │
│ Time-to-Market       │ 41d med  │   ↓      │ <30d     │  Yellow     │
│ Customer Value       │ NPS 38   │   ↑      │ 45       │  Yellow     │
│                      │ CSAT 4.4 │   →      │ 4.3      │  Green      │
│                      │ TTV 2.1d │   ↓      │ <2d      │  Yellow     │
├──────────────────────┴──────────┴──────────┴──────────┴─────────────┤
│ Top 3 risks: ...                                                     │
│ Top 3 wins:  ...                                                     │
│ Decisions needed from CEO/board: ...                                 │
└──────────────────────────────────────────────────────────────────────┘
```

A worked example for Q3 of the mock scenario lives in [sample OKR scorecard](../examples/sample-okr-scorecard.md).

## The three rolled-up indices

For the board and CEO, the five lenses roll up to **three composite indices** (defined in [productivity-measurement.md](productivity-measurement.md)):

- **Throughput Index** — DORA + spec-shipping rate.
- **TTM Index** — median idea-to-impact time, by feature size.
- **Customer Value Index** — composite of CSAT, NPS, TTV (weighted by quarterly product priority).

**Red on any index for two consecutive months** triggers a written 30-day response from the responsible director. **Green across all three for two consecutive quarters** is the bar for declaring the operating system "working."

## What I refuse to measure (or measure carefully)

- **Lines of code, commits, PR count per engineer.** These reward noise.
- **Velocity points across teams.** Story points are a *within-team* planning tool. Comparing them across teams is a category error.
- **Individual AI usage rates.** Adoption is a team-level metric, not an individual scorecard item. Pressuring individuals on AI usage corrupts judgment.
- **Activity dashboards that watch engineers in real time.** They damage trust and produce worse work.

## How metrics flow back into action

- A **yellow** metric is named in the next monthly review with an owner and a 30-day plan.
- A **red** metric becomes a quarterly objective for the responsible team.
- A **green** metric trending down for two months becomes yellow.
