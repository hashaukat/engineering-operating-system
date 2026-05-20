# Developer Experience & Internal Developer Platform

> *"Make the right thing the easy thing."* — Operating principle #3.

Developer Experience (DevEx) is what every engineer feels every day: how long it takes to get from "I want to ship X" to "X is in production safely." It is the single largest determinant of an org's throughput, reliability, AI leverage, and morale.

In an AI-first world this becomes even more decisive: engineers now generate options at 10× speed, so the **friction between idea and production becomes the bottleneck**. Internal Developer Platform (IDP) and paved-road thinking is how we attack that friction systematically.

---

## The DevEx promise

A new engineer should be able to:

- **Day 1:** Get a laptop, accounts, IDE, AI assistant, and a working local dev loop without filing a single ticket.
- **Day 2:** Run the full app locally and pass the existing test suite.
- **Day 5:** Ship a small, real change to production via the paved road, with the team's review.

If any of those is impossible, we have a DevEx defect. We track and fix DevEx defects with the same seriousness as customer-facing defects.

---

## Paved roads, golden paths

The **paved road** is the supported, opinionated way to do common things. It is *not* mandatory — engineers can leave it — but leaving it is a deliberate decision with documented trade-offs.

| Category | Paved road provides |
|---|---|
| **New service** | Templated repo, CI/CD wired, observability default, deploy on green, SLO scaffolding |
| **Local dev** | One-command bootstrap, devcontainers/Nix/whatever; identical to CI environment |
| **AI assistance** | Approved tools pre-configured, prompt guides, spec→code agents, evaluator harness |
| **Auth** | Identity SDK, session library, role helpers, tested against threat model |
| **Data access** | Approved DB clients, migration tooling, query telemetry, PII tagging |
| **Async / messaging** | Standard queue patterns, retry/DLQ baked in |
| **Feature flags** | Default flag service, kill-switch convention, expiration enforcement (see [release-engineering.md](release-engineering.md)) |
| **Observability** | Logs, metrics, traces auto-emitted with service metadata; default dashboards |
| **Secrets** | Approved secrets manager, no-code-secrets pre-commit hook |
| **Compliance** | SBOM, signed artifacts, license scan, all on by default |

**The rule:** if 3+ teams need it, the platform team owns it. If <3 teams need it, the team owns it themselves until it becomes shared.

---

## The Internal Developer Platform

A self-service surface ("portal" or CLI, often both) exposing the paved roads. Minimum capabilities:

1. **Service catalog** — every service, owner, dependencies, SLOs, runbooks, on-call. Searchable. (Backstage-style.)
2. **Scaffolding** — `new service` / `new endpoint` / `new data pipeline` commands produce production-shaped scaffolds.
3. **Environments** — ephemeral preview environments per PR; one-click reset of long-lived envs.
4. **Deploy** — uniform deploy command across runtimes; progressive delivery defaults ([release-engineering.md](release-engineering.md)).
5. **Observability** — pre-wired dashboards, log search, trace viewer, error tracker per service.
6. **AI tooling surface** — approved models, prompt registry, eval harness, agent runtime, all reachable from the IDP.

The IDP is **a product** with a product manager (in the platform team), users (every engineer), and a roadmap shaped by user research, not by intuition. See [sample-platform-team-charter.md](../examples/sample-platform-team-charter.md).

---

## The "Thinnest Viable Platform" (TVP) discipline

From *Team Topologies*: the platform must be **just enough** to accelerate, never so big it becomes its own bottleneck.

- A platform feature ships only when at least one stream-aligned team needs it now and ideally a second team has expressed interest.
- Platform features that nobody uses are retired.
- Platform team measures itself on **adoption** and **time saved per stream team**, not on platform LOC or feature count.

---

## DevEx metrics — what we measure

Tracked on the [scorecard](metrics-scorecard.md), team-health and delivery lenses:

| Metric | Target |
|---|---|
| **Time to first commit** (new hire) | < 2 days |
| **Time to first production deploy** (new hire) | < 5 days |
| **Local dev bootstrap time** | < 30 minutes from clean machine |
| **PR feedback latency** (PR open → first review) | < 4 working hours, p75 |
| **CI duration** (PR pipeline, p75) | < 15 minutes |
| **Time waiting for environments** | ~0; preview envs are ephemeral and instant |
| **% of teams using paved-road defaults** | > 80% for the supported categories |
| **Friction score** from quarterly survey | trending up; ≥ DX Core 4 "Developer Experience" benchmark |
| **% of PRs with AI assistance** | tracked at *team* level only, never individual ([policy](ai-assisted-development-policy.md)) |

