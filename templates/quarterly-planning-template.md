# Quarterly Planning Template

> Use with the cadence defined in [planning-rhythm.md](../docs/planning-rhythm.md). One per team, per quarter. Maximum 2 pages. If it is longer, it is not a plan.

## Header

| Field | Value |
|---|---|
| Team | `<team name>` |
| Quarter | `Q<n> YYYY` |
| EM | `<name>` |
| Tech Lead | `<name>` |
| Product Partner | `<name>` |
| Headcount (start of qtr) | `<n>` |
| Headcount (planned end) | `<n>` |
| Document status | Draft \| Reviewed \| Signed |

## 1. Outcomes (1–3 max)

Each outcome is a measurable change in a customer or business metric. **Not features. Not projects.**

For each outcome:

- **Outcome statement** — one sentence. Verb + metric + target + window.
  > *Example: "Reduce p75 enterprise checkout latency from 2.4s → 1.2s by end of quarter, measured via RUM."*
- **Strategy horizon** — H1 / H2 / H3 (per [strategy](../docs/engineering-strategy.md))
- **Why this, why now** — 2 sentences
- **Primary spec(s)** — links to the [specs](spec-template.md) that deliver this outcome
- **Customer-value metric impacted** — which CSAT / NPS / TTV / CES signal
- **Definition of done** — what evidence will we accept that the outcome was met

## 2. Non-goals

Things we are explicitly *not* doing this quarter. This is how we say no on purpose.

- `<thing>` — because `<reason>`
- `<thing>` — because `<reason>`

## 3. Capacity model

| Allocation | % | Engineer-weeks |
|---|---|---|
| Planned outcome work | ≤ 70% | |
| Unplanned (interrupts, escalations) | 15% | |
| Reliability / tech debt | 10% | |
| Learning / 20% time | 5% | |

If planned work > 70%, the plan is overcommitted. Cut scope before signing.

**On-call burden this quarter:** `<weeks per engineer>`. Above 1 in 4 triggers a reliability investment.

## 4. Risks (top 3)

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| | H/M/L | H/M/L | | |

## 5. Dependencies

Things this team needs from other teams to succeed. Each line has a named owner on the other side and a date by which we need it.

| Need | From team | Owner | Needed by |
|---|---|---|---|

## 6. AI leverage assumption

Per the [AI policy](../docs/ai-assisted-development-policy.md) and [productivity measurement](../docs/productivity-measurement.md):

- AI tooling we expect to lean on this quarter: `<list>`
- Spec-shipping target (count of specs taken from intent → acceptance passing in prod): `<n>`
- Specific bets on AI leverage: `<e.g., "test generation expected to halve QA cycle on feature X">`
- AI-related risks: `<list>`

## 7. Hiring this quarter

| Role | Level | Start of loop | Target start date |
|---|---|---|---|

Hiring load (interview hours per engineer per week) should not exceed `<n>`. If it does, it is on the risk list.

## 8. Sign-off

| Role | Name | Signed |
|---|---|---|
| EM | | |
| Tech Lead | | |
| Product Partner | | |
| Director | | |

---

## Mid-quarter review (filled in week 6)

- Outcomes on track / at risk / off track — with one-line update on each
- Anything we are choosing to drop or descope
- Updated risk list
- One ask of leadership (if any)
