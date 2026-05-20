# `agents.md` — The Agent Registry

> The catalog of autonomous and semi-autonomous AI agents the organization runs in production. If `crontab.md` is the scheduler, this is the systemd unit file: every agent declared, scoped, owned, and governed in one place.
>
> **Rule of the registry:** if an agent is not in this file, it is not allowed to act on production systems, customer data, or shared infrastructure. No exceptions.

This file is the operational backbone of the [AI agent governance doc](docs/ai-agent-governance.md). The doc is the policy; this file is the running list.

---

## Why this exists

You cannot govern what you have not catalogued. Three years from now, every engineering org will have somewhere between 5 and 500 agents quietly acting on its behalf — opening PRs, triaging tickets, paging humans, modifying infrastructure, replying to customers, processing payments. Most of them will have been deployed by individual teams under deadline pressure, with no central record. That is exactly how outages, breaches, and runaway spend happen.

The registry is the answer. Every agent is a tracked, owned, governed unit. New agents go through a lifecycle (propose → pilot → graduate → retire). The registry is reviewed monthly. Agents that haven't run in 90 days are retired by default.

---

## The standard agent record

Every agent in the registry has, at minimum, the following fields. Copy this block when registering a new agent.

```yaml
name: <short-id>                       # e.g., release-notes-drafter
owner: <one human, named>              # Accountable. Not a team. Not an agent.
backup-owner: <one human>              # Vacation/leave coverage.
purpose: <one sentence>                # What it does. Plain English.
trust-tier: <T0|T1|T2|T3>              # See "Trust tiers" below.
scope:
  reads: [<systems / data classes>]
  writes: [<systems / data classes>]
  external-calls: [<APIs / models>]
identity: <managed identity / service account>   # Never a human's credentials.
permissions: <least-privilege list, linked to IaC>
blast-radius: <what's the worst this agent can do in a single bad run>
kill-switch: <how a human stops it in <60 seconds>; who has the button
audit-log: <where every action is recorded; retention period>
eval-suite: <link to evals + pass thresholds + run cadence>
human-in-the-loop:
  required-for: [<actions that require human approval>]
  approval-mechanism: <PR review / ticket / Slack approval / signed change>
rollout: <% of traffic / cohorts / regions>
on-call: <who pages when it misbehaves>
runbook: <link>
review-cadence: <weekly | monthly | quarterly>
last-reviewed: <date>
status: <proposed | piloting | production | deprecated | retired>
```

If a field is empty, the agent does not ship. The registry has no optional fields.

---

## Trust tiers

Agents are classified by **blast radius**, not by how impressive they are. A clever agent with a small blast radius is T1; a "simple" agent that can touch production data is T3.

| Tier | Description | Examples | Requirements |
|---|---|---|---|
| **T0** | Read-only, internal-only, no PII. | Code search, doc summarizer, internal Q&A | Owner, identity, audit log. No eval gate required. |
| **T1** | Writes only to ephemeral / non-production. | Draft PR descriptions, draft 1:1 agendas, scratchpad summaries | + Eval suite, kill switch, monthly review. |
| **T2** | Writes to production systems with human-in-the-loop on every action. | Proposed PRs (human merges), drafted customer replies (human sends), draft runbooks | + Pre-merge gate, change audit, weekly review during pilot. |
| **T3** | Writes to production systems autonomously (no per-action human approval). | Auto-remediation of known incidents, auto-rollback on SLO burn, autonomous code refactors merging on green | + Full eval gate, staged rollout, kill switch tested monthly, blameless postmortem on any unintended action, executive review quarterly. |

**Promotion is one tier at a time.** No agent jumps from T1 to T3. Every promotion requires a written case, a 30-day clean run at the prior tier, and explicit sign-off by the trust-tier owner.

**Demotion is automatic.** Any unintended action, eval regression beyond threshold, or security finding demotes the agent one tier immediately, pending review.

---

## Non-negotiables for every production agent

Regardless of tier:

