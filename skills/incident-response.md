# Incident Response

> An incident is a learning opportunity that happens to be on fire. The org that runs incidents calmly, communicates clearly, and converts each one into systemic improvement compounds reliability. The org that runs them as theater repeats them.

This is the personal-skill companion to [incident-management.md](../docs/incident-management.md) and the [postmortem-template.md](../templates/postmortem-template.md).

---

## Purpose

You can act calmly and effectively when production is broken — as a responder, a commander, a comms lead, or a bystander — making the right calls about mitigation, communication, and escalation under time pressure, and converting the event into durable improvements once it's over.

---

## Why it matters in an AI-first org

- **More automation, bigger blast radius.** AI-driven changes and agents can fail at machine speed and scale. The incident skill is no longer just for SREs.
- **Incidents are public faster.** Status pages, Twitter, customer Slacks. Comms craft is operational, not optional.
- **The work is collaborative under stress.** Bad responder behavior costs minutes of MTTR and weeks of trust.

---

## The practice

### Before any incident — preparation

- **Know the on-call runbook for your services.** Reading it during the incident is a process failure.
- **Know the comms protocol** — channels, severity definitions, who declares, who paging customers ([incident-management.md](../docs/incident-management.md)).
- **Practice.** GameDays, chaos exercises, tabletop scenarios. The skill atrophies without reps.
- **Make sure rollback paths are tested** ([release-engineering.md](../docs/release-engineering.md)). Untested rollback is wishful thinking.

### The first minutes (any role)

- **Confirm impact, set severity.** Who's affected, what's broken, how bad. Don't guess; query the dashboards.
- **Declare the incident in the standard channel.** Names the event; brings responders; starts the clock and the timeline.
- **Identify roles immediately.** Incident Commander (IC), Comms Lead, Subject Matter Experts (SMEs), Scribe. Even informally — "Maya, you commander; Raj, you comms; I'll dig into the DB." Avoids two people doing the same thing and zero people doing the missing one.
- **Mitigate before you diagnose.** Rollback, failover, flag-off, traffic shift. Stop the bleeding; root-cause after.
- **Communicate early, even with little.** "We're aware, investigating, will update in 15." Silence is worse than incomplete information.

### During the incident — as a responder

- **One thing at a time.** Multiple parallel changes during an incident make root cause unknowable. Coordinate through the IC.
- **Say what you're about to do, then do it.** "I'm going to roll back deploy 472." The IC and the channel need a coherent picture.
- **Use the timeline.** Every observation, decision, action — timestamped in the incident channel. The scribe consolidates; everyone contributes.
- **Don't quietly try things.** A silent fix attempt that fails will be the unknown variable in the postmortem.
- **Ask for help early.** A second responder, a more senior eng, a SME from another team. There is no medal for solo-incident heroics.

### During the incident — as Incident Commander

- **You are not the deepest expert; you are the conductor.** Your job is decisions, prioritization, comms, and escalation — not solving the problem hands-on.
- **Run short, structured huddles** (every 15–30 min): "What do we know? What are we trying? Who's doing what? When do we re-sync?"
- **Make calls.** "We're rolling back, not forward-fixing." "We're escalating to Sev1." The team needs decisions, not consensus-seeking.
- **Protect the responders' focus.** Funnel exec and customer questions to the comms lead.
- **Know when to escalate.** When a Sev2 is dragging > 2h with no progress, when customer impact is growing, when responders are exhausted — bring in more humans or a more senior commander.

### During the incident — as Comms Lead

- **Templates beat improvisation.** Pre-baked status-page templates, customer-comms templates, exec-update templates. Fill in, send.
- **Cadence matters.** Even "no new info" updates on the agreed cadence are reassuring.
- **Plain language. No jargon.** Customers and execs need to know what's happening, what you're doing, when next update.
- **Internal updates differ from external.** Internal: detail, hypotheses, blockers. External: impact, mitigation, ETA, next update.

### After mitigation — the handoff

- **"Mitigated" is not "resolved."** Service is back; root cause may still be open. Be explicit about which state you're in.
- **Schedule the postmortem before everyone disperses.** Within 5 business days; sooner is better.
- **Preserve evidence.** Logs, dashboards, configs, the incident channel. Don't let them roll off retention.

