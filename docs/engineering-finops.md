# Engineering FinOps & AI Cost Management

> The bill is real. In an AI-first org, cloud + AI inference can grow from a rounding error to a top-3 line item in 18 months. This doc is how we keep that growth tied to value, not surprise.

Engineering FinOps is not about *spending less*. It is about **knowing what we spend, why, and whether it's earning its keep** — so leadership can choose to invest more where it returns and less where it doesn't.

---

## The three financial guarantees

1. **Transparency** — every team can see, weekly, what their slice of cloud + AI spend is and how it's trending.
2. **Attribution** — every cost line is traceable to a service, team, customer, or feature. Unattributed cost is a finding.
3. **Unit economics** — for revenue-generating features, we know cost-per-request and cost-per-customer. For internal features, we know cost-per-engineer or cost-per-workflow.

If a team cannot answer "what does this feature cost us per active user?", that is a leadership-attention item, not an accounting one.

---

## What we track

| Domain | Tracked |
|---|---|
| **Cloud compute** | Per service, per environment, per team. Cost / request, cost / DAU, cost / GB processed |
| **Storage & data transfer** | Per service. Egress is the silent budget killer; tracked separately |
| **Databases & caches** | Per cluster, per team. Right-sizing reviewed quarterly |
| **AI model inference** | Per feature, per model, per prompt template, per customer-segment if relevant |
| **AI training / fine-tuning** | Per project, including data prep |
| **AI tooling (assistants, agents)** | Per team. Not per individual — see [productivity-measurement.md](productivity-measurement.md) |
| **Observability & security tooling** | Vendor-by-vendor; growth tracked relative to traffic |
| **Build, CI, artifact registries** | Per team |

Each domain has an **owner** (named person), a **budget** (set during quarterly planning), and an **alerting threshold** (e.g., page on 50% / 80% / 100% of monthly budget consumed).

---

## The FinOps loop

