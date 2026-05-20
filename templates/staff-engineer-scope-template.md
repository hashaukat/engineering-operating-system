# Staff Engineer Scope Document

> The contract between a Staff+ engineer and the organization. Defines what they own, what they influence, and how success is measured. Reviewed every 6 months. Aligned with the IC track in [career ladders](../docs/career-ladders.md).

| Field | Value |
|---|---|
| Engineer | `<name>` |
| Level | IC5 \| IC6 \| IC7 \| IC8 |
| Reporting EM / Director | `<name>` |
| Sponsor (skip-level) | `<name>` |
| Time horizon | `6 / 12 months` |
| Last updated | `YYYY-MM-DD` |

---

## 1. Scope of impact

In one sentence, the *territory* this engineer is accountable for. Be specific — "scaling" or "quality" is not a scope; "the search ranking system across web, iOS, and Android" is.

> **Scope:** `<one sentence>`

## 2. The 3–5 outcomes for this horizon

Concrete, measurable. Each outcome maps to a strategy horizon (H1/H2/H3 per [strategy](../docs/engineering-strategy.md)).

| # | Outcome | Strategy horizon | Metric / evidence |
|---|---|---|---|
| 1 | | | |
| 2 | | | |

## 3. The systems this engineer owns

- `<system A>` — accountable for architecture, evolution, on-call rotation
- `<system B>` — co-owns with `<team>`; advisory role
- `<system C>` — sunsetting; owns the deprecation plan

## 4. The decisions this engineer is the decider on

- Architectural direction for `<area>`
- Tooling choices for `<area>`
- Tech-lead-of-record on the [ARB](../docs/architecture-review-process.md) for `<scope>`

## 5. The decisions this engineer informs but does not own

- Hiring decisions on `<team>` — provides technical sign-off
- Product roadmap for `<area>` — provides technical feasibility input

## 6. Leverage commitments

A Staff+ engineer is judged on leverage, not personal output. Each commitment is measurable.

- **Spec authorship:** authors or substantially reviews ≥ `<n>` significant specs per quarter ([spec-driven dev](../docs/spec-driven-development.md))
- **Mentoring:** named mentor for `<n>` engineers; reviews their growth quarterly
- **Org-wide contributions:** `<e.g., owns the eval harness used by 5 teams>`
- **External:** `<e.g., maintains 1 talk / 2 OSS contributions / 1 blog per year>` (IC6+)
- **AI judgment:** sets norms for AI usage on their teams; reviews AI-feature evals ([AI policy](../docs/ai-assisted-development-policy.md))

## 7. What this engineer is explicitly NOT doing

The hardest part of staff scope is what to *say no to*. Examples:

- Not the deep expert on `<adjacent area>` — that's `<other engineer>`
- Not personally writing the majority of the code on their team
- Not the people manager for their team

## 8. Success criteria (6-month check)

How both sides will know this is working.

- [ ] Outcomes 1–N met (with evidence)
- [ ] Leverage commitments met
- [ ] Survey signal: team reports they understand and value this engineer's role
- [ ] Sponsor and EM both report this engineer is operating at level

## 9. Failure modes to watch

We name these on purpose so we can see them coming.

- **Hero pattern:** doing everything themselves, not multiplying others
- **Drift:** scope quietly broadening to include everything interesting
- **Architecture-astronaut:** specs and RFCs without grounded customer impact
- **Conflict avoidance:** not making hard calls; deferring to consensus

## 10. Career growth direction

- Where this engineer wants to be in 12–24 months
- Gaps they are working on
- Stretch opportunities being arranged

## 11. Sign-off

| Role | Name | Signed |
|---|---|---|
| Engineer | | |
| EM / Director | | |
| Sponsor (skip-level) | | |

---

## How this is used

- **Quarterly check-in:** engineer + EM review the doc; update progress.
- **Calibration:** the document is the primary input to promotion calibration ([career ladders](../docs/career-ladders.md)).
- **Disagreement:** if the engineer's actual work drifts from the scope doc, that is a conversation — *not* a surprise.