- **Named human owner.** Never a team alias. Never an agent. The owner's name is in this file.
- **Managed identity.** The agent authenticates as itself, with its own credentials and audit trail. Never as a human, never with shared keys.
- **Least privilege.** Permissions enumerated; reviewed; expressed in IaC; reviewed quarterly.
- **Kill switch.** A documented mechanism that any on-call engineer can execute in under 60 seconds. Tested monthly for T2/T3.
- **Append-only audit log.** Every action the agent took, with timestamp, input, output, decision. Retained per data-governance policy.
- **Eval suite.** Pass thresholds. Run on every prompt/model/tool change. Drift report monthly.
- **Blast-radius limit.** A hard cap on what the agent can change in one run (number of files, dollar amount, customer count, infra resources). The cap is enforced in code, not policy.
- **Rollback path.** Every action the agent takes is reversible, or the action requires human approval.
- **Page-able.** When the agent misbehaves, a named on-call human gets paged.

---

## Example registry entries

Three worked examples spanning the tiers. A real org would have dozens.

### `release-notes-drafter` (T1)

```yaml
name: release-notes-drafter
owner: Priya Shah (Release Engineering Lead)
backup-owner: Marcus Wei
purpose: Draft release notes from merged PRs and linked specs for human edit before publication.
trust-tier: T1
scope:
  reads: [github-repos:product/*, specs-db:read]
  writes: [docs-staging:write]
  external-calls: [internal-llm-gateway]
identity: msi-release-notes-drafter
permissions: github:repo:read, specs-db:read, docs-staging:write (least-privilege IaC ref: infra/agents/release-notes.bicep)
blast-radius: One draft doc in staging per release. No production publish.
kill-switch: Disable the GitHub Action `release-notes-drafter.yml`; Release Eng + Platform on-call have button.
audit-log: agents-audit-log/release-notes-drafter (90-day retention)
eval-suite: evals/release-notes/ (factual-accuracy >= 0.95, no-customer-PII = 1.0, run on every prompt/model change)
human-in-the-loop:
  required-for: [publish]
  approval-mechanism: Release manager edits + clicks publish.
rollout: 100% of releases since 2026-Q1.
on-call: Release Engineering rotation
runbook: runbooks/release-notes-drafter.md
review-cadence: monthly
last-reviewed: 2026-05-01
status: production
```

### `incident-summarizer` (T2)

```yaml
name: incident-summarizer
owner: Dana Okafor (SRE Lead)
backup-owner: Hiroshi Tanaka
purpose: Draft Sev2 incident timelines and contributing-factor summaries from logs, traces, and chat for the incident commander to edit.
trust-tier: T2
scope:
  reads: [logs:read, traces:read, incident-chat:read]
  writes: [postmortem-drafts:write]
  external-calls: [internal-llm-gateway]
identity: msi-incident-summarizer
permissions: see infra/agents/incident-summarizer.bicep
blast-radius: One draft postmortem per incident. No external publication.
kill-switch: Pause via incident-bot `/pause incident-summarizer`; SRE + Security on-call have button.
audit-log: agents-audit-log/incident-summarizer (1-year retention; ties to postmortem)
eval-suite: evals/incident-summaries/ (timeline-accuracy >= 0.9, no-blame-language = 1.0, no-PII = 1.0)
human-in-the-loop:
  required-for: [publish-postmortem, action-item-assignment]
  approval-mechanism: Incident commander edits and signs.
rollout: Sev2 and Sev3 only. Sev1 still drafted by humans.
on-call: SRE rotation
runbook: runbooks/incident-summarizer.md
review-cadence: monthly
last-reviewed: 2026-05-10
status: production
```

### `slo-burn-auto-rollback` (T3)

```yaml
name: slo-burn-auto-rollback
owner: Dana Okafor (SRE Lead)
backup-owner: Anika Patel
purpose: Automatically roll back the most recent deploy when SLO error-budget burn rate exceeds 14x for >5 minutes on a tier-1 service.
trust-tier: T3
scope:
  reads: [slo-metrics:read, deploy-history:read]
  writes: [deploy-controller:rollback]
  external-calls: []
identity: msi-slo-burn-auto-rollback
permissions: deploy-controller:rollback (scoped to tier-1 services list; IaC ref)
blast-radius: One rollback per service per 30-minute window. Cannot deploy forward. Cannot touch infra.
kill-switch: Feature flag `agents.slo-burn-auto-rollback.enabled = false`; SRE + Eng leadership have button; auto-flips off after 3 rollbacks in 1h.
audit-log: agents-audit-log/slo-burn-auto-rollback (2-year retention)
eval-suite: evals/auto-rollback/ (synthetic SLO burn scenarios, false-positive-rate < 0.01, run weekly)
human-in-the-loop:
  required-for: []
  approval-mechanism: N/A (T3); blameless postmortem required on every action within 24h.
rollout: tier-1 services only; tier-2 in pilot.
on-call: SRE primary
runbook: runbooks/slo-burn-auto-rollback.md
review-cadence: weekly during pilot; monthly in production; full executive review quarterly.
last-reviewed: 2026-05-15
status: production
```