Borrowed from the [FinOps Foundation](https://www.finops.org/framework/) framework:

1. **Inform** — visibility. Dashboards per team, weekly digest, monthly review.
2. **Optimize** — right-size, schedule, commit, refactor. Driven by data, owned by teams.
3. **Operate** — automate the controls (auto-scaling, idle shutdown, tier transitions); make wasteful choices hard.

The loop runs continuously; we do not do "the annual cost review."

---

## Cost on the scorecard

Cost is a first-class signal on the [metrics scorecard](metrics-scorecard.md):

- **% of cost attributed** to a team / service / feature (target: > 95%)
- **Cost growth vs traffic growth** (cost should sub-linearly track demand; if it doesn't, that's the investigation)
- **Cost per unit of customer value** (cost / DAU, cost / transaction, cost / completed workflow)
- **% of cost on committed-use / reserved** vs on-demand
- **Idle / unused resource %** (trending toward zero)
- **AI inference cost per AI-feature request** with quality alongside (cheap and bad is not a win)

---

## AI cost management — the new discipline

AI inference cost behaves unlike traditional cloud cost: it scales with *user activity* and *model choice*, has rapidly changing vendor pricing, and can spike from a bad prompt change overnight.

### Standing practices

- **Budget at the feature level.** Every AI-backed feature has a monthly spend ceiling and an alert before it.
- **An AI Gateway** (see [developer-experience.md](developer-experience.md) and [ai-first-stance.md](ai-first-stance.md)) — one place all model calls go through, where rate limits, cost tracking, model routing, and audit logging happen. No team calls vendor APIs directly.
- **Model routing by stake.** Cheap/fast model by default; expensive/capable model only when the task warrants it. Routing decisions are part of the [spec](../templates/spec-template.md).
- **Prompt cost reviews.** Long prompts and verbose responses are a cost line item. Token-cost is part of the AI feature review.
- **Caching.** Semantic caching for repeated questions; embedding caches for retrieval. Paved-road capability.
- **Eval cost is budgeted.** Eval suites that cost more than they save get redesigned.
- **Cost regression alerts.** A sudden 2× in cost-per-request pages the team. Treat as a Sev3 incident class.
- **Per-customer cost monitoring.** Detect the customer whose query pattern is costing 100× the average; address via product, not just infrastructure.

### Vendor strategy

- **Multiple model providers** evaluated; portability designed in (prompt portability, retrieval portability).
- **Self-hosted / open-weights option** for at least one workload class, to retain leverage.
- **Contract reviews quarterly.** AI pricing moves fast; long-term contracts only when the math justifies it.
- **Avoid sticky vendor primitives** in the critical path (proprietary tool-calling shapes, proprietary embeddings).

---

## Cloud cost — the boring fundamentals (still required)

- **Tagging discipline.** Every resource tagged with team, service, environment, cost-center. Untagged resources are blocked from creating in production accounts.
- **Right-sizing.** Quarterly review; automated where possible (managed services, autoscaling groups with realistic targets).
- **Commitments.** RIs / Savings Plans / Committed-use discounts for the steady-state baseline.
- **Idle elimination.** Scheduled shutdown for non-prod outside business hours. Idle resources auto-detected and pinged to owner.
- **Data transfer.** Architect around egress. Multi-region traffic patterns reviewed.
- **Storage lifecycle.** Hot → warm → cold → delete, with policy. Old logs and backups age out automatically.

---

## How cost shows up in planning

- **Quarterly planning** ([planning-rhythm.md](planning-rhythm.md), [quarterly-planning-template.md](../templates/quarterly-planning-template.md)) includes a cost projection per major initiative.
- **Specs** ([spec-template.md](../templates/spec-template.md)) include an "operational cost" section for any non-trivial feature, with AI-inference cost called out explicitly.
- **ADRs** ([architecture-decision-record.md](../templates/architecture-decision-record.md)) include a cost dimension in the trade-off comparison.
- **Postmortems** ([postmortem-template.md](../templates/postmortem-template.md)) for cost-incidents go through the same blameless process as reliability incidents.

---

## Roles

- **Each team** owns the cost of the services and features it owns. End of negotiation.
- **A FinOps lead** (often inside the platform team) owns the tooling, the dashboards, the quarterly review, the vendor strategy. Enabler, not gatekeeper.
- **The Director / VP of Engineering** owns the org-wide cost target at the board, communicates trade-offs to the CFO.
- **The CTO and CFO** partner on a quarterly cost-vs-value review; not an interrogation, a strategic look at where to invest more and where to retreat.

---

## Anti-patterns to name and kill

- **Cost as a finance problem.** Engineering owns its bill. Finance helps with allocation and contracts.
- **Hero cost-cutting.** A single engineer cleans up 30% of waste in a heroic week. Predictable: it grows back in two quarters because the system didn't change.
- **Optimizing without measuring value.** Cutting cost on a service that drives 40% of revenue is a bad trade.
- **"Cloud is cheap."** It isn't. At scale it is the single largest variable cost in many software businesses.
- **AI usage without budgets.** "Just turn it on" → six months later, surprise on the monthly invoice.
- **Per-individual AI cost tracking used punitively.** Track at *team* and *feature* level. Individual surveillance kills experimentation. See [AI policy](ai-assisted-development-policy.md).
- **Long, vague prompts in hot paths.** Cost per request grows linearly with prompt length. Cheap to fix, often un-noticed.

---

## Further reading

- **FinOps Foundation** — [FinOps Framework](https://www.finops.org/framework/) — the standard practitioner reference.
- **J.R. Storment & Mike Fuller** — *Cloud FinOps* (O'Reilly, 2nd ed.) — the canonical book.
- **Corey Quinn** — [Last Week in AWS](https://www.lastweekinaws.com/) — cloud cost reality, weekly.
- **AWS / GCP / Azure pricing calculators and well-architected frameworks** — vendor-specific but useful baselines.
- **Anyscale, Together, Anthropic, OpenAI, Google** — published inference pricing; reread quarterly because it moves.
