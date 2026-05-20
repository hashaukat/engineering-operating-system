# Architecture Review Process

> Architecture is the set of decisions that are expensive to change. The job of the review process is not to slow them down — it is to make sure we make them once, deliberately, and with the right people in the room.

## The three artifacts

| Artifact | Used for | Owner | Review forum |
|---|---|---|---|
| **ADR** (Architecture Decision Record) | A specific decision with options and tradeoffs | Author engineer | Team or ARB depending on scope |
| **RFC** (Request for Comments) | A proposed design, often larger than a single decision | Author engineer or Staff | Async first, then ARB if needed |
| **Tech Spec** | An implementation plan once direction is set | Team | Team self-review |

ADR template: [`templates/architecture-decision-record.md`](../templates/architecture-decision-record.md).

## When you need an ADR / RFC

Use the **blast radius** test. Write a doc if any of these apply:

- Affects more than one team.
- Introduces a new external dependency, cloud service, or data store.
- Changes a public API or wire protocol.
- Affects security, compliance, or PII handling.
- Costs > $50k/year in infra or licensing.
- Is hard to reverse (data model, vendor commitment, language/runtime choice).

If none apply, you do not need an RFC. Just build it well and write good commit messages.

## The Architecture Review Board (ARB)

A small, rotating group — not a permanent committee.

- **Standing members (3):** the Head of Architecture or most senior platform Staff+, the Security Engineering lead, the Head of Engineering or a delegated Director.
- **Rotating members (2):** two Staff+ engineers from product teams, rotating quarterly.
- **Cadence:** weekly 60-min meeting; async review the other 6 days.

**The ARB does not approve every decision.** Teams own their architecture. The ARB is convened only for cross-team or high-blast-radius decisions, and acts as advisor-of-record for the rest.

## Review flow

```
Draft RFC  →  Async comments (5 business days)  →  Author revises  →  Decision
                                                                          │
                                                ┌─────────────────────────┤
                                          Team-scope                 ARB-scope
                                                │                         │
                                          Tech Lead signs           ARB 60-min review
                                                                          │
                                                                    Decision recorded
```

**Definition of decision:** the RFC is updated with the outcome, the date, and the author of record. Decisions are not "verbal during a meeting."

## Decision rights

| Scope | Decider |
|---|---|
| Within a single service owned by one team | Team Tech Lead |
| Cross-team within one domain | Group EM + Domain Staff Engineer |
| Cross-domain / platform-affecting | ARB |
| Vendor / cost > $250k/yr or new compliance regime | Head of Engineering + CFO/Legal |

The principle: **push decisions to the smallest unit that has the context and the accountability.** Centralize only when the decision creates externalities.

## ADR lifecycle

Every ADR has a status:

- **Proposed** — under review.
- **Accepted** — current decision.
- **Superseded by ADR-NNN** — replaced; both ADRs link to each other.
- **Deprecated** — no longer recommended; not yet replaced.

ADRs live in `/architecture/decisions/` inside the relevant repo and are *never deleted*. The history is the value.

## AI in architecture work

- **Allowed:** drafting RFC sections, generating alternative designs to consider, summarizing prior ADRs, critiquing a draft.
- **Required:** the author of record is a human. The RFC must state which sections were AI-drafted.
- **Best practice:** when AI generates an alternative, *write down why we rejected it*. This builds organizational memory.

## What I refuse

- Verbal architecture decisions. If it is worth deciding, it is worth writing down.
- ARBs that become bottlenecks. If the ARB queue is > 2 weeks, we add capacity or push decisions back to teams.
- "Architecture by retrofit" — ADRs written after the code is already in main as paperwork.
- ARB members who only critique. Membership requires offering alternatives.
