# Planning Rhythm

> Planning is the heartbeat of the organization. If it is irregular, every team improvises. If it is over-engineered, every team rebels. The goal is a calm, predictable rhythm everyone can plan their lives around.

## The cadence

```
Annual     ──────────►   1× per year   (Nov)     "What are we becoming?"
Quarterly  ──────────►   4× per year             "What are we doing?"
Monthly    ──────────►   12× per year            "Are we on track?"
Sprint     ──────────►   ~26× per year (2-week)  "What are we shipping?"
Weekly     ──────────►   52× per year            "What is blocked?"
```

## Annual planning (November)

**Outputs:**
- Refreshed [engineering strategy](engineering-strategy.md) with H1/H2/H3 allocation.
- Headcount plan by team, mapped to the [team topology](team-topologies.md).
- 3–5 company-level engineering bets for the year.
- Budget envelope (people, infra, tools, AI usage).

**Owners:** Head of Engineering with CEO, CFO, CPO. Directors contribute their team plans.

**Anti-patterns I refuse:**
- Annual roadmaps with sprint-level detail. The world changes too fast.
- Headcount plans without a topology rationale.
- "Top-down" plans without IC sanity checks.

## Quarterly planning (the workhorse)

A 3-week cycle, run at the end of every quarter, using the [quarterly planning template](../templates/quarterly-planning-template.md).

| Week | Activity | Owner |
|---|---|---|
| Week -3 | Leadership drafts 3–5 quarterly objectives | Directors |
| Week -2 | Each team drafts their quarterly plan against objectives | EM + Staff/Tech Lead + PM |
| Week -1 | Cross-team review: dependencies, capacity, risks | Group EMs |
| Week 0  | Plans signed, published, communicated all-hands | Head of Eng |

**Each team's plan contains:**
1. The 1–3 quarterly outcomes they are accountable for.
2. The horizon (H1/H2/H3) and strategy bet each maps to.
3. Explicit *non-goals* — what we are choosing not to do.
4. Capacity model: planned engineer-weeks, with ≤70% allocated to planned work. The remaining 30% absorbs unplanned work, incidents, paying down tech debt, and learning.
5. Top 3 risks and the mitigation plan.

## Monthly business review

90 minutes, leadership team only. Format:

1. **Scorecard walk-through** ([metrics scorecard](metrics-scorecard.md)) — 20 min.
2. **One team deep-dive** — 30 min (rotating; team owns the agenda).
3. **Open risks and decisions** — 30 min.
4. **Strategy temperature check** — 10 min.

## Sprint cadence

2-week sprints, team-owned. No org-wide sprint ceremony. Teams choose their own rituals provided they:

- Have a written team working agreement.
- Run a retro every sprint and act on at least one improvement.
- Publish a sprint summary (what shipped, what slipped, why) to a public channel.

## Weekly leadership operating cadence

| Day | Meeting | Duration |
|---|---|---|
| Monday | Leadership team standup (blockers only) | 30 min |
| Tuesday | Architecture council ([review process](architecture-review-process.md)) | 60 min |
| Wednesday | 1:1s | varies |
| Thursday | Incident review (if any sev1/sev2 in past 2 weeks) | 60 min |
| Friday | Engineering all-hands (biweekly) | 45 min |

## What I refuse to do in planning

- **Re-plan every quarter from zero.** Most of the previous quarter's plan should carry over. Re-planning everything is a tell that nothing was real.
- **Stack-rank teams.** Stack-ranking teams optimizes for the wrong game.
- **Treat capacity as a number on a spreadsheet.** Capacity is a function of focus, on-call burden, hiring load, and morale. Track all four.
