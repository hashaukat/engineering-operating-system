# The Kernel

> The irreducible core of this operating system. Everything else — docs, templates, skills, examples — composes on top of these. If any of these fails, everything above it degrades.

This document is intentionally short. Kernels are small. If it grows past one page, it has stopped being the kernel.

---

## What a kernel is, and isn't

In a real operating system the kernel is the smallest, always-running, most-privileged core. It provides the **primitives** that everything else assumes; it is **boring and stable**; it changes rarely and carefully; and when it fails, every program above it fails.

An engineering organization has a kernel too. Most orgs that struggle struggle because their kernel is implicit — present in the heads of two or three people, never written down, never taught, never enforced — so the userspace (rituals, frameworks, OKRs, tools) sits on sand.

This is ours. **Three primitives, one substrate, one scheduler.** Memorize them.

---

## The substrate: trust and psychological safety

The hardware the kernel runs on. You cannot invoke it; you build it, every day, by doing what you said you'd do and by making it safe to tell the truth. Without it, the three primitives below degrade into theater:

- writing becomes CYA,
- decisions become politics,
- inspection becomes spin.

Protect this above all. It is the slowest to build and the fastest to destroy.

---

## The three primitives

### 1. Write it down

**Specs, decisions, postmortems, status, context.** If it isn't written, it didn't happen, can't be reviewed, can't be inherited, can't be fed to AI, and can't survive the people who knew it.

- Every meaningful piece of work begins with a written spec or RFC. See [spec-driven development](docs/spec-driven-development.md) and [skills/writing-specs.md](skills/writing-specs.md).
- Every meaningful decision is recorded with rationale and alternatives. See [decision-making](docs/decision-making.md), [templates/decision-record-template.md](templates/decision-record-template.md), [templates/architecture-decision-record.md](templates/architecture-decision-record.md).
- Every incident produces a blameless postmortem. See [incident-management](docs/incident-management.md), [templates/postmortem-template.md](templates/postmortem-template.md).
- Every status update is written, dated, and searchable.

This is the primitive AI amplifies the most. An org that writes things down can use AI fluently; an org that doesn't, can't.

### 2. Decide and own it

**Every meaningful decision has a named owner, a type, a written rationale, and a reversal criterion.**

- **Owner** — one human name. Not a committee.
- **Type** — Type 1 (one-way door, careful, slow) or Type 2 (reversible, bias to action). See [decision-making.md](docs/decision-making.md).
- **Rationale** — what we believed, what we considered, what we rejected.
- **Reversal criterion** — what we'd have to see to change our mind.

Decisions without owners drift. Decisions without rationale get re-litigated forever. Decisions without reversal criteria become identity.

This is the primitive AI threatens the most: the supply of plausible-sounding options is now infinite, so the discipline of *choosing* is the scarce resource. See [skills/critical-thinking-and-judgment.md](skills/critical-thinking-and-judgment.md) and [docs/critical-thinking-with-ai.md](docs/critical-thinking-with-ai.md).

### 3. Inspect reality

**Metrics, postmortems, retros, evals, customer contact, honest status.** The system that distinguishes the organization that is operating from the organization that is telling itself stories.

- **Metrics** — DORA, SPACE, DX, AI metrics, customer value, reliability. See [productivity-measurement](docs/productivity-measurement.md), [metrics-scorecard](docs/metrics-scorecard.md).
- **Evals** — the parallel quality pyramid for AI features. See [templates/ai-feature-eval-template.md](templates/ai-feature-eval-template.md).
- **Postmortems and retros** — what actually happened, not what we wished had.
- **Customer contact** — every leader spends time directly with customers, every month.
- **Honest status** — green/yellow/red mean something; yellow is allowed; green requires evidence.

This is the primitive that AI both supercharges (anomaly detection, trace summarization) and corrupts (sycophantic summaries, confidently wrong reports). Treat AI outputs as a junior analyst: useful, often right, never trusted blind. See [skills/working-with-ai.md](skills/working-with-ai.md).

---

## The scheduler: a weekly operating cadence

The kernel's clock interrupt. A predictable loop at team, org, and leadership levels:

**Plan → Execute → Review → Learn**, every week, every quarter, every year.

- **Weekly:** team standup or written update; leader written update; 1:1s. See [skills/running-one-on-ones.md](skills/running-one-on-ones.md).
- **Quarterly:** planning, OKR setting, scorecard review. See [planning-rhythm.md](docs/planning-rhythm.md), [templates/quarterly-planning-template.md](templates/quarterly-planning-template.md).
- **Annually:** strategy, org design, ladder calibration, budget. See [engineering-strategy.md](docs/engineering-strategy.md), [org-design.md](docs/org-design.md).

The cadence is the *only* thing that turns the three primitives from documents into a living system. Skip the cadence and the primitives quietly die.

---

## Userspace (everything else)

Built on top of the kernel:

- **`docs/`** — the operating model: how strategy, org, security, quality, DX, finops, governance work. *Tuned* per org; *composes on* the kernel.
- **`templates/`** — the standard interfaces (syscalls) — spec, ADR, postmortem, 1:1, planning.
- **`skills/`** — the userland toolchain — what individuals practice.
- **`examples/`** — reference programs.

Everything in userspace is **tunable** to your stage, domain, distribution, and AI maturity. The kernel is not.

---

## How to use the kernel

- **As a diagnostic.** When something is broken in your org, ask: *which primitive failed?* Almost always it's one of the three (or the substrate beneath them).
- **As a non-negotiable.** Stage, domain, headcount, and AI tooling change. The kernel does not. If a proposed change weakens the kernel, the change is wrong.
- **As an onboarding contract.** Every new leader and engineer reads this on day one. It is shorter than the offer letter.
- **As the AI-first claim, made concrete.** AI's leverage *and* its risk both land on the kernel. Writing, deciding, inspecting are exactly what AI accelerates and exactly what it can corrupt. Strengthening the kernel is how you safely turn up AI.

---

## What's *not* in the kernel (on purpose)

These matter — they live in userspace, not the kernel — because they should vary by org, stage, and domain:

- A specific strategy.
- A specific org design or team topology.
- A specific tech stack or platform.
- A specific tool (Jira / Linear / GitHub / Notion).
- A specific AI policy or model choice.
- A specific career ladder shape.
- A specific set of OKRs.

If any of these creeps into the kernel, it has stopped being the kernel.

---

## The one-paragraph version

*Build trust. Write things down. Decide with named owners and written rationale. Inspect reality honestly. Run the weekly loop. Everything else is tuning.*
