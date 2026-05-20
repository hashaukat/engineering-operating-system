# Sample Spec: Checkout Idempotency (SPEC-2026-014)

> A worked example of a [spec-driven](../docs/spec-driven-development.md) feature using the [spec template](../templates/spec-template.md). This is what a "micro" spec looks like in practice for a real, customer-impacting fix.

| Field | Value |
|---|---|
| Spec ID | SPEC-2026-014 |
| Status | **Accepted** (2026-04-08) |
| Owner | Priya Shah (Tech Lead, Enterprise team) |
| Reviewers | A. Chen (Staff), R. Ortiz (SRE), J. Park (PM) |
| Created | 2026-04-03 |
| Last updated | 2026-04-08 |
| Size | **Micro** (~1 sprint) |
| Links | Discovery doc · ADR-091 (idempotency key strategy) |

---

## 1. Intent

### Problem
Enterprise customers occasionally see **duplicate charges** when our checkout retry logic fires during transient payment-provider timeouts. Evidence:

- 14 support tickets in Q1 2026 tagged "duplicate charge" (up from 6 in Q4 2025).
- 3 of those required manual refunds and an apology call from CS leadership.
- Telemetry shows our retry path fires ~0.3% of checkouts; in ~4% of those, the upstream call had actually succeeded.

### Customers affected
All paying customers, but the impact concentrates on enterprise (higher transaction values → bigger blast radius per duplicate).

### Outcome we are committing to
> *Eliminate duplicate-charge incidents caused by our retry path within 30 days of GA, measured by tickets tagged "duplicate charge" attributable to retry (target: 0 per month, baseline: 4–5).*

### Why now
Two enterprise renewals in Q2 cited this in their procurement reviews. CS bandwidth on manual refunds is at a tipping point.

### Non-goals
- Not redesigning the checkout flow.
- Not changing payment providers.
- Not adding idempotency to non-checkout retry paths in this spec (a follow-up spec will).

---

## 2. Technical Spec

### Approach
Add an **idempotency key** to every checkout request to our payment provider, generated client-side at the moment of *intent* (not retry). Provider supports `Idempotency-Key` header natively (per ADR-091). Our checkout service stores the key keyed on (customer_id, cart_hash, attempt_window) for 24 hours in Redis. Retries reuse the same key.

### Alternatives considered

- **A: Idempotency key strategy (chosen).** Simple, provider-native, low blast radius.
- **B: Distributed lock per cart.** Higher complexity, risk of deadlock on retry, doesn't solve the problem if the lock times out.
- **C: Async checkout via outbox pattern.** Correct long-term, but a multi-quarter change. We choose to take A now and consider C in a future architectural roadmap.
- **D (AI-generated): Optimistic concurrency on the cart record.** Rejected — does not address the retry-with-stale-state failure mode.

### Affected systems and teams
- `checkout-service` (this team owns)
- `payments-gateway` (this team owns)
- Redis cluster (Infra & SRE — informed, no changes required)

### Data model changes
- New Redis key namespace `checkout:idem:{customer_id}:{cart_hash}`, TTL 24h.
- No relational schema change.

### API / contract changes
- Internal `POST /checkout` adds optional `idempotency_key` header. If absent, server generates one and returns it in response (for client-side retry).
- No breaking change for existing clients.

### Dependencies
- None new.

### Risks
| Risk | Mitigation |
|---|---|
| Redis outage causes idempotency keys to be lost mid-checkout | Graceful degradation: fall back to current behavior + log; SRE paged if degradation rate > 0.1% |
| Key collisions between simultaneous cart updates | Cart hash includes line-item hashes + timestamp bucket; collision probability < 10⁻¹² over 24h window |
| Provider behavior under repeated identical key not as documented | Pre-launch contract test against provider sandbox + 1% canary in prod for 48h |

### Rollout plan
1. Behind feature flag `checkout_idempotency`, default off.
2. Internal dogfood: 100% of test accounts, 24h.
3. Canary: 1% of traffic, 48h. Monitor duplicate-charge ticket rate, payment provider error rate, p75 latency.
4. Ramp: 10% → 50% → 100% over 72h, with halt criteria.
5. Flag removal after 30 days at 100%.

### Rollback plan
Flip flag off. Effective in < 60s. No data migration required (Redis keys self-expire).

---

## 3. Acceptance Spec