---

## The agent lifecycle

Agents move through five states. The registry tracks `status` for each.

1. **proposed** — Owner has written the YAML block and an intent doc. Reviewed in the next architecture council or AI governance review.
2. **piloting** — Approved at low rollout (one team, one service, low % traffic). Eval suite must pass before pilot. Weekly review for the duration of the pilot.
3. **production** — Promoted after a successful pilot (defined criteria: clean run, eval pass, no security findings). Standard review cadence kicks in.
4. **deprecated** — Replacement exists or scope removed. Reads-only for the deprecation window. Audit log retained.
5. **retired** — Removed from production. Identity revoked. Permissions deleted. Entry stays in registry (with `status: retired`) for historical record.

**Default retirement:** any agent in `production` that has not run in 90 days is auto-deprecated and reviewed for retirement. Dead agents are a security liability.

---

## Anti-patterns

- **Shadow agents.** Agents running in production without a registry entry. The single most dangerous anti-pattern. Detected by audit of managed identities and outbound LLM calls; offenders are killed, not negotiated with.
- **The everything agent.** One agent with broad write permissions across many systems. Split it. Blast radius scales with scope; scope should be narrow.
- **Owner-by-team.** "The platform team owns it." No. One human. Names rotate; ownership doesn't blur.
- **Eval-free production.** "It works fine in our experience" is not an eval. No eval suite, no production.
- **Kill switch that requires the owner.** If only the owner can stop the agent, the agent will run during the owner's vacation when it shouldn't. Kill switch is on-call accessible, always.
- **Permission creep.** Agent gets one more permission, then one more. Quarterly review must include "what can we take away?", not just "what should we add?"
- **Promoted on optimism.** Promoted to T3 because it "seems reliable." Promotion is evidence-based: clean eval runs, clean audit log, named promotion criteria met.
- **Audit log written by the agent.** Audit log is written by the platform, not the agent. The agent cannot edit its own record.
- **Human-in-the-loop that's actually rubber-stamping.** Reviewer approves 100 / 100 PRs from the agent without reading them. Either the agent earned promotion to T3 or the review is theater. Decide.
- **Agents that page other agents in a loop.** Infinite-loop incidents. Every agent action must terminate; loops must be detected and broken.

---

## Relationship to the kernel and crontab

| Layer | Manifestation for agents |
|---|---|
| Kernel substrate (trust / safety) | Agents that can be killed in 60s and reviewed in public earn trust; agents that can't, don't. |
| Kernel primitive 1 (write it down) | The registry *is* the writing-down. Plus every agent maintains an audit log. |
| Kernel primitive 2 (decide and own it) | Every agent has a named human owner; every T2/T3 promotion is a written decision with reversal criteria. |
| Kernel primitive 3 (inspect reality) | Every agent has an eval suite, an audit log, and a review cadence. |
| Scheduler / crontab | Most agents are *triggered* by the crontab (the eval drift report, the agent-activity review, the agent governance review) or *run* a crontab job on a human's behalf. |

The registry is the AI-first claim made operational: agents are first-class citizens of the org, governed like any other production system, with humans as the author of record at every gate.

---

## Further reading

- [docs/ai-agent-governance.md](docs/ai-agent-governance.md) — the policy underlying this registry
- [docs/ai-assisted-development-policy.md](docs/ai-assisted-development-policy.md) — the broader AI-use stance
- [docs/security-and-supply-chain.md](docs/security-and-supply-chain.md) — agent identity, secrets, supply chain
- [templates/ai-feature-eval-template.md](templates/ai-feature-eval-template.md) — the eval format every agent uses
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — threat model inputs
- [Anthropic — Responsible Scaling Policy](https://www.anthropic.com/news/anthropics-responsible-scaling-policy) — tier-based agent governance, external reference
