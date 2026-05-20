# `operating-manual.md` — Installing This OS

> The boot sequence. If you are a new VP of Engineering, Head of Engineering, or CTO inheriting an organization and you want to install this operating system, this is the order to do it in. If you are a founder building from scratch, the order is the same — you just hit each step earlier and at smaller scale.
>
> The rest of the repo is the reference manual. This file is the install guide.

---

## Read this first

This OS is **domain-agnostic** and **stage-agnostic** in structure, but the install pace varies. A 15-person org installs the kernel in week one and the rest over a quarter. A 500-person org installs the kernel in week one and takes a year to fully retrofit the rest. The kernel is always non-negotiable.

The two unshakeable rules of installation:

1. **Install the kernel first.** Trust + write-it-down + decide-and-own + inspect-reality + the weekly loop. Without these, every later step is decoration.
2. **Install in public.** Don't roll out the OS by surprise memo. Explain what you're doing, why, what changes, what doesn't. People follow operators who narrate their reasoning.

---

## Phase 0 — Diagnose (Week 1)

Before you change anything, see what's actually there. Your first commitment is to inspect reality (kernel primitive #3) about the org itself.

**Do:**
- Read the last 12 weeks of: incident reports, postmortems, planning docs, eng all-hands decks, OKR reviews, exit interviews, customer-escalation threads.
- Hold 1:1s with every direct report. One question matters: *"What's working, what's broken, what would you change if you were me?"* Listen. Don't pitch the OS.
- Skip-level 1:1s with a sample across levels, tenure, and teams. Same question.
- Pull metrics: DORA (or whatever exists), reliability, hiring funnel, attrition, AI tool adoption, cost.
- Map the existing crontab: what meetings happen, who runs them, what artifacts do they produce. Most orgs cannot answer this. That itself is a finding.
- Map the existing agents: every script, bot, GitHub Action, autonomous pipeline. Most orgs cannot answer this either. Bigger finding.
- Read [docs/common-pitfalls.md](docs/common-pitfalls.md) with the org in mind. Mark which pitfalls are live.

**Do not:**
- Announce a strategy.
- Reorg.
- Cancel meetings.
- Add meetings.
- Promise outcomes.

**Output:** a private one-page diagnosis. Three things working, three things broken, three things you don't yet understand. Share with your boss; not yet with the org.

---

## Phase 1 — Install the kernel (Weeks 2–4)

The kernel is the only thing you install fast. Everything else is staged.

**Do:**
- Publish or adopt [kernel.md](kernel.md). One page. Send to the org with a short note: *"This is how we will operate. The rest of our system composes on this."*
- Stand up the **weekly written update** for yourself, top-down. Three sections: wins, risks, asks. Same format every week. You go first. Within four weeks, every leader two levels down does the same.
- Stand up **weekly 1:1s** with every direct report. Standing agenda template from [skills/running-one-on-ones.md](skills/running-one-on-ones.md). No skipping. Reschedule, don't cancel.
- Adopt the **decision protocol** from [docs/decision-making.md](docs/decision-making.md). From day one, every meaningful decision you make has a named owner, type, rationale, reversal criterion, written down. Model it for the org.
- Hold the **first blameless postmortem** for any incident in the window, using [templates/postmortem-template.md](templates/postmortem-template.md). Run it yourself if you have to. The first one sets the cultural norm forever.
- Name **one psychological-safety move**. Often: take an honest miss publicly. "We said X; we didn't deliver; here's why; here's what we're changing." Costs you nothing real and buys years of credibility.

**Do not:**
- Touch org structure yet.
- Adopt new tools.
- Roll out OKRs from scratch.
- Deploy new agents.

**Output:** the kernel is live and visible. Weekly cadence is running. The org has seen you write a decision down, run a postmortem, and tell the truth in public.

---

## Phase 2 — Install the crontab (Weeks 5–8)

Now the recurring jobs that exercise the kernel.