### Functional acceptance criteria
- [x] Two concurrent identical checkout requests result in exactly one charge — verified by `tests/checkout/idempotency_concurrent.spec.ts`
- [x] Retry of a previously-succeeded checkout returns the original response, does not re-charge — `tests/checkout/idempotency_retry_success.spec.ts`
- [x] Retry of a previously-failed checkout proceeds normally — `tests/checkout/idempotency_retry_failure.spec.ts`
- [x] Client without idempotency key gets one in response, can retry safely — `tests/checkout/idempotency_server_generated.spec.ts`
- [x] Redis outage causes graceful degradation, not checkout failure — `tests/checkout/idempotency_redis_down.spec.ts`

### Non-functional acceptance criteria
- [x] p75 checkout latency increase ≤ 30ms (measured via RUM)
- [x] No regression on checkout success rate (28-day moving avg)
- [x] SLO attainment on `/checkout` endpoint remains ≥ 99.95% in 14-day post-GA window

### Telemetry / observability requirements
- Counter: `checkout.idempotency.key_reused` (segmented by reason: retry / duplicate-submit / concurrent)
- Counter: `checkout.idempotency.redis_unavailable` (alerts > 0.1% over 5 min)
- Dashboard: `Checkout / Idempotency` (added to on-call's standard view)
- Runbook entry: `runbooks/checkout-idempotency.md`

### Eval suite
N/A — not an AI feature.

### Customer-value signal
- **Primary:** support tickets tagged "duplicate charge" attributable to retry. Baseline: 4–5/month. Target: 0/month. Measured 30d post-GA.
- **Secondary:** enterprise CSAT for billing-related interactions. Baseline: 4.0/5. Target: ≥ 4.3/5. Measured 90d post-GA.

---

## 4. Operational Plan

### Owners
- Build owner: Priya Shah
- On-call team after launch: Enterprise team
- Runbook: `runbooks/checkout-idempotency.md` (must exist before canary)

### Communication
- Internal announcement: #engineering, day of GA
- Customer-facing announcement: None (internal fix; CS notified)
- Support team briefing: 1 week before GA, includes runbook for legacy duplicate-charge tickets

### Sunset / cleanup
- Feature flag `checkout_idempotency` — expires 2026-06-01 (60d post-GA)
- No deprecated behavior to remove

---

## 5. Decision log

| Date | Decision | Decider | Rationale |
|---|---|---|---|
| 2026-04-03 | Spec drafted (AI-assisted in sections 2, 3) | Priya Shah | — |
| 2026-04-05 | Chose Option A over C (async outbox) | A. Chen (Staff) | Time-to-impact; outbox to be considered in Q3 architecture roadmap |
| 2026-04-08 | Spec accepted | Priya Shah | Reviewers signed; canary starts 2026-04-15 |
| 2026-04-22 | Canary metrics within bounds; ramping to 100% | R. Ortiz (SRE) | Duplicate-charge rate dropped to 0 in canary cohort |

---

## 6. Post-ship review (filled 2026-05-22, 30 days post-GA)

- **Acceptance criteria met?** Yes — all 8 criteria pass; SLO attainment 99.97% in window.
- **Customer-value signal moved as expected?** Yes — 0 duplicate-charge tickets attributable to retry in 30d window (baseline: 4–5/month). CSAT signal too early; will re-check at 90d.
- **What did we learn?** The "Redis unavailable" graceful-degradation path activated 3 times during a brief cluster failover and behaved as designed. Without the spec's explicit acceptance criterion for this case, the fallback path would not have been built — and we would have shipped a worse outage. **The spec was the design.**
- **Spec changes triggered by what we learned?** None. SPEC-2026-027 (idempotency for refund path) opened as a follow-up.

---

## 7. AI usage on this spec

- **Sections drafted with AI assistance:** Section 2 (Alternatives — including the rejected Option D), Section 3 (functional acceptance criteria first pass), Section 6 (post-ship review timeline reconstruction from logs).
- **Tools used:** Copilot in IDE for test scaffolding; chat tool for alternatives generation.
- **Reviewer who validated AI-drafted sections:** A. Chen (Staff Engineer).
- **What we learned about AI usage:** the AI-generated Option D was usefully wrong — surfacing it forced the team to explicitly articulate why optimistic concurrency does *not* solve this problem, which strengthened the chosen design's rationale. The post-ship timeline draft saved ~2 hours of log spelunking.

This entry is required per the [AI policy](../docs/ai-assisted-development-policy.md) and builds organizational memory about where AI helps and where it misleads.
