# Engineering Strategy

> Strategy is a small number of hard choices about where engineering will and will not invest, expressed clearly enough that any engineer can use it to make a tradeoff on a Tuesday afternoon.

## 1. The job of engineering

Engineering exists to **compound business value through software**. That compounding has three sources:

1. **Throughput** — the rate at which we convert intent into shipped, working software.
2. **Leverage** — the rate at which each engineer's output is multiplied by platforms, abstractions, and AI.
3. **Trust** — the reliability, security, and quality that allow customers and the business to plan around us.

A good strategy improves all three. A great strategy makes the *next* strategy easier.

## 2. The 3-horizon model

| Horizon | Timeframe | Question | Allocation |
|---|---|---|---|
| **H1 — Run** | 0–6 months | Are we operationally excellent at what we do today? | 60% |
| **H2 — Grow** | 6–18 months | Are we widening our moat in the products customers already pay for? | 30% |
| **H3 — Transform** | 18–36 months | Are we building the capability that will define the company in 3 years? | 10% |

Allocation is a *forcing function*. If H3 falls to zero, the company will be disrupted. If H1 falls below 50%, the company will lose its customers before it gets to H3.

## 3. Where I choose to invest

For the [mock scenario](../examples/mock-q3-engineering-plan.md), the strategy is:

1. **Platform first.** A small platform team is the single highest-leverage investment when scaling 3x. Build paved roads before pouring more engineers onto them.
2. **Reliability as a product.** Move from 99.5% → 99.95% by treating SLOs as planning inputs, not afterthoughts.
3. **AI as a multiplier, not a layoff lever.** Adopt AI-assisted development to raise the floor of every engineer, with safety rails — see [AI policy](ai-assisted-development-policy.md).
4. **Stream-aligned ownership.** Reorganize around customer-facing value streams ([team topologies](team-topologies.md)), not technical silos.
5. **Quality at the source.** Invest in test infrastructure, observability, and review tooling so that quality is cheaper than rework.

## 4. Where I choose *not* to invest

Strategy is also subtraction. In the mock scenario, I would explicitly **not**:

- Rewrite the monolith. Strangle, don't rewrite.
- Build an internal ML platform. Buy or rent until our usage justifies it.
- Adopt a second cloud. Multi-cloud is a tax most organizations of this size cannot afford.
- Roll our own AI evals framework. Use an existing one and contribute back.

## 5. How strategy shows up in the operating system

A strategy that lives only in a deck is decoration. This one shows up in:

- **Planning** — every quarterly objective is mapped to an H1/H2/H3 horizon ([planning rhythm](planning-rhythm.md)).
- **Hiring** — the [hiring plan](hiring-process.md) is shaped by team topology, not headcount targets.
- **Architecture** — RFCs must state which strategic bet they advance ([architecture review](architecture-review-process.md)).
- **Metrics** — the [scorecard](metrics-scorecard.md) measures throughput, leverage, and trust separately.

## 6. Strategy review cadence

- **Monthly:** leadership team reviews the scorecard against strategy.
- **Quarterly:** strategy is re-stated, not re-written. We change the *plan* often; we change the *strategy* rarely.
- **Annually:** the 3-horizon allocation is debated and re-set with the CEO and board.
