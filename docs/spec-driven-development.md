# Spec-Driven Development

> In an AI-first organization, the spec is the source code. Code is increasingly generated, regenerated, and refactored by AI from specifications. The specification — not the implementation — is the durable artifact engineers own.

This is the single biggest shift in how software gets built in 2026, and the operating system has to be designed for it.

## Why specs are now the unit of work

When AI can produce a working implementation from a clear specification in minutes, the bottleneck shifts upstream:

- **Old bottleneck:** typing code, wiring frameworks, writing boilerplate.
- **New bottleneck:** stating intent precisely enough that an AI (and a human reviewer) can verify the result is correct.

The engineer's job becomes: **define the spec, define the acceptance criteria, define the evals, govern the result.** The implementation is an output, not the work product.

This is not a prediction. It is already how the best teams ship. The Engineering Operating System makes it the *default*.

## The four artifacts of a spec-driven team

Every meaningful change produces a chain of artifacts:

```
   Intent Spec   →   Technical Spec   →   Acceptance Spec   →   Implementation
   (what & why)      (how)                (proof of correct)     (code, generated or written)
```

| Artifact | Owner | Lives in | AI role |
|---|---|---|---|
| **Intent spec** | PM + Tech Lead | Product brief / one-pager | AI drafts, humans decide |
| **Technical spec** | Tech Lead or Staff Eng | RFC or [spec template](../templates/spec-template.md) | AI drafts options, human chooses |
| **Acceptance spec** | Tech Lead + QA | Executable: tests, evals, SLO definitions | AI generates; humans curate |
| **Implementation** | Team | Code in repo | AI generates the majority; human reviews |

The acceptance spec is the contract. If the implementation passes the acceptance spec, it ships. If it doesn't, the spec was wrong or the implementation was wrong — and we know which.

## The spec-driven flow

```
1. Problem framed in plain language        (PM + Tech Lead)
2. Intent spec written                     (one page; reviewed in 24h)
3. Technical spec drafted with AI          (tech lead + AI; humans own decisions)
4. Acceptance spec written                 (tests, evals, SLOs, telemetry — before code)
5. Implementation generated/written        (AI-assisted; tracked)
6. Acceptance spec runs in CI              (gate to merge)
7. Telemetry verifies in prod              (gate to declare success)
8. Spec is the artifact that survives      (code may be regenerated; the spec is canonical)
```

Steps 2, 3, 4 happen **before** any non-trivial code. The team's working agreement enforces this.

## What "spec-first" changes about the day-to-day

- **Code reviews** look at the spec first. If the spec is ambiguous, the implementation cannot be evaluated.
- **PR descriptions** link to the spec and state which sections of the spec the change implements.
- **Refactors** are spec-preserving: the acceptance spec must still pass. A refactor that requires the acceptance spec to change is not a refactor — it's a redesign.
- **AI agents** are given the spec as their primary context. The spec is also the *grading rubric* used in evals.
- **Onboarding** new engineers means reading current specs, not reading the whole codebase.

## Specs as living documents

A common failure: specs are written once and abandoned. We prevent this by treating specs as code:

- Specs live in the repo next to the system they describe (`/spec/*.md`).
- Spec changes go through PRs with reviewers.
- Specs are versioned. A spec PR that changes acceptance criteria requires an explicit migration note.
- A drift detector compares production behavior to spec assertions weekly; drift becomes a ticket.

## How big is a spec?

| Spec size | Lifespan | Example |
|---|---|---|
| **Micro** (1–2 pages) | Single PR | "Add idempotency key to checkout API" |
| **Feature** (3–10 pages) | 1–4 sprints | "Multi-currency support" |
| **System** (10–30 pages) | Multi-quarter | "Search ranking v3" |
| **Product** (RFC-grade) | Annual+ | "Workspaces (multi-tenant model)" |

Anything bigger should be decomposed before work starts.

## How spec-driven dev meshes with the rest of the EOS

- **Planning** ([planning rhythm](planning-rhythm.md)): quarterly objectives are stated as spec-level outcomes, not feature lists.
- **Architecture** ([architecture review](architecture-review-process.md)): every RFC produces or updates a spec, never just a design.
- **Execution** ([execution model](execution-model.md)): the spec is the entry condition for the *Build* stage.
- **Productivity** ([productivity measurement](productivity-measurement.md)): "specs shipped to production-passing acceptance" is the primary throughput metric, not commits.
- **AI policy** ([AI policy](ai-assisted-development-policy.md)): specs are the trustworthy context AI agents need to be safe.
- **Ladders** ([career ladders](career-ladders.md)): a Staff engineer is increasingly defined by the *quality of specs they author and review*, not lines of code.

## Anti-patterns I refuse

- **"AI wrote it, ship it."** No spec, no merge.
- **Specs written *after* the code,** as paperwork. This recreates the world we are leaving.
- **Specs without acceptance criteria.** A spec that cannot be falsified is not a spec.
- **Specs that are 80-page Word docs.** Specs are short, in markdown, in the repo. If a spec is too long to read in one sitting, it is too long to ship as one piece.
- **Treating the implementation as canonical.** When the implementation and the spec disagree, the spec wins or the spec changes — explicitly.

## Adoption path (for a team starting today)

1. Pick one upcoming feature. Write a [spec](../templates/spec-template.md) before any code.
2. Generate the acceptance spec (tests + evals + telemetry) before any implementation.
3. Use AI to generate the implementation against the spec.
4. Ship. Measure the cycle time end-to-end.
5. Compare to a similar previously-shipped feature. The team will not go back.

A team typically reaches mature spec-driven flow in 2–3 sprints.
