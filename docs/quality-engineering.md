# Quality Engineering

> Quality is a property of how we work, not a stage we add at the end. In an AI-first world where code is generated faster than humans can read it, **automated quality is the only quality that scales**.

This doc defines the testing strategy, the eval discipline for AI features, and the quality gates that apply to every change.

---

## The five principles of quality

1. **Quality is built-in, not bolted on.** Tests, evals, and reviews are part of the work, not a separate phase.
2. **Tests describe behavior, not implementation.** A test that breaks every time you refactor is a maintenance burden masquerading as a safety net.
3. **Coverage is a *floor*, not a goal.** 80% coverage of trivial getters is not safety. 100% coverage of the payment path is.
4. **AI evals are tests.** AI-backed features need eval suites as much as services need unit tests. No evals → no ship.
5. **Slow tests are broken tests.** A test suite that engineers skip is worse than no suite at all.

---

## The testing pyramid (and why it still matters)

```
        ╱──╲   E2E / UI / journey  ─ 5–10%
       ╱────╲  Integration / contract ─ 20–30%
      ╱──────╲ Unit / component ─ 60–70%
     ────────
```

Inverting the pyramid (lots of slow E2E tests, few fast unit tests) is the single most common testing anti-pattern. We invest in the foundation and pay it forward in CI speed.

| Layer | Purpose | Owner | Speed target |
|---|---|---|---|
| **Unit** | A function or class behaves correctly | Author of the change | < 5ms each |
| **Component** | A module behaves correctly with internal collaborators | Author | < 50ms each |
| **Integration** | A service behaves correctly with its real dependencies (DB, queue, etc.) | Team | < 1s each |
| **Contract** | Services agree on their interfaces | Both teams (consumer-driven) | < 1s each |
| **End-to-end** | A user journey works across services | Team | reserved for happy-path smoke + a small set of critical journeys |
| **Performance / load** | The system meets latency / throughput targets | Team + platform | scheduled, not per-PR |
| **Security** | SAST / DAST / dependency scans | Platform + team | per-PR + scheduled — see [security-and-supply-chain.md](security-and-supply-chain.md) |

---

## Quality gates

Every PR to a production service passes through these gates **automatically**. Manual gates are the failure mode.

1. **Lint + format** — no warnings, no style debate.
2. **Type check** — for typed languages, errors block.
3. **Unit + component tests** — must pass.
4. **Coverage delta** — coverage of changed code must not decrease meaningfully (default: ≥80% on changed files).
5. **Integration tests** — relevant subset based on changed paths.
6. **SAST + SCA + secrets scan** — see [security-and-supply-chain.md](security-and-supply-chain.md).
7. **License scan** — block disallowed licenses.
8. **Spec linkage** — for non-trivial PRs, link to the spec ([spec-driven-development.md](spec-driven-development.md)).
9. **Human review** — at least one approving review; CODEOWNERS for sensitive paths.
10. **Eval suite** (for AI-backed code paths) — must pass.

Gates are the **same for AI-generated and human-written code**. The author of record (human) is accountable either way ([AI policy](ai-assisted-development-policy.md)).

---

## AI evals as tests — the new discipline

For any code path that calls a model (LLM, classifier, retrieval system, agent), traditional unit tests are insufficient because the output is non-deterministic and the failure modes are subtle.

**Treat evals as a parallel pyramid:**

| Layer | Purpose | Cadence |
|---|---|---|
| **Unit-level evals** | Specific prompt or function produces expected structured output | Per-PR |
| **Offline benchmark** | Known-answer regression set | Per-PR for changed components; per-model-version for shared models |
| **LLM-as-judge** | Subjective quality at scale (helpfulness, faithfulness, tone) | Nightly on sampled prod traffic |
| **Human review** | Ground truth on edge cases | Weekly on sampled set |
| **Safety / red-team** | Adversarial inputs, prompt injection, harmful outputs | Pre-launch + quarterly + on any model/prompt change |

Full template: [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md).

**Eval suite requirements (table-stakes):**

- Stored in the repo, versioned with the code.
- Owned by a named human.
- Rollback criteria defined *before* launch, not after the first regression.
- Cost-bounded — evals that cost more per run than they save are a finding.
- Run on **every** model/prompt change, treated as critical CI.

---

## Test data management

Often where teams' quality bleeds out. Standing rules:

