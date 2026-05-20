# Start Here — A New Manager's Guided Tour

> **Audience:** You're a newly-promoted engineering manager, a senior engineer about to manage, or a new EM joining a team that uses this operating system. Maybe you've managed before but never in an AI-first org. This is the guided walkthrough of how to *use* this repo.

This is the doc nobody wrote for me when I started managing. It tells you, in order, what to read, what to install, what to measure, and what to defend — week one, month one, quarter one, year one.

---

## The mental model in one paragraph

> An **Engineering Operating System (EOS)** is the explicit system around your engineers — how decisions get made, how work flows, how reliability is governed, how careers progress, how AI is adopted. Your job as a manager is not to "drive execution." Your job is to *install and maintain that system* so a team of talented humans (and increasingly, AI) compound into an organization that ships customer value faster, more reliably, more humanely than the competition.

Everything in this repo is in service of that job.

---

## Week 1 — Calibrate

### Read, in this order

1. **[README.md](../README.md)** — the 6 AI-first claims and the repo map. (10 min)
2. **[operating-principles.md](operating-principles.md)** — the 12 principles. Pick the 3 you most disagree with and write down why. You'll come back to this in 90 days. (15 min)
3. **[ai-first-stance.md](ai-first-stance.md)** — what "AI-first" actually means here. (15 min)
4. **[decision-making.md](decision-making.md)** — door types, DACI, pre-mortems, the five questions. This is the most-used framework in the whole repo. (20 min)
5. **[critical-thinking-with-ai.md](critical-thinking-with-ai.md)** — the question/verify/push-back doctrine. Required because everything you and your team produce will increasingly touch AI. (20 min)

### Do

- **Meet your team 1:1.** No agenda except: what are you working on, what's blocking you, what do you wish your previous manager had done differently. Take notes. Don't fix anything yet.
- **Read your team's last 3 postmortems** and their current quarterly plan. If neither exists, that's a finding.
- **Find your team's spec registry** (if any) and your team's decision log (if any). If neither exists, that's also a finding.

### Don't

- **Don't reorg.** Don't change the standup format. Don't kill any meeting. Don't introduce any new tool. You haven't earned the right to change anything yet.
- **Don't promise anything to skip-levels.** Listen, write down, follow up.

---

## First 30 Days — Diagnose

### Read

6. **[execution-model.md](execution-model.md)** — Intent → Discovery → Spec → Build → Ship → Operate → Learn. Map your team's actual flow against this. Where does work *actually* stall? (20 min)
7. **[spec-driven-development.md](spec-driven-development.md)** + **[spec-template.md](../templates/spec-template.md)** — the unit of work in an AI-first org. (20 min)
8. **[productivity-measurement.md](productivity-measurement.md)** + **[metrics-scorecard.md](metrics-scorecard.md)** — what to measure and how. (30 min)
9. **[incident-management.md](incident-management.md)** + **[postmortem-template.md](../templates/postmortem-template.md)** — the blameless culture you must defend from day one. (20 min)
10. **[common-pitfalls.md](common-pitfalls.md)** — score your current team against the 48 pitfalls. Anything ≥1 in three pitfalls of the same category indicates a *systemic* gap, not a one-off. This is your prioritized backlog. (30 min)

### Do

- **Run a [team-health survey](../templates/team-health-survey.md).** Quarterly cadence starting now. Share results back with the team.
- **Establish 1:1 cadence.** Weekly for direct reports, bi-weekly for skip-levels.
- **Write a "Manager README."** A one-pager: how you make decisions, how you give feedback, how you escalate, what good looks like to you, how you use AI. Share it with the team. ([operating-principles.md](operating-principles.md) and [decision-making.md](decision-making.md) are inputs.)
- **Inventory the team's AI usage.** Which tools? Which approved? Which workflows actually accelerated? Which got rubber-stamped? You're not auditing — you're learning the baseline.

### Don't

- **Don't introduce DORA dashboards yet.** Measure quietly for a quarter before publishing anything. Premature dashboards become political theater.
- **Don't do skip-level performance reviews.** You don't know enough.

---

## First Quarter — Install

By the end of your first 90 days, your team should have these in place. None of them is heavy. All of them compound.

### Rituals you install

| Cadence | Ritual | Source |
|---|---|---|
| Daily | Async written standup (replace verbal if possible) | [planning-rhythm.md](planning-rhythm.md) |
| Weekly | 1:1s with every direct report (30 min, agenda owned by them) | [operating-principles.md](operating-principles.md) |
| Weekly | Written team update (what shipped, what's stuck, what's coming) | [planning-rhythm.md](planning-rhythm.md) |
| Sprint | Sprint demo + retro | [planning-rhythm.md](planning-rhythm.md) |
| Sprint | Spec review (any spec ≥1 week of work) | [spec-driven-development.md](spec-driven-development.md) |
| Per-decision | Decision record for every Type 1 decision | [decision-making.md](decision-making.md), [decision-record-template.md](../templates/decision-record-template.md) |
| Per-incident | Blameless postmortem within 5 business days, action items tracked | [incident-management.md](incident-management.md) |
| Quarterly | Team health survey, planning cycle, postmortem-of-the-quarter review | [planning-rhythm.md](planning-rhythm.md), [team-health-survey.md](../templates/team-health-survey.md) |

