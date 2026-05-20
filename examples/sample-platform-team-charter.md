# Platform Team Charter: Developer Platform

> Example charter for the Developer Platform team in the [mock 40→120 scenario](mock-q3-engineering-plan.md). Uses the [team topologies](../docs/team-topologies.md) model: this is a long-lived **platform team** that treats its output as a product consumed by stream-aligned teams.

| Field | Value |
|---|---|
| Team name | Developer Platform |
| Type | Platform (long-lived) |
| EM | `<name>` |
| Tech Lead | `<name>` |
| Director | Director, Platform & Infra |
| Headcount (target) | 8 |
| Charter date | `YYYY-MM-DD` |
| Review cadence | Quarterly |

---

## 1. Mission

> *Reduce the cognitive load of building, shipping, and operating services at our company, so that every product engineer ships faster, more safely, and more reliably.*

Our internal customers are every product engineering team. Our output is a set of paved roads — opinionated, supported, and consumed by choice.

## 2. Why we exist (the alternative we are preventing)

Without a platform team, every product team independently:
- Picks a service template (5 different ones emerge in a year)
- Wires its own CI/CD (with subtly different security postures)
- Rolls its own observability (with incompatible dashboards)
- Manages its own secrets (and rotates them at different cadences)

The result: doubled costs, halved reliability, security drift, and an onboarding time measured in weeks. The platform team's job is to make those problems invisible.

## 3. The products we own

We treat each as an internal product with a roadmap, customers, and adoption metrics.

| Product | Description | Stage |
|---|---|---|
| **Service Template** | One-command scaffold for new services (Go, TS, Python flavors) | GA |
| **Golden CI/CD Pipeline** | Build, test, security scan, deploy, with safe defaults | GA |
| **Observability-in-a-Box** | Metrics, logs, traces, dashboards, alerts wired by default | GA |
| **Secrets & Config Service** | Centralized; pull-based; rotation built-in | GA |
| **Feature Flag Service** | Internal flag platform with mandatory expiry | Beta |
| **Internal Developer Portal** | Service catalog, ownership, runbooks, dependencies | Beta |
| **Spec Registry** | Storage and CI integration for [specs](../docs/spec-driven-development.md) | Alpha |

## 4. How we work

- **Customers in the loop.** Quarterly interviews with one engineer per product team. Drive product backlog.
- **Paved road, not mandatory road.** Teams can opt out — and we treat their reasons as our product backlog.
- **Self-service first.** A new team should be able to spin up a production-ready service in < 1 hour without talking to us.
- **Docs are a deliverable.** No product launches without docs; docs broken = bug.
- **We are on-call for our platforms.** Same severity model as product services ([incident management](../docs/incident-management.md)).

## 5. How we measure success

| Metric | Target | Source |
|---|---|---|
| Platform NPS (internal) | ≥ +30 | Quarterly survey |
| % of services on golden pipeline | ≥ 90% by EOY | Service catalog |
| New-team setup time | < 1 hour | Onboarding tracker |
| New-hire time-to-first-merge | < 14 days | Onboarding tracker |
| Mean time saved per service per quarter (self-reported) | trend up | DX survey |
| Cost per service per month (vs. roll-your-own baseline) | < 50% | Finance |
| Platform on-call burden | < 1 page/night actionable | PagerDuty |

NPS, adoption, and time-to-first-merge are also on the org-level [scorecard](../docs/metrics-scorecard.md).

## 6. Interaction model

Per [team topologies](../docs/team-topologies.md):

- **Default mode with product teams:** X-as-a-Service. Self-service. Low coordination.
- **Collaboration mode** used only for: onboarding a new team, migrating off a deprecated platform, debugging a sev1.
- We deliberately *avoid* becoming a ticket queue. If we get one, the product backlog gets an item to self-serve it.

## 7. Decision rights

- Architecture *within* our products: we decide.
- Architecture *across* products that use us (e.g. service-to-service auth): proposed by us, ratified at [ARB](../docs/architecture-review-process.md).
- Vendor selection > $50k/yr: proposed by us, approved by Director.

## 8. AI in the platform

Per the [AI policy](../docs/ai-assisted-development-policy.md), the platform team owns the infrastructure that makes AI-first development safe:

- The **AI gateway** (cost, rate limit, audit, policy enforcement) — co-owned with AI Platform team.
- The **spec registry** integration with CI — specs in the repo, validated on PR.
- The **eval harness** wiring in CI — co-owned with AI Platform team.
- The **paved-road AI usage telemetry** — team-level adoption, never individual.

This is why the platform team is staffed to 8 from day one, not 4 — the AI-first stance loads work onto platform.

## 9. What we explicitly do NOT own

- Product engineering teams' services.
- Production incident response for product services (we support, we don't drive).
- Hiring decisions for product teams (we advise on platform engineering hires only).
- Cloud provider relationship management — that's Infra & SRE.

## 10. Risks we are watching

| Risk | Mitigation |
|---|---|
| Becoming a ticket queue | Strict triage; every ticket → self-service backlog item |
| Building things no one adopts | Quarterly NPS + adoption metrics; sunset what doesn't take |
| Falling behind product team needs | Product team rep rotates through our roadmap reviews |
| On-call burn from supporting too many services | Burden capped at 1 page/night; SLOs on platform services |

## 11. Sign-off

| Role | Name | Signed |
|---|---|---|
| Platform EM | | |
| Director, Platform & Infra | | |
| Head of Engineering | | |