Note what's *not* measured: lines-of-code, individual PR counts, individual AI usage. See [productivity-measurement.md](productivity-measurement.md) for why.

---

## The DevEx feedback loop

- **Quarterly developer experience survey** — short (10 questions), comparable across quarters. Use the DX Core 4 framework as a base.
- **Friction logs** — every engineer is invited to log "I lost > 30 minutes to X." Reviewed weekly by the platform team.
- **Office hours** — platform team holds weekly drop-in for stream teams.
- **Embedded enabling missions** — platform engineers spend 1–2 weeks/quarter embedded on a stream team to feel the friction themselves.

---

## How AI changes DevEx

Several shifts the org explicitly invests in:

1. **Scaffolding is generated, not templated.** AI generates a service skeleton tuned to the spec, not a one-size-fits-all template. The paved-road parts still come from the IDP.
2. **The "first PR" is AI-drafted, human-finalized.** Onboarding is now: read the spec → ask the AI to draft → review, fix, ship. We teach the *review-and-fix* skill explicitly ([critical-thinking-with-ai.md](critical-thinking-with-ai.md)).
3. **Local-to-prod parity matters more.** AI-generated code breaks more often when the local environment differs from prod, because the AI can't see your environment. Devcontainers / Nix / equivalent become essential.
4. **Spec quality determines AI leverage.** Investments in [spec-driven development](spec-driven-development.md) and the [spec template](../templates/spec-template.md) directly raise DevEx because they raise the floor of every AI-assisted task.
5. **Eval harness is part of the platform.** Customer-facing AI features need evals as much as services need tests ([ai-feature-eval-template.md](../templates/ai-feature-eval-template.md)); the eval harness is paved-road infrastructure.

---

## Anti-patterns to name and kill

- **The platform team as ticket queue.** Stream teams file tickets; platform team services them; nobody builds product features. The platform team is a *product team* with a product, not a service desk. ([common-pitfalls.md](common-pitfalls.md) #7)
- **Mandatory paved road.** Forces stream teams off-road silently because the road doesn't fit. Paved roads are *easy-on, easy-off*; deviation is logged, not punished.
- **Platform feature wishlist without users.** Building "what we think they need." Always tie a platform investment to a named stream team and a named pain.
- **Onboarding by tribal knowledge.** "Ask Sarah; she knows." If Sarah is the documentation, the documentation has a single point of failure.
- **CI as a debugging tool.** 45-minute CI runs because nobody owns CI. CI duration is a first-class metric.
- **AI tooling sprawl.** Every team adopts a different AI assistant, gateway, eval harness. No org-level leverage, exploding cost, security holes everywhere. The IDP centralizes the AI surface.

---

## Roles

- **Platform team(s)** — own the IDP and the paved roads ([team topologies](team-topologies.md); see [sample-platform-team-charter.md](../examples/sample-platform-team-charter.md)).
- **Enabling teams** — temporarily embed to help stream teams adopt new paved-road capabilities (DevEx, AI adoption).
- **Stream-aligned teams** — consumers; expected to push back on platform gaps with friction logs.
- **Director of Platform Engineering** — accountable for org-wide DevEx metrics at the leadership team.

---

## Further reading

- **Skelton & Pais** — *Team Topologies* ([key concepts](https://teamtopologies.com/key-concepts)) — Thinnest Viable Platform, four team types.
- **Forsgren, Humble, Kim** — *Accelerate* + [DORA Research](https://dora.dev/research/) — the empirical case that developer experience predicts org performance.
- **Spotify Engineering** — [Backstage](https://backstage.io/) — the open-source IDP reference implementation.
- **CNCF Platforms Working Group** — [Platform White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/).
- **DX (getdx.com)** — [Core 4 framework](https://getdx.com/research/measuring-developer-productivity-with-the-dx-core-4/) — Developer Experience as one of four scorecard dimensions.
- **Will Larson** — [*Magnitudes of exploration*](https://lethain.com/magnitudes-of-exploration/) and adjacent essays on platform engineering trade-offs.
- **Camille Fournier** — [*Platform engineering for the rest of us*](https://skamille.medium.com/) — keeping platforms grounded in stream-team need.
