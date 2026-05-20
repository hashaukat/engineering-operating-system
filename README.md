# Engineering Operating System

> A complete, AI-first operating model for how a modern software engineering organization should run.
>
> This repository captures the operating model, principles, rituals, templates, and measurement systems I would install as a Head of Engineering / VP of Engineering / CTO to take an organization into the next frontier of **AI-augmented software engineering** — while it scales, ships faster, and delights customers.

It is a **leadership artifact**, not a code repository. The goal is a single, comprehensive package an executive could adopt across the majority of software businesses.

---

## The AI-first stance

Everything in this repo is built around six claims about how the best software organizations operate today:

1. **Specs, not code, are the durable artifact.** Code is increasingly generated; the specification is what engineers own. See [spec-driven development](docs/spec-driven-development.md).
2. **AI is in the default path** for discovery, design, build, ship, operate, and learn — with humans as the author of record at every gate. See [AI policy](docs/ai-assisted-development-policy.md).
3. **Decision-making is a first-class engineering skill** — taught, practiced, and measured — because AI raises the supply of plausible options to near-infinite, and judgment is now the scarce resource. See [decision-making](docs/decision-making.md).
4. **We question, verify, and push back on AI** the way we do with a respected peer. Sycophancy and confident-wrongness are the most expensive failure modes of an AI-first org. See [critical thinking with AI](docs/critical-thinking-with-ai.md).
5. **Productivity is measured as customer value delivered per unit time**, not as activity. See [productivity measurement](docs/productivity-measurement.md).
6. **Customer satisfaction is engineering's scoreboard**, not just product's — CSAT, NPS, Time-to-Value, Customer Effort Score, alongside Time-to-Market, reliability, and quality.

The full position is in [docs/ai-first-stance.md](docs/ai-first-stance.md).

---

## Why this exists

Most engineering organizations don't fail because of technology. They fail because the *system* around the engineers — how decisions are made, how work is planned, how reliability is governed, how careers progress, how AI is adopted — is implicit, inconsistent, or absent.

An **Engineering Operating System (EOS)** makes that system explicit. It is the layer that turns talented individuals into a compounding organization.

This repo answers three questions a board, CEO, or hiring committee would ask me:

1. **How do you think?** — See [operating principles](docs/operating-principles.md), [engineering strategy](docs/engineering-strategy.md), and [AI-first stance](docs/ai-first-stance.md).
2. **How do you operate?** — See [spec-driven development](docs/spec-driven-development.md), [planning rhythm](docs/planning-rhythm.md), [execution model](docs/execution-model.md), [productivity measurement](docs/productivity-measurement.md), and [metrics scorecard](docs/metrics-scorecard.md).
3. **How do you scale?** — See [org design](docs/org-design.md), [team topologies](docs/team-topologies.md), [career ladders](docs/career-ladders.md), and the mock scenario in [examples/mock-q3-engineering-plan.md](examples/mock-q3-engineering-plan.md).

---

## Mock scenario: the through-line

Every artifact in this repo is written against one realistic transformation:

> **Scale a 40-person engineering org to 120 people in 18 months while reducing deployment friction, improving reliability (99.5% → 99.95%), and introducing AI-assisted development safely.**

Read the full plan in [examples/mock-q3-engineering-plan.md](examples/mock-q3-engineering-plan.md).

---

## Repository map

### `docs/` — the operating model
| Document | Purpose |
|---|---|
| [start-here-for-new-managers.md](docs/start-here-for-new-managers.md) | **Start here.** The whole-story walkthrough: Week 1 → 30 days → quarter → year |
| [ai-first-stance.md](docs/ai-first-stance.md) | What "AI-first" actually means and what changes because of it |
| [engineering-strategy.md](docs/engineering-strategy.md) | The 3-horizon strategy and how engineering compounds business value |
| [operating-principles.md](docs/operating-principles.md) | The 12 principles I use to make decisions |
| [decision-making.md](docs/decision-making.md) | Decision-making as a first-class engineering skill: door types, DACI, pre-mortems, calibrated confidence, decision logs |
| [critical-thinking-with-ai.md](docs/critical-thinking-with-ai.md) | Question, verify, push back: the anti-gullibility doctrine for an AI-first org |
| [spec-driven-development.md](docs/spec-driven-development.md) | Specs as the durable artifact; how teams ship in an AI-augmented world |
| [org-design.md](docs/org-design.md) | How I structure reporting lines, spans, and layers |
| [team-topologies.md](docs/team-topologies.md) | Stream-aligned, platform, enabling, and complicated-subsystem teams |
| [planning-rhythm.md](docs/planning-rhythm.md) | Annual → quarterly → sprint cadence |
| [execution-model.md](docs/execution-model.md) | How work flows from intent to production |
| [developer-experience.md](docs/developer-experience.md) | The paved roads, the platform, and the DevEx promise that makes the system livable |
| [quality-engineering.md](docs/quality-engineering.md) | Testing, gates, flakiness policy, and evals as a parallel quality pyramid |
| [release-engineering.md](docs/release-engineering.md) | Decoupling deployment from release; canary, flags, kill switches, AI-feature rollout |
| [security-and-supply-chain.md](docs/security-and-supply-chain.md) | Provenance, SBOMs, SLSA, AppSec, AI-specific threats, and incident response |
| [data-and-privacy-governance.md](docs/data-and-privacy-governance.md) | Classification, consent, retention, AI training data, RAG, regulatory baseline |
| [engineering-finops.md](docs/engineering-finops.md) | Cost as a first-class signal, including AI inference cost management |
| [productivity-measurement.md](docs/productivity-measurement.md) | DORA + SPACE + DX + AI metrics + TTM + customer value, unified |
| [metrics-scorecard.md](docs/metrics-scorecard.md) | The leadership scorecard rolled up across all measurement lenses |
| [incident-management.md](docs/incident-management.md) | On-call, severity, command, and learning |
| [architecture-review-process.md](docs/architecture-review-process.md) | ADRs, RFCs, and the architecture council |
| [career-ladders.md](docs/career-ladders.md) | IC and management tracks, IC4–IC8 / M3–M6 |
| [hiring-process.md](docs/hiring-process.md) | Sourcing, loop design, bar raising, and onboarding |
| [ai-assisted-development-policy.md](docs/ai-assisted-development-policy.md) | How we use Copilot, agents, and evals safely |
| [ai-agent-governance.md](docs/ai-agent-governance.md) | Governance for autonomous agents that *act*: scoping, identity, kill switches, review |
| [common-pitfalls.md](docs/common-pitfalls.md) | The avoidable mistakes this operating system is designed to prevent, mapped to the antidote |

