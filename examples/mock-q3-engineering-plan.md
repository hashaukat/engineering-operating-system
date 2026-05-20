# Mock Engineering Plan: 40 → 120 in 18 Months, AI-First

> **The scenario.** You are joining a Series C B2B SaaS company as Head of Engineering. Today: 40 engineers, 8 teams, $50M ARR, 99.5% reliability, deploys 2x/week, AI usage informal and inconsistent.
>
> **The mandate.** In 18 months: 120 engineers, reliability at 99.95%, deploy multiple times per day, AI in the default path for every team, time-to-market cut in half, customer NPS up 10 points — all without breaking the culture.
>
> This document is the plan. It uses the full [Engineering Operating System](../README.md) as its operating model.

---

## 0. Read of the situation (week 1–4)

Before any plan, the diagnostic. What I would look at first:

| Domain | What I'd measure | Likely findings at this stage |
|---|---|---|
| **Throughput** | DORA on every service | Lead time days–weeks; deploys batched; CFR > 20% on some services |
| **Trust** | SLO coverage, incident postmortems, secret-leak history | SLOs informal; incidents not learned from |
| **Leverage** | DX Core 4, CI times, onboarding-to-first-merge | DX 3.0/5, CI 25 min p75, onboarding 4 weeks |
| **TTM** | Sample 10 recent features end-to-end | Idea-to-impact 4–6 months median |
| **Customer value** | NPS, CSAT, support escalations, churn | NPS ~30, top complaint = reliability |
| **AI** | Tool sprawl, no policy, no evals | "Some teams use Copilot, no one knows how well it's working" |
| **Org** | Spans, layers, ownership gaps | A few overloaded EMs; 3 systems with no clear owner |

Output: a **30-day diagnostic memo** to the CEO with the top 5 systemic gaps and the proposed shape of the response.

---

## 1. Strategy on a page

| Field | Value |
|---|---|
| Horizon | 18 months |
| Owner | Head of Engineering |

**Where we are going:** *In 18 months we are a 120-person, AI-first engineering organization that ships customer value in days instead of months, with 99.95% reliability and a +10 NPS.*

**The 3 bets:**
1. **Platform first.** A dedicated platform investment (paved roads, golden paths, internal developer platform) is the highest-leverage thing we can do before tripling headcount.
2. **Spec-driven, AI-augmented delivery.** Every team adopts [spec-driven development](../docs/spec-driven-development.md). AI is in the default path. Time-to-market falls because intent is captured cleanly and translated into code with high leverage.
3. **Reliability as a product.** Move from 99.5% → 99.95% by treating SLOs as planning inputs, error budgets as governance, and incidents as the most important learning artifact we produce.

**Explicitly not doing:**
- Not rewriting the monolith. Strangling, not rewriting.
- Not building an internal ML platform. Renting until usage justifies it.
- Not adopting a second cloud.
- Not building our own AI evals framework — extending an existing one.
- Not "moving fast and breaking things." Moving fast and *measuring everything*.

**Biggest risk:** scaling too fast and damaging culture, on-call sustainability, or quality. Hiring is throttled by the platform's ability to absorb new engineers, not by recruiting capacity.

---

## 2. Target end-state org

Built per [org design](../docs/org-design.md) and [team topologies](../docs/team-topologies.md).

```
Head of Engineering (1)
├── Director, Product Engineering         (60)
│   ├── Group EM, Growth                  (15: 2 stream-aligned)
│   ├── Group EM, Core Product            (25: 3 stream-aligned)
│   └── Group EM, Enterprise              (20: 2 stream-aligned + 1 enabling)
├── Director, Platform & Infra            (33)
│   ├── EM, Developer Platform (IDP)      (8)
│   ├── EM, Data Platform                 (8)
│   ├── EM, Infra & SRE                   (10)
│   └── EM, Security Engineering          (7)
├── Director, AI & ML Engineering         (15)
│   ├── EM, AI Platform (gateway, evals, prompt registry, vector) (7)
│   └── EM, Applied AI (model-backed features) (7)
├── Chief of Staff / Eng Ops              (3: ops, programs, comms)
└── Hiring buffer                          (8)
                                          ───
                                          120
```

**Why this shape:**
- **50% product, 30% platform, 12% AI, 8% leadership/ops.** Under-investing in platform is the most common scaling mistake; we will not make it.
- **AI as a first-class org** from day one — not a tiger team that gets reabsorbed.
- **Security inside platform** — not a separate compliance silo.
- **Eng Ops** small but real, because at >60 engineers it pays for itself.

---

## 3. The 18-month timeline

Each phase has a single dominant theme. The plan is sequenced so that capability lands *before* the headcount that needs it.

