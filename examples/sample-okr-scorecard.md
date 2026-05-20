# Sample OKR Scorecard — Q3, Month 9 of the Mock Plan

> A worked example of the engineering scorecard mid-way through the [40→120 transformation](mock-q3-engineering-plan.md). This is what the Head of Engineering would walk through with the CEO and leadership team in the monthly business review.

| Field | Value |
|---|---|
| Quarter | Q3 |
| Month | 9 of 18 |
| Headcount | 78 engineers |
| Reporting period | Last 28 days |

---

## The one-page scorecard

```
┌─────────────────────────────────────────────────────────────────────────┐
│ ENGINEERING SCORECARD — Sep YYYY                          78 engineers  │
├──────────────────────┬──────────┬───────────┬──────────┬───────────────┤
│ Lens                 │ Now      │ 90d trend │ Target   │ Status        │
├──────────────────────┼──────────┼───────────┼──────────┼───────────────┤
│ Throughput           │ High     │   ↑       │ Elite    │ Yellow        │
│  - Deploys/svc/day   │ 1.4      │   ↑       │ ≥1       │ Green         │
│  - Lead time (med)   │ 1.8 d    │   ↓       │ <1 d     │ Yellow        │
│  - CFR               │ 14%      │   ↓       │ <15%     │ Green         │
│  - MTTR              │ 1h 20m   │   →       │ <1h      │ Yellow        │
│  - Specs shipped Q3  │ 47       │   ↑       │ 60       │ Yellow        │
├──────────────────────┼──────────┼───────────┼──────────┼───────────────┤
│ Trust                │ 99.83%   │   ↑       │ 99.95%   │ Yellow        │
│  - SLO attainment    │ 99.83%   │   ↑       │ 99.95%   │ Yellow        │
│  - Sev1/Sev2 (qtr)   │ 3 / 7    │   ↓       │ Trend ↓  │ Green         │
│  - Time to CVE patch │ 18h      │   ↓       │ <24h     │ Green         │
├──────────────────────┼──────────┼───────────┼──────────┼───────────────┤
│ Leverage (DX + AI)   │ 3.7/5    │   ↑       │ 4.2/5    │ Yellow        │
│  - DX Core 4 avg     │ 3.7      │   ↑       │ 4.2      │ Yellow        │
│  - Onboard→1st merge │ 13 d     │   ↓       │ <14 d    │ Green         │
│  - Platform NPS      │ +24      │   ↑       │ +30      │ Yellow        │
│  - AI accept rate    │ 42%      │   ↑       │ ≥50%     │ Yellow        │
│  - CI time p75       │ 12 min   │   ↓       │ <10 min  │ Yellow        │
├──────────────────────┼──────────┼───────────┼──────────┼───────────────┤
│ Time-to-Market       │ 78 days  │   ↓       │ <90 d    │ Green         │
│  - Discovery cycle   │ 12 d     │   ↓       │ <14 d    │ Green         │
│  - Build cycle       │ 22 d     │   ↓       │ <14 d    │ Yellow        │
│  - Rollout cycle     │ 9 d      │   ↓       │ <14 d    │ Green         │
├──────────────────────┼──────────┼───────────┼──────────┼───────────────┤
│ Customer Value       │ Mixed    │   ↑       │ Strong   │ Yellow        │
│  - NPS               │ 36       │   ↑ +3    │ 40+      │ Yellow        │
│  - CSAT (overall)    │ 4.2      │   ↑       │ 4.3+     │ Yellow        │
│  - TTV (new cust)    │ 2.1 d    │   ↓       │ <1.5 d   │ Yellow        │
│  - Customer Effort   │ 5.2/7    │   →       │ ≥5       │ Green         │
│  - Cust-rep incidents│ 6/qtr    │   ↓       │ <3/qtr   │ Yellow        │
│  - AI feat trust     │ 4.1/5    │   ↑       │ ≥4.3     │ Yellow        │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## The three rolled-up indices

| Index | Value | Trend | Target | Status |
|---|---|---|---|---|
| Throughput Index | 78/100 | ↑ | 85+ | Yellow |
| TTM Index | 72/100 | ↑ | 80+ | Yellow |
| Customer Value Index | 70/100 | ↑ | 80+ | Yellow |

**Two consecutive months of yellow on Customer Value Index** → triggers a written 30-day response from the Director of Product Engineering. (See "Decisions needed" below.)

---

## Top 3 wins this month

1. **Onboarding → first merge dropped to 13 days** (from 18 last quarter, 25 at baseline). The IDP service-template paved road is working. Specifically: new hires in the last cohort all shipped within 14 days; the longest was a Staff hire who chose a deeper first PR.
2. **Spec-driven dev hit 80% of new features.** 47 specs shipped in Q3 to date, on track for 60. The two teams that piloted spec-driven flow in Q1 are now the fastest-shipping teams in the org and are the de facto coaches for new adopters.
3. **AI feature trust score climbed from 3.8 → 4.1** for our document summarization feature, after the AI Platform team tightened the eval suite and caught a regression in our retrieval pipeline. The eval harness paid for itself this month.

## Top 3 risks

1. **Reliability gap to target (99.83% vs 99.95%) is concentrated in 2 services.** Both predate the IDP and have not been migrated. Plan: dedicated reliability sprint in Q4 led by SRE + service owners.
2. **AI suggestion acceptance rate stuck at 42% in 3 teams** despite climbing org-wide. Initial investigation suggests inconsistent IDE setup, not skill. The AI Adoption enabling team rotates to those 3 teams next month.
3. **Customer-reported incidents (6/qtr) are not falling fast enough.** Top categories: latency on enterprise reports (3), checkout edge cases (2), notifications (1). Latency is in flight; the other two need explicit ownership decisions this month.

## Decisions needed from CEO / leadership

1. **Approve a 4-week reliability sprint in Q4** that pauses non-critical feature work on the two below-SLO services. Estimated TTM cost: 1 quarter's feature throughput on those services. Reliability payoff: closes the gap to 99.95%.
2. **Approve hiring 2 additional SRE engineers** ahead of the original Q4 plan to support the migration of legacy services to the IDP.
3. **Confirm Customer Value Index remains a P0 quarterly objective** — answer determines whether the Director of Product Engineering's 30-day response plan targets +5 NPS this quarter or holds.

---

## What this scorecard is *not* showing

Per [productivity measurement](../docs/productivity-measurement.md), the following are deliberately absent:

- Individual engineer activity metrics.
- Story-point velocity comparisons across teams.
- Individual AI usage rates.
- Lines of code, commits, PR counts per person.

If a board member asks for them, the answer is to walk them through this doc instead.

---

## Sample team-level rollup (illustrative — Enterprise team)

| Metric | Team value | Org target |
|---|---|---|
| Specs shipped this quarter | 8 | varies |
| Spec → prod cycle time (med) | 16 days | <14 d |
| DORA — deploys/day | 2.1 | ≥1 |
| DORA — CFR | 11% | <15% |
| SLO attainment (Enterprise Admin svc) | 99.91% | 99.95% |
| DX Core 4 avg | 3.9 | 4.2 |
| On-call pages/wk (avg per engineer) | 1.3 | <2 |
| Customer-reported incidents (this team's surface) | 2 | <1 |
| Top customer-value metric movement | Enterprise NPS 41 (+4 QoQ) | — |

The team's narrative: shipping consistently, slightly slow on cycle time due to one large multi-quarter migration, on-call healthy, customers happy. No intervention needed; continue.
