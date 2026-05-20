# Estimation & Forecasting

> Estimates are not promises; they are *calibrated forecasts under uncertainty*. The org that estimates honestly plans well, ships predictably, and is trusted by its partners. The org that estimates as a negotiation tactic — by either side — accumulates broken commitments and rebuilds trust at the end of every quarter.

---

## Purpose

You can produce an estimate — for a task, a feature, a quarter — that is honest about uncertainty, useful for decision-making, and durable enough to be reviewed without embarrassment. You can also recognize when estimation is the wrong tool and ask for a different one.

---

## Why it matters in an AI-first org

- **AI changes velocity unevenly** — some tasks 5× faster, some unchanged, a few slower. Old gut estimates miscalibrate in both directions.
- **Planning depends on aggregate predictability**, not heroic individual estimates ([planning-rhythm.md](../docs/planning-rhythm.md)).
- **Forecasting customer-value delivery** is increasingly how engineering is measured ([metrics-scorecard.md](../docs/metrics-scorecard.md)). Estimation feeds it.
- **AI assistants over-promise.** Their "this should take 2 hours" is uncalibrated; your judgment is the load-bearing input.

---

## The practice

### Estimate ranges, not points

- **Always give a range.** "3–5 days, 80% confident" is honest. "4 days" is a fiction.
- **Use the [Cone of Uncertainty](https://en.wikipedia.org/wiki/Cone_of_Uncertainty).** Early-discovery estimates are 4× wide; post-spec estimates are ~1.5×. Quote the cone where you are, not where you wish you were.
- **Confidence is part of the estimate.** Tell people whether you're 50%, 80%, or 95% sure.
- **Refresh the estimate as you learn.** Re-estimate at each step; communicate when it shifts materially.

### Decompose before estimating

- **Break work into chunks** that each take less than a few days. Anything bigger is a guess, not an estimate.
- **List the unknowns explicitly.** "Estimate is contingent on: API X behaving like the docs say; vendor Y answering by Tuesday." Unknowns are part of the estimate.
- **Identify the spikes** — work whose purpose is to *reduce uncertainty*. Time-box them; estimate them separately.

### Reference-class forecasting (the underused superpower)

- **Find similar past work.** "Last quarter we shipped a similar integration in 6 weeks." Past actuals beat inside-view intuition almost every time.
- **Beware the inside view.** "But this one is different / smaller / cleaner" — usually it isn't, and the cost is paid in slip.
- **Keep a personal / team history.** Past estimate vs past actual. Read it before quoting new estimates.

### When to refuse to estimate

- **Pure research / discovery.** Estimate the *time-box*, not the outcome.
- **No spec.** "Build a thing that sort of does X" cannot be estimated. Estimate the spec first; estimate the work after.
- **Bad data.** "Estimate Q3 capacity for 8 hires we don't have yet." Name the assumption; refuse to pretend.
- **Estimation as theater.** When asked to estimate to satisfy a process that won't use the estimate — name it; offer to do the planning a different way.

### For larger horizons (sprint / quarter / year)

- **Use throughput, not estimation, for aggregates.** "We've shipped ~22 stories per sprint over the last 5 sprints" is a better Q3 input than "we estimate Q3 at 130 stories."
- **Probabilistic forecasting** ([Daniel Vacanti](https://www.actionableagile.com/) / Monte Carlo) beats point-estimate roll-ups for "when will this be done?" at scale.
- **Always quote at a confidence level.** "85% chance we ship by Sep 30" is operational; "we will ship by Sep 30" is a story.
- **Build slack into the plan.** ~30% of capacity is the well-documented number for KTLO + incidents + interrupts in steady-state teams. Booking 100% is how plans break ([planning-rhythm.md](../docs/planning-rhythm.md)).

---

## Drills

- **Daily — estimate the next task.** Range + confidence + assumption. At end-of-day, record actual. Look at the gap. Patterns emerge in 2 weeks.
- **Weekly — pre-mortem the sprint.** Before sprint start, write "what would make this sprint miss?" Compare at retro.
- **Monthly — estimate-vs-actual review.** Personal or team. Look at biases: do you systematically under-estimate? On which kinds of work?
- **Quarterly — calibration check.** Of your 80%-confident estimates, did ~80% hit? If 60% hit, you're miscalibrated; recalibrate.
- **For AI-assisted tasks:** estimate separately *with* and *without* AI assistance for the same task class. Track which gap is real and which is illusion.
- **With your manager:** review your estimation history together. The patterns they see (over-promising under pressure; sandbagging for safety; ignoring known risks) are hard to see alone.

---

## Common failure modes

- **Single-point estimates.** "5 days." Sets a false expectation; gets quoted as a commitment; the slip is then a "miss."
- **Estimating to please.** Quoting what the asker wants to hear. Always backfires; trust never recovers cleanly.
- **Estimating to defend.** Padding 3× so you can always be a hero. Slows the org, destroys credibility.
- **Ignoring history.** Confident new estimates with no glance at past actuals. Predictably wrong.
- **Estimate-as-promise.** Asker treats the estimate as a commitment; engineer doesn't push back. Now everyone is unhappy when it shifts.
- **No re-estimation.** Locking in week-1 estimates and never updating, even when you've learned that week-1 was wrong.
- **Aggregating estimates without slack.** Booking 100% of capacity against features. KTLO, incidents, interrupts, illness, all unaccounted. The plan is fiction by week 3.
- **Inside view on novel work.** "I've never done this but it should take a week." Usually 3×–5× off.
- **Trusting AI's estimate.** A model saying "this is a 2-hour task" is uncalibrated. Use it as one data point, not as the answer.

---

## Tune for your context

- **Earlier-stage:** less formal estimation; more emphasis on weekly forecast updates and short-cycle adjustment.
- **Mature, contract-bearing orgs:** explicit confidence levels and reference-class forecasting; estimates may have external commitments attached.
- **Heavy-research / AI-research teams:** time-box discovery; estimate post-discovery; refuse upfront estimates on irreducible unknowns.
- **Agency / consulting context:** estimation is partly negotiation; the skill is honest about which part is estimate and which is commitment.
- **Distributed teams:** the *writing-down* part of estimation matters more; verbal estimates evaporate across time zones.

---

## Further reading

- **Steve McConnell** — *Software Estimation: Demystifying the Black Art* — the most thorough single book.
- **Daniel Vacanti** — *Actionable Agile Metrics for Predictability* and the [Monte Carlo forecasting tools](https://www.actionableagile.com/) — probabilistic forecasting.
- **Daniel Kahneman & Amos Tversky** — *planning fallacy* and *reference-class forecasting* — the cognitive basis for why naive estimates are systematically optimistic.
- **DORA / Accelerate** — research on flow and predictability; throughput metrics over point estimates.
- **Magne Jørgensen** — long-running academic work on software-effort estimation biases.
- **Will Larson** — [lethain.com on systems thinking and planning](https://lethain.com/) — pragmatic, leadership-level estimation context.