### Phase 1 — Foundation (months 1–3)
*"Stop the bleeding, install the operating system."*

| Workstream | Outcome | Owner |
|---|---|---|
| Operating system installed | Quarterly planning, metrics scorecard, ARB, incident process live | Head of Eng + Eng Ops |
| Diagnostic + scorecard baseline | All 5 lenses measured and published internally | Eng Ops |
| Spec-driven development pilot | 2 teams adopt spec-driven flow as a pilot | Tech leads |
| AI policy published | [AI policy](../docs/ai-assisted-development-policy.md) ratified; approved tools list; AI gateway MVP | Director, AI Eng |
| Platform team chartered | [Platform charter](sample-platform-team-charter.md) signed; first 3 paved roads scoped | Director, Platform |
| Incident process reset | New severity model, IC roles, postmortem template adopted | SRE Lead |
| Hiring: 8 hires | 2 platform, 2 AI Eng, 4 product engineers (replacing attrition) | All |

**End of Phase 1:** scorecard live, processes in place, ~45 engineers. The org *sees itself* for the first time.

### Phase 2 — Leverage (months 4–9)
*"Make the right thing the easy thing. AI in the default path."*

| Workstream | Outcome | Owner |
|---|---|---|
| Internal Developer Platform v1 | Paved road: service template + CI/CD + observability + secrets, 5 services migrated | Dev Platform EM |
| Spec-driven dev org-wide | All teams using [spec template](../templates/spec-template.md) for feature work | All EMs |
| AI Adoption enabling team | Time-boxed enabling team rotates through each product team | Director, AI Eng |
| Eval harness | Shared eval framework; first 3 AI features have eval suites | AI Platform EM |
| Reliability sprint | Top 10 SLOs defined; error budget policy enforced; on-call burden reset | SRE Lead |
| Postmortem culture | Monthly incident reviews running; action item completion rate published | Eng Ops |
| Hiring: 35 hires | Scaled hiring with paved-road onboarding; time-to-first-merge < 14 days | All |

**End of Phase 2:** ~80 engineers. DORA solidly "high" on most services. Spec-driven flow is the default. The first AI feature ships with a real eval suite.

### Phase 3 — Compound (months 10–15)
*"Scale the system, not the headcount."*

| Workstream | Outcome | Owner |
|---|---|---|
| Platform self-service | New team can be productive in < 1 week using IDP | Dev Platform EM |
| AI in every team | Every team has named AI-leverage bets in their quarterly plan | EMs |
| Customer value index live | CSAT/NPS/TTV/CES on scorecard; engineering owns its contribution | Head of Eng + CPO |
| Architecture migrations | Top 2 strangle-the-monolith carveouts complete | Staff engineers + ARB |
| Reliability hit 99.9% | Sustained for one full quarter | SRE + product teams |
| Hiring: 30 hires | Backfill + growth; Staff/Sr Staff hires brought in for leverage | All |

**End of Phase 3:** ~110 engineers. Customer-value lens is producing actionable signal. Reliability at 99.9% and on the path to 99.95%.

### Phase 4 — Operate (months 16–18)
*"Prove the system. Hand off. Set the next horizon."*

| Workstream | Outcome | Owner |
|---|---|---|
| Reliability hit 99.95% | Sustained quarter | SRE |
| TTM index target met | Median feature TTM < 90 days | All |
| NPS +10 | Sustained quarter | Product + Eng |
| Annual planning | The 18-month plan wraps and the next horizon is set | Head of Eng + CEO |
| Operating system handoff-ready | Directors own their slice of the EOS independently | Head of Eng |
| Hiring: ~10 hires | Final fills + strategic Principal hire for next horizon | All |

**End of Phase 4:** 120 engineers, mandate met. The operating system is now self-sustaining.

---

## 4. The measurement plan

Tracked monthly per the [scorecard](../docs/metrics-scorecard.md). Targets at each milestone:

| Index / metric | Baseline | M6 | M12 | M18 (target) |
|---|---|---|---|---|
| **Throughput** | | | | |
| Deploys/service/day | 0.3 | 1 | 3 | 5+ |
| Lead time (median) | 9 days | 3 days | 1 day | < 1 day |
| Specs shipped/quarter | n/a | 30 | 80 | 150 |
| **Trust** | | | | |
| SLO attainment | 99.5% | 99.7% | 99.9% | 99.95% |
| CFR | 22% | 18% | 12% | < 10% |
| MTTR (Sev1/2) | 4h | 2h | 1h | < 1h |
| **Leverage** | | | | |
| DX Core 4 (avg) | 3.0 | 3.5 | 4.0 | 4.3 |
| Onboarding → first merge | 25 days | 18 days | 12 days | < 10 days |
| AI suggestion acceptance (team avg) | not measured | 35% | 45% | 50% |
| **TTM** | | | | |
| Feature TTM (median) | 130 days | 90 days | 70 days | < 60 days |
| **Customer value** | | | | |
| NPS | 30 | 33 | 38 | 40+ |
| CSAT | 4.0 | 4.1 | 4.2 | 4.3+ |
| TTV (new customer → first success) | 3.0 days | 2.5 days | 2.0 days | < 1.5 days |
| Customer-reported reliability incidents | 12/qtr | 8/qtr | 5/qtr | < 3/qtr |