### Artifacts that exist by day 90

- [ ] Team charter (mission, scope, on-call, SLOs) — see [sample-platform-team-charter.md](../examples/sample-platform-team-charter.md) for shape
- [ ] At least 3 written specs in the spec registry
- [ ] At least 1 decision record in the decision log (you'll have made one — log it)
- [ ] An on-call rotation that respects humans (no solo on-call for new engineers; documented escalation path)
- [ ] An eval harness for any AI feature your team owns ([ai-feature-eval-template.md](../templates/ai-feature-eval-template.md))
- [ ] Your team's metrics scorecard, computed monthly even if not yet published ([metrics-scorecard.md](metrics-scorecard.md))

### Read

11. **[org-design.md](org-design.md)** + **[team-topologies.md](team-topologies.md)** — your team is one of four types. Knowing which one clarifies a lot of ambiguity. (30 min)
12. **[ai-assisted-development-policy.md](ai-assisted-development-policy.md)** — the rules of the road. (15 min)
13. **[hiring-process.md](hiring-process.md)** — you will hire within 6 months. Learn the loop before you need it. (20 min)
14. **[career-ladders.md](career-ladders.md)** — promotion conversations are coming. Be ready. (30 min)

---

## First Year — Lead

You've earned the right to change things. Now do the harder work.

### Lead one full planning cycle

Use [quarterly-planning-template.md](../templates/quarterly-planning-template.md) and the [planning rhythm](planning-rhythm.md). Make your team's plan the cleanest one in the org. Two non-negotiables:

- The plan names the **customer outcome**, not just the deliverable.
- The plan reserves **explicit capacity for KTLO and incidents** (typically 20–30%). Booking 100% against features is the most common quarterly-planning mistake — see [common-pitfalls.md](common-pitfalls.md) #11.

### Run at least one calibration cycle

For performance reviews and promotions, sit in the [career ladders](career-ladders.md) calibration committee. Bring evidence, not vibes. Reward the behaviors in the ladder (especially **judgment about AI output** at IC4+), not just shipping volume.

### Hire deliberately

Use the [hiring process](hiring-process.md) end-to-end. Include the AI-allowed module *and* the AI-not-allowed module. The candidates who only shine with AI are not who you want as your senior bench in 2027.

### Publish your scorecard

By the end of your first year, your team's [metrics-scorecard.md](metrics-scorecard.md) is visible monthly to your peers and your skip. Five lenses (delivery, reliability, AI quality, customer value, team health) rolled up into three indices. Don't optimize a single metric — optimize the system that produces all of them.

### Become a teacher

Your highest-leverage activity in year two is *not* making good decisions. It is **growing the engineers who make good decisions when you're not in the room**. The [career ladder](career-ladders.md), [decision-making](decision-making.md), and [critical-thinking-with-ai](critical-thinking-with-ai.md) docs exist so the senior people on your team have a shared language for what "good" looks like. Reference them in 1:1s. Make the system visible.

---

## When you're stuck

- **"My team isn't shipping."** Start with [execution-model.md](execution-model.md). Find the *one* stage that's the bottleneck. Don't optimize everywhere at once.
- **"My team is shipping but customers aren't happier."** That's [productivity-measurement.md](productivity-measurement.md) #15 — you're optimizing delivery without outcomes. Re-anchor on the customer-value lens of the scorecard.
- **"Reliability is bad."** Read [incident-management.md](incident-management.md) and [common-pitfalls.md](common-pitfalls.md) §6. Usually it's blameful postmortems with no follow-through.
- **"AI is making things worse, not better."** Read [critical-thinking-with-ai.md](critical-thinking-with-ai.md). The pattern is almost always rubber-stamping and shrinking pushback.
- **"My most senior engineers are unhappy."** Read [career-ladders.md](career-ladders.md). Usually they have no Staff+ scope and management is the only promotion path. Use [staff-engineer-scope-template.md](../templates/staff-engineer-scope-template.md).
- **"I'm in too many meetings."** Read [planning-rhythm.md](planning-rhythm.md) and your own Manager README. Cut anything whose only output is more meetings.
- **"I don't know if I'm doing a good job."** Read [team-health-survey.md](../templates/team-health-survey.md), run it, look at trends over two quarters, and ask your skip what *they* would measure you on. Then write it down and measure it.

---

## The one habit that compounds the most

If you do nothing else from this repo, do this:

> **Write down every significant decision, the reasoning behind it, and what would change your mind. Review them quarterly.**

You will become a measurably better leader within a year. Your team will trust you more. Your successor (because every job ends) will inherit an org they can run, not a black box. And in an AI-first world where *everyone* has a brilliant co-pilot, the leaders who *think clearly in writing* will compound an advantage their competitors cannot copy.

That's the whole job. Welcome.
