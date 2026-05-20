# Strategic Thinking

> Strategy is the discipline of choosing what *not* to do, with limited information, against a real adversary or constraint, so that your team's effort compounds rather than disperses. In an AI-first world, where the cost of execution is dropping, the choice of *what* to execute is the bigger lever.

This is the personal-skill companion to [engineering-strategy.md](../docs/engineering-strategy.md).

---

## Purpose

You can take an ambiguous business situation — competitive, technical, organizational — and produce a written strategy that names the constraint, the trade-off, the bet, and the consequences. You can also tell the difference between a strategy and a wish list, and you push back on the latter.

---

## Why it matters in an AI-first org

- **Execution is cheaper; misdirection is more expensive.** Shipping the wrong thing fast is the new way to fail.
- **The competitive landscape is moving on shorter cycles.** Strategies that worked 2 years ago describe a different world.
- **Specific human judgment is the scarce input.** AI can pattern-match analogies and generate frameworks; it cannot make the actual bet.
- **The org needs a written, defensible "why this."** "Because the AI suggested it" is not a strategy; it is an abdication.

---

## The practice

### The Rumelt frame (use it relentlessly)

Per Richard Rumelt's *Good Strategy / Bad Strategy*, a real strategy has three parts (the **kernel**):

1. **Diagnosis** — what is actually going on. The single most important and most-skipped step. Most "strategies" skip directly to action.
2. **Guiding policy** — the approach you'll take to address the diagnosis. Names what you'll do *and* what you'll explicitly *not* do.
3. **Coherent action** — a small set of mutually-reinforcing moves that implement the policy. Each action makes the others stronger.

If you can't write all three in one page, you don't have a strategy. You have hope.

### Distinguish strategy from its impostors

- **A list of goals is not a strategy.** "Grow revenue 40%, ship 3 products, raise NPS 10pts" — that's a wish list. The strategy is *how*, against what.
- **A roadmap is not a strategy.** Roadmaps describe sequence; strategies describe *why this sequence and not another*.
- **A vision is not a strategy.** "Be the best AI-native X" — directional, not actionable.
- **A buzzword is not a strategy.** "Be AI-first" is a *stance*; the strategy is what changes about your investments and operations as a result.

### The moves of strategic thinking

- **Name the constraint.** What is actually limiting you? Capital, talent, distribution, customer trust, technical debt, time? The constraint shapes the strategy.
- **Name the bet.** Where are you putting disproportionate resources? If your investments are even across 6 things, you don't have a strategy; you have a portfolio.
- **Name what you're *not* doing.** The non-goals are the most useful part. Without them, the team will quietly do everything.
- **Identify the leverage point.** Most situations have a 10×-leverage move and 50 1×-leverage moves. The strategy picks the 10×.
- **Pre-mortem the strategy.** "In 18 months this strategy is judged a failure. What was the cause?" Surfaces fatal flaws optimism suppresses.
- **Write it as if a smart skeptic is reading.** If you can defend it against the strongest objection, you have something.

### Working in time horizons

- **Horizon 1 (run the business):** how the current business gets stronger this year. Reliability, growth, cost.
- **Horizon 2 (scale the next bet):** what's emerging now that will be a meaningful share of the business in 2–3 years.
- **Horizon 3 (explore the frontier):** what we're learning about that might be a thing in 3+ years. Small bets, fast cycles, real learning.

A strategy must specify the *mix* across horizons. Otherwise Horizon 1's urgency consumes Horizons 2 and 3 every quarter. See [engineering-strategy.md](../docs/engineering-strategy.md).

### Working with AI on strategy

- **Use AI to enumerate analogies and frameworks.** "Companies that faced a similar inflection point — what did they do?"
- **Use AI to pre-mortem.** "Argue this strategy will fail. Give me the strongest case." Read it; address it.
- **Never let AI write the strategy.** It will produce something fluent, generic, and unfalsifiable. The work is the *choosing*; AI cannot do it because it has no skin in your game.
- **Be skeptical of analogies.** AI is good at finding similar-looking cases; whether the similarity is causal is your judgment call.

