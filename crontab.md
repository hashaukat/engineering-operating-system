# `crontab` — Scheduled Jobs for the Org

> The kernel says *run a weekly loop*. This file says *here are the specific recurring jobs that run on that loop, who owns them, what artifact they produce, and which ones an AI agent can run for you.*
>
> In Unix, `crontab` is the list of scheduled jobs the system runs without anyone re-deciding to run them. Same idea here: the org's background hygiene — the things that, if skipped, cause it to silently rot.

This file is the operational counterpart to [kernel.md](kernel.md). The kernel defines the *primitives*; the crontab defines the *jobs that exercise them on a schedule*.

---

## The agentic twist

In an AI-first world, most of these jobs are now **agent-assisted or agent-run** — drafted, gathered, summarized, flagged by agents — but the **artifact and the decision remain human-owned**. That separation is load-bearing:

- **Agent runs the job → human owns the output.** The agent prepares the weekly update from PRs, incidents, and metrics; the engineering leader edits, signs, and sends. The agent drafts the 1:1 agenda from prior notes; the manager reads and runs the meeting.
- **Agent surfaces signal → human decides.** The agent flags an SLO drift, an eval regression, a cost anomaly, a stale postmortem action item; a human decides what to do.
- **Agent never closes the loop alone on anything that creates commitment, risk, or judgment.** Performance, hiring, strategy, incidents, security exceptions, money — human-in-the-loop, always.

This is the kernel applied to automation. Writing, deciding, and inspecting get *amplified* by agents; they do not get *replaced* by agents.

The columns in the tables below are:

- **Job** — what runs.
- **Owner** — the human accountable; never an agent.
- **Cadence** — when.
- **Agent role** — what AI does in the loop today (most orgs are already here or one quarter away).
- **Artifact** — what gets written down (the kernel's primitive #1 made concrete).

---

## Daily

| Job | Owner | Cadence | Agent role | Artifact |
|---|---|---|---|---|
| Team standup or async daily update | Tech lead | Every working day | Draft summary from yesterday's PRs/commits/incidents; surface blockers | Standup notes / thread |
| On-call handoff | Outgoing on-call | Every 12–24h | Summarize open incidents, alerts, and watch-items | Handoff doc |
| Deploy & SLO health check | Release / SRE | Continuous + daily readout | Auto-detect anomalies, draft incident if SLO burn-rate exceeded | Daily reliability digest |
| AI eval suite | Quality / platform | Per release (often per merge) | Run evals, diff against baseline, flag regressions | Eval report |
| Dependency / vuln scan | Security platform | Daily | Run SCA, draft triage list with severity + suggested patch | Vuln triage queue |
| Cost anomaly check | FinOps / platform | Daily | Compare spend vs forecast; flag >X% deviations, esp. AI inference | FinOps alert |
| Agent-activity review *(new)* | Eng manager | Daily glance | Summarize what autonomous agents did in the last 24h (PRs, tickets, infra changes) | Agent activity log |

**Non-negotiable in this row:** standup/async equivalent, on-call handoff, SLO health check.

---

## Weekly

| Job | Owner | Cadence | Agent role | Artifact |
|---|---|---|---|---|
| 1:1 with each direct report | Manager | Weekly (biweekly minimum) | Pre-draft agenda from prior notes, recent PRs, goals; never attends | 1:1 notes |
| Leader written update (top 3 wins / risks / asks) | Each eng leader | Weekly | Draft from team data, PRs, metrics, prior week's update | Written update |
| Team retro or written retro | Team | Weekly or per sprint | Summarize sentiment from retros + recent incidents + survey | Retro doc + action items |
| Postmortem action-item audit | Incident commander rotation | Weekly | Scan all open AIs, flag stale ones (>2 weeks) | Stale-AI list |
| Hiring pipeline review | Hiring manager | Weekly during active loops | Summarize candidate status, flag stuck ones | Pipeline doc |
| Skip-level office hours or async Q&A | Senior leader | Weekly (rotating) | Cluster incoming questions; draft FAQ updates | Skip-level notes |
| Roadmap reality check | PM + Eng lead | Weekly | Diff plan vs actual; flag scope/timeline drift | Roadmap status |
| Security ticket triage | AppSec | Weekly | Auto-classify + assign | Triage board |

**Non-negotiable in this row:** 1:1s, leader written update, postmortem AI audit.

---

## Monthly

| Job | Owner | Cadence | Agent role | Artifact |
|---|---|---|---|---|
| Architecture council | Staff+ engineers | Monthly | Pre-read summaries; flag ADRs that conflict with prior ones | ADR decisions |
| Metrics scorecard review | Eng leadership | Monthly | Pull DORA/SPACE/DX/AI metrics; flag trend changes | Scorecard with commentary |
| AI eval drift review | Quality + AI lead | Monthly | Compare eval scores vs baseline + flag regressed prompts/models | Eval drift report |
| FinOps deep-dive | Eng + Finance | Monthly | Anomalies, top spenders, AI inference per feature/user | FinOps memo |
| Security posture review | CISO / sec lead | Monthly | Open vulns aging, mean-time-to-patch, AI-specific threats | Sec posture report |
| Team health survey | Each manager | Monthly | Summarize sentiment, surface themes, flag risks | Survey results |
| Skip-level 1:1 rotation | Senior leader | Monthly per skip | Prep brief on each engineer | Notes |
| OKR mid-quarter check | Each team | Mid-quarter | Status roll-up, flag at-risk | OKR scorecard |
| Pitfalls scan | Eng leader | Monthly | Scan against [docs/common-pitfalls.md](docs/common-pitfalls.md); flag patterns | Pitfalls memo |
| Agent governance review *(new)* | Platform / sec | Monthly | Summarize what autonomous agents have done, errors, escapes | Agent ops review |

**Non-negotiable in this row:** scorecard review, AI eval drift, security posture, team health.

---

## Quarterly

| Job | Owner | Cadence | Agent role | Artifact |
|---|---|---|---|---|
| Quarterly planning | Eng + PM leadership | Quarterly | Pre-draft from prior quarter scorecard + roadmap + customer signals | Quarterly plan |
| OKR setting & review | Each team & leader | Quarterly | Suggest OKRs from goals + prior misses; never sets them | OKRs |
| Career calibration / promo committee | Senior leadership | Quarterly | Compile evidence packets from PRs, docs, peer feedback | Calibration outcomes |
| Strategy review | CTO / VP Eng | Quarterly | Diff strategy vs reality; surface invalidated assumptions | Strategy memo |
| Org design review (spans / layers / topology) | Senior leadership | Quarterly | Surface span-of-control or layer issues from org data | Org review notes |
| AI policy + model review | AI lead + Security | Quarterly | Summarize model updates, vendor changes, new evals, incidents | Updated policy |
| Vendor / tool audit | Eng ops | Quarterly | List spend, usage, overlap, unused seats | Vendor decisions |
| Reliability & incident retrospective | SRE lead | Quarterly | Aggregate Sev1/2 themes; recurring failure modes | Reliability memo |
| Roadmap reset | Eng + PM | Quarterly | Diff what shipped vs planned; what to cut, defer, accelerate | Updated roadmap |

**Non-negotiable in this row:** quarterly planning, OKR setting, career calibration, reliability retrospective.

---

## Annually

| Job | Owner | Cadence | Agent role | Artifact |
|---|---|---|---|---|
| Strategy reset (3-horizon) | CTO / CEO | Annual | Surface inputs from customer, competitive, market, internal data | Strategy doc |
| Budget & headcount plan | CTO + Finance | Annual | Model scenarios; cost-per-engineer; AI cost trajectory | Budget |
| Compensation review / bands | CTO + People | Annual | Benchmark vs market; flag inversions | Updated bands |
| Career ladder calibration | Senior leadership | Annual | Surface inconsistencies across teams/geos | Ladder updates |
| Operating principles review | CTO | Annual | Surface where principles were ignored or contradicted | Updated principles |
| Org design review (major) | CTO / CEO | Annual | What did and didn't work this year | Org changes |
| AI-first stance review | CTO + AI lead | Annual | What's changed in capability, cost, risk, regulation | Updated stance |
| Kernel review | CTO | Annual | Surface where the kernel was bypassed | Kernel diff (rarely changes) |

**Non-negotiable in this row:** strategy reset, budget, compensation, ladder calibration.

---

## Event-driven (interrupts, not cron, but listed for completeness)

Triggered by an event rather than a clock. Same discipline: agent surfaces, human owns.

| Trigger | Job | Owner | Agent role |
|---|---|---|---|
| Sev1/Sev2 incident | Run incident; blameless postmortem within 5 business days | Incident commander | Draft timeline + contributing factors from logs/traces |
| Security incident | Activate sec response; legal + comms loop | CISO | Same |
| Major customer escalation | Escalation review | VP Eng + CS leader | Summarize history + impact |
| Significant attrition (>X% in a quarter) | Org diagnostic | Senior leadership | Surface exit-interview themes |
| Customer-facing AI feature regresses | Roll back; eval root-cause | AI feature owner | Run regression bisect |
| New regulation (e.g., AI Act, regional privacy) | Compliance impact review | Legal + Eng | Map regulation → systems |
| Acquisition / divestiture | Integration plan | VP Eng + corp dev | Surface tech-debt + cultural deltas |
| Strategy pivot | Plan revision off-cycle | CTO | Diff new plan vs in-flight commitments |

---

## How to use this crontab

- **Install it gradually.** A new leader should not turn on all of these in week one. Start with the non-negotiables in each row and add jobs as the org matures.
- **Name an owner for every job. One human.** No agent owns a job. No committee owns a job.
- **Every job produces an artifact.** No written artifact, no job. (See kernel primitive #1.)
- **Audit the crontab quarterly.** Which jobs produced value? Which produced ritual? Kill the rituals.
- **Tune cadence to org size.** Daily standups stop scaling around 8 people; weekly written updates start mattering above 20; monthly skip-levels matter above 100; ladder calibration cross-org matters above 200.

## Anti-patterns

- **Ritual without artifact.** Meeting happens; nothing is written; no one can act. Cut the meeting or add the artifact.
- **Artifact without owner.** Doc is generated weekly; no one reads it; no one decides. Assign or delete.
- **Agent runs job *and* closes loop.** Agent drafts and ships the executive update with no human in the path. Cardinal sin. Always re-attach the human at the commit point.
- **More cron, not better cron.** Adding a new ritual every time something goes wrong. The crontab gets bloated; the signal gets lost. Prefer fixing the cause over adding a job.
- **Cron jobs the leader doesn't run themselves.** If the VP Eng doesn't write the weekly update, no one else's will be honest.
- **Per-team divergence.** Every team invents its own cadence. The crontab should be standard at the org level; teams tune *within* the slots, not the slots themselves.
- **Calendar-as-strategy.** Believing that a full crontab equals a healthy org. The kernel is upstream; cron is downstream. A perfectly-run set of rituals on top of broken trust still fails.

## Relationship to the kernel

| Kernel element | Crontab manifestation |
|---|---|
| Substrate (trust / safety) | Every job is psychologically safe to do honestly (status can be red, postmortems are blameless, surveys are anonymous) |
| Primitive 1 — Write it down | Every job produces a named, durable artifact |
| Primitive 2 — Decide and own it | Every job has a named human owner; decisions made by jobs are logged |
| Primitive 3 — Inspect reality | Most cron jobs *are* inspection — metrics, evals, postmortems, surveys, audits |
| Scheduler — weekly loop | The crontab is the scheduler made explicit |

If you ever want to know what an AI-first engineering organization actually *does* day to day, this file is the answer.