**Do:**
- Adopt [crontab.md](crontab.md). Walk through it with your leadership team. For each non-negotiable job: is it running? who owns it? what artifact does it produce? Fix the gaps.
- Install the **monthly metrics scorecard review**. Use [docs/metrics-scorecard.md](docs/metrics-scorecard.md). Even if metrics are bad — *especially* if metrics are bad — make the review happen on schedule.
- Install the **postmortem action-item audit** (weekly). Most orgs have a graveyard of action items from old postmortems no one closed. Fix that pattern publicly.
- Install **monthly skip-levels** on rotation.
- Pick a **planning rhythm** from [docs/planning-rhythm.md](docs/planning-rhythm.md). Don't redesign it. Adopt it. If quarterly already runs, keep it; just tighten the template.
- Audit existing meetings: kill at least 20%. Add at most 1. The crontab is meant to shrink rituals to the ones that produce artifacts.

**Output:** the org runs a predictable weekly/monthly/quarterly loop. Meeting count is down. Artifact count is up.

---

## Phase 3 — Inventory and govern the agents (Weeks 6–10, parallel)

Run this in parallel with Phase 2. It is urgent and almost always neglected.

**Do:**
- Open [agents.md](agents.md). Start the registry.
- Inventory every agent in production: AI assistants, autonomous scripts, GitHub Actions that take action, bots, pipelines, anything calling an LLM that writes anywhere. Most orgs find 3–10x more than they expected.
- For each: assign trust tier, owner, kill switch, audit log. Anything without all four is **paused** until it has all four. No exceptions.
- Publish the [AI policy](docs/ai-assisted-development-policy.md) and the [agent governance doc](docs/ai-agent-governance.md). Lightweight; not 40 pages.
- Stand up **monthly agent ops review** (already in the crontab).
- Stand up **AI eval drift review** (monthly). Use [templates/ai-feature-eval-template.md](templates/ai-feature-eval-template.md).

**Do not:**
- Ban AI use. You cannot, and you should not.
- Slow shipping in the name of governance. Build the registry and the evals; let teams keep moving.

**Output:** every production agent is named, owned, evaluated, and killable. The org knows what its agents do.

---

## Phase 4 — Tune the userspace (Weeks 8–16)

Now adopt the rest of the docs, *tuned* to your stage and domain. Pick the order based on your diagnosis (Phase 0).

**Common starting tunes:**

- **Reliability is the pain point** → [docs/incident-management.md](docs/incident-management.md), [docs/release-engineering.md](docs/release-engineering.md), [docs/quality-engineering.md](docs/quality-engineering.md).
- **Velocity is the pain point** → [docs/spec-driven-development.md](docs/spec-driven-development.md), [docs/developer-experience.md](docs/developer-experience.md), [docs/execution-model.md](docs/execution-model.md).
- **Scaling people is the pain point** → [docs/org-design.md](docs/org-design.md), [docs/team-topologies.md](docs/team-topologies.md), [docs/hiring-process.md](docs/hiring-process.md), [docs/career-ladders.md](docs/career-ladders.md).
- **Cost is the pain point** → [docs/engineering-finops.md](docs/engineering-finops.md).
- **Security or compliance is the pain point** → [docs/security-and-supply-chain.md](docs/security-and-supply-chain.md), [docs/data-and-privacy-governance.md](docs/data-and-privacy-governance.md).
- **AI quality / safety is the pain point** → [docs/critical-thinking-with-ai.md](docs/critical-thinking-with-ai.md), [agents.md](agents.md), eval coverage.

