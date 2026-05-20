# AI Feature Eval Suite: <Feature Name>

> Every customer-facing AI feature has an eval suite *before* it ships and a continuous eval pipeline *after*. This is the working artifact. Referenced from the [AI policy](../docs/ai-assisted-development-policy.md) and the [spec template](spec-template.md).

| Field | Value |
|---|---|
| Feature | `<name>` |
| Spec | Link to [SPEC-YYYY-NNN](spec-template.md) |
| Owner | `<name>` |
| Model(s) | `<provider/model/version>` |
| Prompt template version | `<git sha or registry ref>` |
| Last reviewed | `YYYY-MM-DD` |

---

## 1. What this feature is supposed to do

One paragraph in plain language. The same description the customer would read. This grounds every eval that follows.

## 2. What "good" looks like (rubric)

Define quality dimensions and the scoring scale. Be specific — vague rubrics produce vague evals.

| Dimension | Definition | Scale | Pass threshold |
|---|---|---|---|
| Correctness | Output factually matches ground truth | 0–1 | ≥ 0.95 |
| Relevance | Output addresses the user's actual ask | 1–5 | ≥ 4 |
| Safety | No policy violations, no harmful content | binary | 100% pass |
| Tone | Matches our product voice | 1–5 | ≥ 4 |
| Latency | p75 response time | seconds | < 2s |
| Cost | $ per successful interaction | $ | < `<target>` |

## 3. Offline benchmark — the regression set

A curated set of input/expected-output pairs. Versioned in the repo.

- Location: `<path/to/eval/set>`
- Size: `<N>` examples
- Coverage: list the scenarios this set must cover (happy path, edge cases, failure modes, adversarial inputs)
- How to add to it: every production incident produces ≥ 1 new eval case

**Pass criteria for a change to ship:**
- Composite score ≥ `<threshold>`
- No regression on safety
- No regression > 5% on any individual dimension

## 4. LLM-as-judge — quality at scale

A nightly sample of production interactions judged by an LLM against the rubric.

- Sample size: `<N>` per day
- Judge model: `<model>` (different from production model)
- Threshold: composite score ≥ `<threshold>`
- Drift alert: if score drops > `<delta>` in 7-day window → page owner

## 5. Human review — ground truth

A weekly human review of a sampled subset (calibrates the LLM judge and catches things the judge misses).

- Sample size: `<N>` per week
- Reviewers: `<list>`
- Calibration check: human vs LLM-judge agreement ≥ `<threshold>`

## 6. Safety / red-team evals

Adversarial inputs designed to break the feature. Run pre-launch and quarterly.

- Categories: prompt injection, jailbreaks, PII leakage, harmful content generation, off-topic abuse
- Pass criteria: 100% safe responses (refusal, safe completion, or escalation)
- Owner: Security Engineering + feature owner

## 7. Production telemetry (post-launch)

What we measure in production, not just in evals.

| Signal | Target | Dashboard |
|---|---|---|
| User acceptance rate (kept / suggested) | ≥ `<target>` | `<link>` |
| In-product "was this helpful?" thumbs-up rate | ≥ `<target>` | `<link>` |
| Hallucination/wrongness rate (from sample reviews) | < 2% | `<link>` |
| Cost per successful interaction | within `<budget>` | `<link>` |
| p75 latency | < `<target>` | `<link>` |
| Safety incidents (flagged outputs) | 0 reaching customer | `<link>` |

## 8. Rollback criteria

This feature is rolled back (flag flipped) if any of these are true:

- Safety incident reaches a customer
- User acceptance rate drops below `<threshold>` for > 24h
- Cost per interaction exceeds `<threshold>` for > 24h
- p75 latency exceeds `<threshold>` for > 1h on critical path

The on-call team has the authority to flip the flag without escalation.

## 9. Change log

Every model swap, prompt edit, or eval-set change is recorded here.

| Date | Change | Owner | Pre-change score | Post-change score |
|---|---|---|---|---|

## 10. Ownership

- Primary owner: `<name>`
- Backup owner: `<name>`
- Review cadence: monthly during first quarter post-launch; quarterly thereafter
- Sunset criteria: when this feature is removed, archive the eval set and link to its retirement decision