- **Production data is never used in non-prod environments** without explicit, scoped, time-limited approval from Data Governance ([data-and-privacy-governance.md](data-and-privacy-governance.md)).
- **Synthetic data generation** is a paved-road capability. Realistic-enough, privacy-safe by construction.
- **Fixtures are versioned** and live with the code, not in a SQL dump someone emailed.
- **Database migrations** have rollback paths tested in CI.

---

## Flakiness — the silent quality killer

A flaky test (passes sometimes, fails sometimes) is **worse than no test**. It teaches engineers to retry CI instead of believing it.

Standing policy:

- A test failing flakily is **quarantined within one working day** (excluded from CI's blocking set, tagged as flaky).
- A quarantined test is **fixed or deleted within one week**.
- Teams report flaky-test count on the [scorecard](metrics-scorecard.md); persistent flakiness is a finding.

---

## Performance & load testing

- Critical user journeys have **performance budgets** (p95 / p99 latency, throughput, memory).
- **Continuous performance testing** for tier-1 services; not just before launch.
- **Load test before launches** that change the request shape, scale, or downstream calls.
- **Synthetic monitoring** in production for the critical journeys.

---

## Quality metrics — what we track

On the [scorecard](metrics-scorecard.md):

| Metric | Lens |
|---|---|
| **Change failure rate** | Delivery / reliability |
| **Mean time to restore** | Reliability |
| **Escaped defects per release** | Delivery |
| **% of services with current SLOs** | Reliability |
| **% of AI-backed features with passing eval suite** | AI quality |
| **Test suite duration (p75)** | Delivery / DevEx |
| **Flaky-test count per team** | DevEx |
| **% of changed code covered (rolling)** | Delivery |
| **Customer-reported bug rate** | Customer value |

What we *don't* track: lines of test code, test counts in isolation, individual engineer's "test coverage." Those metrics gamify quickly and predict nothing.

---

## Quality across the lifecycle

| Lifecycle stage | Quality practice |
|---|---|
| **Discovery** | Define success criteria in the [spec](../templates/spec-template.md); identify failure modes |
| **Design** | Threat model in the [ADR](../templates/architecture-decision-record.md); identify test seams |
| **Build** | Tests written with the code; PRs gated automatically |
| **Ship** | Progressive delivery with kill switches ([release-engineering.md](release-engineering.md)) |
| **Operate** | SLOs, monitors, alerts, synthetic checks ([incident-management.md](incident-management.md)) |
| **Learn** | Postmortems include "what test should have caught this" ([postmortem-template.md](../templates/postmortem-template.md)) |

---

## Roles

- **Every engineer** owns the tests of the code they write.
- **No "QA team that catches bugs at the end."** That model failed in 2010 and is unrecoverable in 2026. Quality is upstream.
- **Quality engineering specialists** (when the org is large enough) embed with stream teams to build test infrastructure, eval harnesses, and frameworks — *enablers*, not gatekeepers.
- **Staff+ engineers** are expected to raise the team's testing bar — visible in the [career ladder](career-ladders.md).

---

## Anti-patterns to name and kill

- **"We'll add tests later."** Later never comes.
- **The inverted pyramid.** Lots of slow E2E tests, no unit tests. Predicts disaster.
- **Coverage as a target.** People game it with trivial tests; real coverage drops.
- **Tests asserting implementation details.** Refactors break tests; team stops refactoring; rot sets in.
- **AI-generated tests that don't actually catch regressions.** Verify your tests fail when the code is broken. If they pass either way, they are noise.
- **Skipping evals on AI features because "we tested it manually."** Manual testing of stochastic systems is not a quality strategy.
- **CI as the testing strategy.** Tests should be runnable locally in seconds; CI is the backstop, not the discovery path.

---

## Further reading

- **Kent Beck** — *Test-Driven Development by Example*.
- **Michael Feathers** — *Working Effectively with Legacy Code* — the test-seam discipline that makes untested code testable.
- **Martin Fowler** — [TestPyramid](https://martinfowler.com/bliki/TestPyramid.html), [ContractTest](https://martinfowler.com/bliki/ContractTest.html).
- **Google** — [Testing on the Toilet](https://testing.googleblog.com/) — short, sharp testing-pattern essays.
- **Forsgren, Humble, Kim** — *Accelerate* — continuous testing as a delivery-performance predictor.
- **Hamel Husain** — [evals essays](https://hamel.dev/blog/posts/evals/) — pragmatic AI evaluation patterns.
- **OpenAI** — [Evals framework](https://github.com/openai/evals); **Anthropic** — published evaluation methodology.