### After mitigation — the postmortem

See the [postmortem template](../templates/postmortem-template.md) and [Google SRE postmortem culture](https://sre.google/sre-book/postmortem-culture/). Personal-skill highlights:

- **Blameless, not blame-free.** Name what happened and who did what; do not name *who's at fault*. The system is what's reviewed.
- **Multiple contributing causes.** "Root cause" is usually a misnomer; complex failures have several. Name them all.
- **Action items are real work**, on real backlogs, with real owners and dates. Postmortems with no follow-through are theater.
- **Share the postmortem widely.** Other teams learn from your incident. Hoarded postmortems waste the learning.

---

## Drills

- **Quarterly — GameDay.** Practice a real failure (kill a service, simulate a region outage, inject latency). Rehearse roles.
- **Monthly — read a public postmortem.** Cloudflare, GitHub, AWS, Datadog publish detailed ones. Each is a free masterclass.
- **Monthly — tabletop.** Walk through a hypothetical incident: "Our auth provider returns 500s for 40% of requests. Go." 30 minutes; high learning.
- **Before on-call shift:** read the runbook for your services. Confirm you have access to dashboards, paging, and rollback.
- **After each incident you're in:** write a one-paragraph personal retro. What did you do well? What would you do differently?
- **With your manager:** ask to shadow as IC, then run a low-Sev incident as IC under their watch. The role is learnable; nobody is born commander.

---

## Common failure modes

- **Diagnosing before mitigating.** Heroically root-causing while users are suffering. Stop the bleeding first.
- **Multiple uncoordinated fixers.** Three people quietly trying three different things. Now nobody can tell which one helped or hurt.
- **No IC.** Everyone responds; nobody is in charge. Decisions don't get made; comms don't get sent.
- **Silent incident.** No status page, no customer notification, hope nobody notices. They notice, and the trust loss exceeds the incident itself.
- **Hero culture.** One person stays up 18 hours and "saves" the incident. The system that *requires* that hero is the problem.
- **Postmortem-as-theater.** Read once, action items never assigned or completed. The next incident is identical.
- **Blame.** Names a person as cause. Future incidents get hidden, not learned from. The single most expensive cultural failure in ops.
- **Skipping postmortem for "small" incidents.** Small incidents are leading indicators. Skipping them is how you accumulate near-misses until the big one.
- **AI-feature incidents treated as "the model misbehaved."** The system that deployed the model without a kill switch, evals, or rollback is the issue. See [ai-agent-governance.md](../docs/ai-agent-governance.md).

---

## Tune for your context

- **Smaller orgs:** roles consolidate (one person may be IC + comms + responder). The *roles* still exist as a mental model; recognize when you need to ask for help to split them.
- **Highly regulated:** comms, evidence preservation, and notification SLAs become legally meaningful. Templates and runbooks tighten.
- **24/7 services:** follow-the-sun on-call; handoff hygiene becomes a skill of its own.
- **Customer-impacting AI features:** add kill-switch use to the first-minutes runbook; treat output-quality regressions as Sev-class incidents.

---

## Further reading

- **Google SRE Book** — [Incident Management](https://sre.google/sre-book/managing-incidents/) and [Postmortem Culture](https://sre.google/sre-book/postmortem-culture/) — the canonical references.
- **PagerDuty** — [Incident Response Documentation](https://response.pagerduty.com/) — practical, role-based, open-source.
- **Charity Majors** — [charity.wtf](https://charity.wtf/) — observability and ops culture writing.
- **John Allspaw** — *[Each necessary, but only jointly sufficient](https://www.kitchensoap.com/2012/02/10/each-necessary-but-only-jointly-sufficient/)* and broader writing on complex-systems failure.
- **Dr. Richard Cook** — *[How Complex Systems Fail](https://how.complexsystems.fail/)* — 18 short, true observations every responder should read.
- **Public postmortems** — [github.com/danluu/post-mortems](https://github.com/danluu/post-mortems) curated list.
