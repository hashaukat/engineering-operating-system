# Critical Thinking & Judgment

> The scarce resource in an AI-first org is *judgment*: the ability to look at a confident, plausible answer and decide whether to trust it, push back, or change the question. Everything else can be generated.

---

## Purpose

You can take a claim, a recommendation, an analysis, or a plan — from a person, a model, a vendor, or yourself — and assess whether it's actually true, complete, and load-bearing for the decision in front of you. You hold opinions calibrated to evidence and update them when the evidence changes.

---

## Why it matters in an AI-first org

The supply of plausible answers is now effectively infinite. Models will produce a confident, well-formatted recommendation for any question, including the wrong one. Three things change:

- **Plausibility is no longer a signal of correctness.** It used to be a weak one; it isn't anymore.
- **The cost of a confidently-wrong decision is paid downstream** — in production, in customer trust, in unwound work.
- **The scarce skill is the verifier**, not the generator. Senior engineers and leaders are now mostly verifiers.

This skill is the foundation under [decision-making.md](../docs/decision-making.md) and [critical-thinking-with-ai.md](../docs/critical-thinking-with-ai.md).

---

## The practice

Observable behaviors of people who do this well:

- **Restate before responding.** "What I think you're asking is X — is that right?" Catches half the wrong answers before they're given.
- **Name the question type.** Empirical (look it up), analytical (reason about it), values (negotiate it), or predictive (make a forecast). Different types need different evidence.
- **Distinguish claim from evidence from inference.** When given an answer, separate "what the source says," "what is actually shown," and "what the speaker concluded from it."
- **Ask the steel-man and the strongest counter.** "What's the best version of this argument? What's the best argument against it?"
- **Express uncertainty in calibrated terms.** Not "I'm pretty sure" but "I'm ~70% confident" — with a willingness to be measured against it.
- **Identify the irreversible.** Type 1 vs Type 2 (Bezos). Slow down on Type 1, speed up on Type 2.
- **Pre-mortem before commitment.** "Assume this fails in 6 months. What was the cause?" Surfaces what optimism suppresses.
- **Look for the disconfirming evidence**, not the confirming. The most valuable input is the one that would change your mind.
- **Note your priors and updates.** "I thought X. The new evidence is Y. I now think Z." This is the unit of intellectual honesty.

---

## Drills

- **Daily — restate-then-answer.** For one week, restate every non-trivial question before answering. Notice how often the restatement reveals you would have answered the wrong question.
- **Weekly — calibrate your forecasts.** Each week, write down 3–5 predictions with explicit % confidence (a meeting outcome, a metric for the week, a project ETA). Score them quarterly. Tetlock's research shows calibration improves measurably from this alone.
- **Weekly — devil's advocate on your own draft.** Before sending any non-trivial doc, write the strongest 3-paragraph rebuttal to your own argument. Edit accordingly.
- **Monthly — kill a belief.** Pick a strongly-held view (technical, organizational, strategic) and seriously investigate whether it's still true. Most aren't, after 18 months.
- **Quarterly — postmortem your decisions.** Pull your last quarter's [decision records](../templates/decision-record-template.md). Which were right? Which weren't? *Why* — was it the process or the luck?
- **With your manager:** ask them to push back hardest on the decisions you're *most* confident about. Confidence is where calibration fails hardest.

---

## Common failure modes

- **Plausibility = correctness.** It sounds right, it's well-written, so it's right. The single biggest AI-era failure.
- **Confirmation seeking.** Asking "what supports this?" instead of "what refutes this?"
- **First-answer anchoring.** The first plausible answer becomes the default; further options are evaluated as worse-than-the-first instead of on their merits.
- **Hidden uncertainty.** Expressing 60%-confidence claims with 100%-confidence language.
- **Authority deference.** "Senior person said it, so it's right." (Replace "senior person" with "the model" — same failure, new flavor.)
- **Conclusion before evidence.** Picking the outcome you want, then reverse-engineering the analysis.
- **Refusing to update.** Treating a changed mind as weakness. It's the opposite.
- **Analysis paralysis on Type 2 decisions.** Same critical thinking, wrong door — wastes the team's time.

---

## Tune for your context

- **Earlier-stage orgs** lean harder on speed; bias the practice toward "restate, pre-mortem, decide" and skip the heavier process.
- **High-blast-radius domains** (financial, health, infra) — invest harder in pre-mortems and explicit calibration; the cost of a wrong call is asymmetric.
- **AI-newer orgs** — over-invest in the "claim vs evidence vs inference" practice for a quarter; it's the muscle that catches hallucinations.
- **Distributed teams** — write your reasoning down by default; verbal reasoning doesn't scale or audit.

---

## Further reading

- **Annie Duke** — *Thinking in Bets* and *How to Decide* — calibrated confidence, decision quality vs outcome quality.
- **Philip Tetlock & Dan Gardner** — *Superforecasting* — what actually improves prediction accuracy.
- **Daniel Kahneman** — *Thinking, Fast and Slow* — the cognitive biases that quietly run your decisions.
- **Julia Galef** — *The Scout Mindset* — the disposition this skill is trying to install.
- **Shane Parrish / Farnam Street** — [fs.blog](https://fs.blog/) — mental models and decision quality, long-form.
- **Anthropic / OpenAI / DeepMind research** — sycophancy and hallucination studies; reread quarterly because the science updates.