### `templates/` — what teams actually use
- [spec-template.md](templates/spec-template.md) — the spec-driven development working artifact
- [decision-record-template.md](templates/decision-record-template.md) — lightweight non-architectural decision record
- [ai-feature-eval-template.md](templates/ai-feature-eval-template.md) — eval suite for customer-facing AI
- [quarterly-planning-template.md](templates/quarterly-planning-template.md)
- [architecture-decision-record.md](templates/architecture-decision-record.md)
- [one-page-strategy-template.md](templates/one-page-strategy-template.md)
- [postmortem-template.md](templates/postmortem-template.md)
- [team-health-survey.md](templates/team-health-survey.md)
- [staff-engineer-scope-template.md](templates/staff-engineer-scope-template.md)

### `examples/` — the system applied
- [mock-q3-engineering-plan.md](examples/mock-q3-engineering-plan.md) — the 40→120 scaling plan, AI-first
- [sample-platform-team-charter.md](examples/sample-platform-team-charter.md)
- [sample-okr-scorecard.md](examples/sample-okr-scorecard.md)
- [sample-spec-checkout-idempotency.md](examples/sample-spec-checkout-idempotency.md) — a worked spec-driven example

### `skills/` — the tunable practice library
The docs are the policy; the [skills library](skills/README.md) is the muscle. 16 essential, generic skills — foundational, engineering, management, leadership — each written to be **tuned**, not adopted verbatim, with practice, drills, failure modes, and named further reading.

- **Foundational (everyone):** [critical-thinking-and-judgment](skills/critical-thinking-and-judgment.md), [working-with-ai](skills/working-with-ai.md), [technical-writing](skills/technical-writing.md), [giving-and-receiving-feedback](skills/giving-and-receiving-feedback.md)
- **Engineering craft:** [writing-specs](skills/writing-specs.md), [code-review](skills/code-review.md), [debugging](skills/debugging.md), [incident-response](skills/incident-response.md), [estimation-and-forecasting](skills/estimation-and-forecasting.md)
- **Management craft:** [running-one-on-ones](skills/running-one-on-ones.md), [coaching-and-growth](skills/coaching-and-growth.md), [hiring-and-interviewing](skills/hiring-and-interviewing.md), [running-effective-meetings](skills/running-effective-meetings.md)
- **Leadership craft:** [strategic-thinking](skills/strategic-thinking.md), [prioritization-and-saying-no](skills/prioritization-and-saying-no.md), [influence-and-executive-communication](skills/influence-and-executive-communication.md)

---

## How to read this repo

- **If you are a new-ish manager and want the whole story:** start with [start-here-for-new-managers.md](docs/start-here-for-new-managers.md) — it walks you from Week 1 through your first year using the rest of this repo.
- **If you have 5 minutes:** read this README and [operating principles](docs/operating-principles.md).
- **If you have 20 minutes:** add [AI-first stance](docs/ai-first-stance.md), [decision-making](docs/decision-making.md), [critical thinking with AI](docs/critical-thinking-with-ai.md), and the [mock Q3 plan](examples/mock-q3-engineering-plan.md).
- **If you have an hour:** read everything in `docs/` in the order listed in the table above.
- **If you are stress-testing this system:** read [common-pitfalls.md](docs/common-pitfalls.md) — the well-known engineering-org failure modes and the specific antidote in this EOS for each.

---

## How this is meant to be used

This operating system is deliberately **domain-agnostic**. It is designed to apply to the majority of software organizations — B2B SaaS, B2C product, fintech, marketplace, infrastructure, AI-native — adjusting the *parameters* (team sizes, SLO targets, customer-value metrics) rather than the *structure*.

Adopt it three ways:

1. **As-is** for a new or rebuilding org — install the rituals, templates, and scorecard verbatim and tune over two quarters.
2. **As a diagnostic** for an existing org — read it against your current practice and find the gaps.
3. **As a recruiting / interview artifact** — for leaders who want to communicate how they think, this is the artifact.

## A note on AI

Every section of this operating system is written assuming engineers work alongside AI agents and that AI is in the default path of how work gets done. The org design, the metrics, the career ladders, the review process, the spec-driven flow, and the incident model are all designed for a world where a meaningful share of code, tests, specs, and operations are produced or accelerated by AI. The goal is not to celebrate the tools — it is to make the organization that wields them safer, faster, more measurable, and more humane.

