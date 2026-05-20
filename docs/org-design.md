# Org Design

> Org charts are software. They route information, define interfaces, and create latency. Design them with the same rigor.

## 1. Design constraints

A good engineering org optimizes for:

- **Clear ownership** — every system has exactly one team accountable for it.
- **Low coordination cost** — most work fits inside one team's boundaries.
- **Humane spans** — managers can actually coach the people who report to them.
- **Career paths** — both IC and management tracks have room to grow ([career ladders](career-ladders.md)).
- **Reversibility** — re-orgs are expensive; the structure should survive 18 months of growth without surgery.

## 2. Spans and layers

| Role | Healthy span | Notes |
|---|---|---|
| Engineering Manager (EM) | 5–8 ICs | Below 5 = under-loaded; above 8 = coaching collapses |
| Senior EM / Group EM | 3–5 EMs | Spans of EMs, not ICs |
| Director | 3–5 Group EMs / Sr EMs | Roughly 40–80 engineers |
| VP / Head of Eng | 3–6 Directors | 150–400 engineers before adding another layer |

**Layer rule:** no more than 4 layers between any IC and the head of engineering until ~300 engineers.

## 3. The 40 → 120 shape

For the [mock scenario](../examples/mock-q3-engineering-plan.md), the target shape after 18 months is:

```
Head of Engineering
├── Director, Product Engineering  (60)
│   ├── Group EM, Growth           (15: 2 stream-aligned teams)
│   ├── Group EM, Core Product     (25: 3 stream-aligned teams)
│   └── Group EM, Enterprise       (20: 2 stream-aligned + 1 enabling)
├── Director, Platform & Infra    (35)
│   ├── EM, Developer Platform     (8)
│   ├── EM, Data Platform          (8)
│   ├── EM, Infra & SRE            (10)
│   └── EM, Security Engineering   (7)
├── Director, AI & ML Engineering (15)
│   ├── EM, AI Platform            (7)
│   └── EM, Applied AI             (7)
└── Chief of Staff / Eng Ops       (1, + program managers as embedded contractors)
```

This shape is deliberate:
- **50% product, 30% platform, 12% AI, 8% leadership/ops** is the target allocation.
- The AI org is a *first-class* function from day one — not a tiger team.
- Security engineering reports into platform, not into a separate compliance silo.

## 4. Reporting line principles

1. **Single-threaded ownership.** No engineer reports to two managers. No team is "matrixed" by default.
2. **Functional reporting, dotted-line product alignment.** EMs own their engineers' careers; PMs own the roadmap. Both sign quarterly plans.
3. **Staff+ engineers report up the org they support.** A staff engineer embedded in platform reports to the platform director, not to a separate "staff engineering" silo.
4. **Managers of managers must have managed ICs.** No skip-grade promotion into Group EM without 12+ months of direct IC management.

## 5. Re-org policy

Re-orgs cost ~1 quarter of productivity per affected team. Therefore:

- Re-orgs happen **at most once per year**, on a planned cadence aligned with annual planning.
- Mid-year re-orgs require explicit VP+ approval and a written cost/benefit memo.
- We absorb growth through *team formation* (splitting and chartering new teams) far more often than through re-org.

## 6. Eng-ops function

By ~60 engineers, an engineering operations function pays for itself. Its job:

- Run the [planning rhythm](planning-rhythm.md).
- Maintain the [metrics scorecard](metrics-scorecard.md).
- Coordinate cross-team programs (architecture migrations, incident reviews).
- Own the engineer onboarding experience.

This is the *only* engineering function I would create centrally before 100 engineers.