Adopt one or two areas per month. Each adoption is itself a decision (kernel primitive #2): write it down, name the owner, set reversal criteria.

**Output:** the operating model is in place across the areas that matter most. The areas that don't matter yet, you've consciously deferred.

---

## Phase 5 — Stand up the skills library (Months 3–6)

The OS lives in people's hands. Now build the muscle.

**Do:**
- Publish [skills/](skills/README.md). Make the foundational four required reading for every engineer, every manager:
  - [skills/critical-thinking-and-judgment.md](skills/critical-thinking-and-judgment.md)
  - [skills/working-with-ai.md](skills/working-with-ai.md)
  - [skills/technical-writing.md](skills/technical-writing.md)
  - [skills/giving-and-receiving-feedback.md](skills/giving-and-receiving-feedback.md)
- Assign engineering-craft skills by role; management skills by level; leadership skills to staff+ and managers.
- Tie skills to the [career ladders](docs/career-ladders.md): expected proficiency by level.
- Pick **one skill per team per quarter** to focus on. Practice, drills, retro.
- For new hires, week-1 reading list: [kernel.md](kernel.md), [crontab.md](crontab.md), [skills/critical-thinking-and-judgment.md](skills/critical-thinking-and-judgment.md), [skills/working-with-ai.md](skills/working-with-ai.md).

**Output:** the OS is not just on paper; people are practicing it.

---

## Phase 6 — Strategy and org design (Months 4–9)

You earned the right to touch these by running the prior phases well. Now do them.

**Do:**
- Publish a [one-page strategy](templates/one-page-strategy-template.md) using [docs/engineering-strategy.md](docs/engineering-strategy.md).
- Validate [org design](docs/org-design.md) and [team topologies](docs/team-topologies.md). Reorg only where it clearly unblocks the strategy; never as a substitute for management.
- Run the next quarterly planning using [templates/quarterly-planning-template.md](templates/quarterly-planning-template.md).
- Calibrate [career ladders](docs/career-ladders.md) across the org. Promo committee runs.
- Run a first end-to-end **mock scenario** through the system — use [examples/mock-q3-engineering-plan.md](examples/mock-q3-engineering-plan.md) as the shape.

**Output:** the strategy is on paper, the org is shaped to deliver it, the planning cadence is live, ladders are consistent.

---

## Phase 7 — Compounding (Months 9+)

Past month nine, the work is no longer install; it's compounding.

**Do:**
- Quarterly: run the crontab's quarterly slot end-to-end (planning, scorecard, calibration, strategy review, reliability retrospective).
- Quarterly: review the kernel. Did anything bypass it? Why? Fix the cause, not the symptom.
- Monthly: kill at least one ritual or one agent that's not earning its keep.
- Monthly: ship one improvement to the skills library based on what the org actually needs.
- Annually: full [annual cron pass](crontab.md#annually) — strategy, budget, comp, ladders, principles, kernel.

---

## Signs the install is working

- People quote the kernel back to you without prompting.
- Postmortems describe what happened, not who failed.
- Decisions get re-found in the decision log instead of re-litigated.
- The org's calendar has less on it than it did six months ago, and ships more.
- Engineers and managers can articulate which agents run in their stack and who owns them.
- "I don't know — let me find out" is a normal answer at every level, including yours.
- The board sees the same scorecard you see; nothing is dressed up.

## Signs the install is failing

- The kernel is on the wiki; the org operates as if it isn't.
- Weekly updates are skipped under deadline pressure.
- Postmortems are blameless on paper, blameful in person.
- New rituals are added; old ones never die.
- Agents proliferate; the registry doesn't.
- Your written updates are AI-drafted and feel like it.
- You are exhausted. The OS is supposed to make leadership *less* exhausting because the system carries the load. If it isn't, you are over-doing it or under-trusting it.

---

## A note on AI through the install

At every phase, AI is in the default path:

- **Phase 0:** agents can summarize 12 weeks of incidents, postmortems, OKR reviews to accelerate your read-in.
- **Phase 1:** agents can draft weekly updates, 1:1 agendas, and postmortem timelines. You edit and sign.
- **Phase 2:** agents can flag stale postmortem action items, scorecard anomalies.
- **Phase 3:** ironically, agents help you find your other agents (audit identities, outbound LLM calls).
- **Phase 4–7:** the operating system increasingly runs on agents as background workers, with humans owning the outputs and the decisions.

**The discipline never changes:** agent runs the job, human owns the artifact. The kernel applies to your own leadership work as much as anyone else's.

---

## Further reading

- [kernel.md](kernel.md) — the core
- [crontab.md](crontab.md) — the schedule
- [agents.md](agents.md) — the agent registry
- [docs/start-here-for-new-managers.md](docs/start-here-for-new-managers.md) — the same idea zoomed in for a new manager, not a new VP
- [docs/common-pitfalls.md](docs/common-pitfalls.md) — what to watch for during install
- [examples/mock-q3-engineering-plan.md](examples/mock-q3-engineering-plan.md) — the install applied to a 40→120 scaling story
