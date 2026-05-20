# Spec: <Title>

> The unit of work in our [spec-driven development](../docs/spec-driven-development.md) model. Code is generated, regenerated, refactored — the spec is what we own. Keep this in the repo next to the system it describes.

| Field | Value |
|---|---|
| Spec ID | `SPEC-YYYY-NNN` |
| Status | Draft \| Accepted \| Shipped \| Superseded |
| Owner (author of record) | `<name>` |
| Reviewers | `<names>` |
| Created | `YYYY-MM-DD` |
| Last updated | `YYYY-MM-DD` |
| Size | Micro \| Feature \| System \| Product |
| Links | Discovery doc · ADRs · related specs |

---

## 1. Intent (the *what* and the *why*)

### Problem
What customer or business problem does this solve? Be specific. Cite evidence (support tickets, telemetry, customer interviews).

### Customers affected
Who feels this? How many? How often?

### Outcome we are committing to
The measurable result this change will produce. One sentence. Stated as a *change in a metric* if possible.

> Example: *"Reduce p75 checkout latency from 2.4s to <1.2s for enterprise customers, measured via RUM, within 30 days of GA."*

### Why now
Why this quarter and not next? What changes if we delay?

### Non-goals
Explicit list of what this spec is *not* doing. This is as important as the goals.

---

## 2. Technical Spec (the *how*)

### Approach
The chosen design, in 1–3 paragraphs. Diagrams welcome.

### Alternatives considered
For each: one sentence summary + one sentence on why we did not pick it. AI-generated alternatives go here too — record what we rejected and why.

### Affected systems and teams
Which services change? Which teams need to be informed or sign off?

### Data model changes
Schemas, migrations, backfills. Migration plan.

### API / contract changes
New endpoints, breaking changes, deprecations. Versioning plan.

### Dependencies
External services, libraries, vendors. License and security review needed?

### Risks
Top 3 risks and the mitigation for each.

### Rollout plan
Feature flags, canary, percentage rollout. Owners and timing.

### Rollback plan
What "undo" looks like. How long to execute.

---

## 3. Acceptance Spec (the *proof of correct*)

This is the contract. If these pass in production, the spec is shipped.

### Functional acceptance criteria
Written as testable statements:

- [ ] `<criterion>` — verified by test `<path/to/test>`
- [ ] `<criterion>` — verified by test `<path/to/test>`

### Non-functional acceptance criteria
- [ ] p75 latency on `<journey>` < `<target>`, measured by `<dashboard>`
- [ ] Error rate on `<endpoint>` < `<target>`, measured by `<dashboard>`
- [ ] SLO budget burn < `<target>` for 14 days post-GA

### Telemetry / observability requirements
What events, metrics, traces, dashboards must exist before this can be declared done.

### Eval suite (if this involves AI features)
Link to the [AI feature eval template](ai-feature-eval-template.md) instance for this feature.

### Customer-value signal
Which [customer metric](../docs/productivity-measurement.md) we expect to move. Baseline + target + measurement window.

> Example: *Baseline CSAT for checkout = 4.1; target = 4.3; measured over 30 days post-GA via in-product survey.*

---

## 4. Operational Plan

### Owners
- Build owner: `<name>`
- On-call team after launch: `<team>`
- Runbook: `<link>` (must exist before GA)

### Communication
- Internal announcement: `<channel>`, `<date>`
- Customer-facing announcement: `<owner>`, `<date>`
- Support team briefing: `<date>`

### Sunset / cleanup
- Feature flag expiration date
- Migration completion criteria
- Deprecation of replaced behavior

---

## 5. Decision log

| Date | Decision | Decider | Rationale |
|---|---|---|---|
| YYYY-MM-DD | Spec accepted | `<name>` | |
| YYYY-MM-DD | Changed `<X>` after discovery of `<Y>` | `<name>` | |

---

## 6. Post-ship review

Filled in after the measurement window.

- Acceptance criteria met? Y/N
- Customer-value signal moved as expected? Y/N — with data
- What did we learn? (1 paragraph)
- Spec changes triggered by what we learned? (link to follow-up spec if any)

---

## AI usage on this spec

- Sections drafted with AI assistance: `<list>`
- Tools used: `<list>`
- Reviewer who validated AI-drafted sections: `<name>`

This is required by the [AI policy](../docs/ai-assisted-development-policy.md). It builds organizational memory about where AI helps and where it misleads.