---

## Drills

- **Monthly — write a one-page strategy** on something you own, even informally. Force the kernel: diagnosis, policy, coherent actions. Most don't survive the page; the ones that do clarify your thinking.
- **Quarterly — re-read your strategy and last quarter's outcomes.** What did you predict? What happened? What did you miss? Update.
- **Quarterly — pre-mortem with a colleague.** Each of you spends 30 minutes attacking the other's strategy.
- **Read one strategy doc you didn't write per month.** Public Q-letters from operators (Stripe, Shopify, Snowflake), Bezos shareholder letters, ARK research, your competitors' all-hands transcripts. Calibrates what good looks like.
- **Read one strategy *book* per quarter.** Different ones; rotate. The genre is small and tractable.
- **With your manager / CEO / board:** stress-test your strategy. Ask for the strongest objection, not the polite version.

---

## Common failure modes

- **The wish list.** "Be the best, fastest, most loved, most reliable." Vibe, not strategy.
- **Strategy as a presentation.** 40 slides; no kernel; no constraint named; the room nods. Six weeks later, nothing has changed.
- **Strategy that doesn't change behavior.** The test: what investment, hire, project, or partnership *changed* as a result? If nothing, it wasn't a strategy.
- **Confusing 3-horizon mix.** All H1 (no future), all H3 (no business), or all H2 (no learning). The mix is the strategic choice.
- **Goals masquerading as strategy.** "Grow 40%" is a goal; *how* you grow 40% is the strategy.
- **Strategy without diagnosis.** Pure forward-looking aspirations with no clear-eyed view of the present.
- **One person's strategy.** Not socialized; not pressure-tested; not adopted; doesn't survive contact with the org.
- **Frozen strategy.** Written once, never revisited. The world moves; strategy must too.
- **AI-generated strategy.** Fluent, generic, can fit any company. The fact that it's not specific to *yours* is the tell.
- **Strategy from analogies that don't transfer.** "We'll do what Stripe did." You are not Stripe.

---

## Tune for your context

- **Earlier-stage:** strategy revisited every 3 months; horizon-2/3 small; constraint usually distribution or capital.
- **Scaling:** strategy stabler (annual); constraint shifts to talent and coordination; horizon-2 investment becomes critical.
- **Mature:** strategy multi-year; defense of horizon-3 becomes harder and more important; constraint often complacency.
- **Highly regulated:** strategy includes the regulatory landscape explicitly; long lead times on bets.
- **Engineering-org strategy (vs whole-company):** narrower scope; same discipline. See [engineering-strategy.md](../docs/engineering-strategy.md).
- **AI-native company:** the model frontier *is* part of your strategic context; reread the landscape every quarter.

---

## Further reading

- **Richard Rumelt** — *Good Strategy / Bad Strategy* — the single most useful book on the topic. The "kernel" idea is foundational.
- **Roger Martin** — *Playing to Win* — strategy as a cascade of integrated choices. Useful operational frame.
- **Will Larson** — [Writing an engineering strategy](https://lethain.com/eng-strategies/) and broader writing on engineering strategy at scale.
- **Jeff Bezos** — [annual letters to shareholders](https://www.aboutamazon.com/news/company-news/2021-letter-to-shareholders) — strategic thinking made operational.
- **Clayton Christensen** — *The Innovator's Dilemma* — why successful orgs miss disruption. Still relevant in the AI era for the same reasons.
- **Andy Grove** — *Only the Paranoid Survive* — strategic inflection points; how to recognize and act on them.
- **Hamilton Helmer** — *7 Powers* — structural sources of competitive advantage; useful lens for "what compounds."
- **Geoffrey Moore** — *Crossing the Chasm* — for product strategy in adoption-curve contexts.