---

## 5. AI rollout, specifically

Because this is where the highest leverage *and* the highest risk live.

### Months 1–3: Foundation
- AI policy ratified; approved tool list (Copilot for IDE; one approved chat tool; one approved agent runner).
- AI gateway MVP: one place where API calls go; cost + rate limit + audit log + policy filter.
- Pilot 2 teams on spec-driven dev + AI-assisted build. Measure cycle time vs. control.

### Months 4–9: Leverage
- AI Adoption enabling team rotates through every product team (4-week engagement each).
- Eval harness lands; first 3 customer-facing AI features ship with full eval suites.
- Prompt registry — every production prompt versioned, owned, rollback-able.
- Spec-driven flow is now the default. Specs are the AI's primary context.

### Months 10–15: Compound
- Every team has a named AI-leverage bet in their quarterly plan.
- Agent-based PRs allowed in sandboxed scope (refactors, dependency bumps, doc updates) with human approval gate.
- AI cost per merged PR on the scorecard; trended monthly.

### Months 16–18: Operate
- AI usage is invisible — it is simply how we work.
- AI-touched code defect rate is *equal or lower* than human-only code (the bar).
- Customer-facing AI features have measurable trust scores ≥ 4.3/5.

**What we will refuse along the way:**
- Individual AI usage metrics on performance reviews.
- Shipping AI features without evals.
- "AI agents that act on production without human approval" — until we have months of safe sandboxed behavior to justify expanding scope.

---

## 6. The org transitions that will be hard

I name these explicitly so the CEO and board see them coming.

1. **Hiring pace will be uncomfortable.** 80 hires in 18 months while keeping the bar means saying no often. Time-to-fill will lengthen mid-plan. This is correct.
2. **The platform team will feel slow for two quarters.** They are building paved roads while product teams want pavement *now*. Hold the line — the compound payoff is real.
3. **Some current managers will not scale to the new org.** Calibration in months 9–12 will surface this. We will invest in coaching and be honest when it does not work.
4. **AI adoption will create skill anxiety.** Make growth paths and training real; reward judgment, not usage rates.
5. **Reliability investment will compete with shipping.** Error-budget policy makes this a *rule*, not a debate.

---

## 7. What I would ask of the CEO and board

- **Budget envelope** that scales linearly with the plan, including a line item for AI tooling and infra.
- **Hiring authority** with a published bar — and air cover when we say no to "almost" candidates.
- **Patience for two quarters** while the platform investment compounds.
- **Customer voice in the room** — a standing 30-min slot in monthly business reviews for top customer feedback.
- **Permission to say no** to commitments that would break the operating system we are installing.

---

## 8. What the first 90 days look like, day by day (excerpt)

| Day | Activity |
|---|---|
| 1–7 | 1:1s with every Director and every Staff+ IC; 30-min listening tour with PM and CS leadership |
| 8–14 | Diagnostic data pulled across all 5 lenses; first scorecard draft |
| 15–21 | Diagnostic memo to CEO; presentation to leadership team |
| 22–30 | Operating system installation begins: quarterly planning calendar, ARB charter, scorecard published |
| 31–45 | AI policy v1 published and ratified; approved tools list; AI gateway MVP scoped |
| 46–60 | First quarterly planning cycle under the new system; 2 spec-driven pilot teams chartered |
| 61–75 | Platform team charter signed ([example](sample-platform-team-charter.md)); first 3 paved roads scoped |
| 76–90 | First monthly business review with full scorecard; first incident review; first hiring cohort onboarding |

---

## 9. Why this plan works

Three things compound:

1. **The platform makes new hires productive faster.** Each subsequent hire costs less and ships sooner.
2. **Spec-driven + AI compresses TTM dramatically.** A team that captures intent cleanly and uses AI to translate it can ship 3–5× faster than one that does not.
3. **Reliability investment creates trust capital** that buys permission to ship faster, not pressure to ship slower.

The plan does not "balance" tradeoffs. It picks a side: **leverage and trust first, headcount second.** That is the only way 40 → 120 turns into a stronger company instead of a more crowded one.
