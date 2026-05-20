# Critical Thinking With AI

> *AI is a brilliant, well-read, eager intern who will confidently tell you the wrong answer with a smile, and who has never been held accountable for an outage in its life.*

The most expensive failure mode of an AI-first engineering organization is not that AI tools are bad. It is that **humans become gullible**. They stop questioning. They stop verifying. They stop pushing back. The model said it, the PR builds, the test passes, ship it.

This is a cultural failure, not a tooling failure. This document is the operating system's antidote.

---

## The core stance

> **Treat every AI response the way you would treat a confident answer from a smart, junior teammate who joined yesterday: with respect, with curiosity, and with verification.**

You wouldn't merge a junior engineer's first PR without reading it. You wouldn't deploy a junior's first migration without testing it. You wouldn't accept a junior's claim that "this library handles concurrency correctly" without checking. You would do all of that *kindly*, *collaboratively*, in a way that helps them grow — because that's a healthy engineering culture.

Hold AI to the same bar. Not lower. Not higher. **The same.**

---

## The three habits: Question, Verify, Push Back

These three habits, practiced daily, are the difference between an AI-augmented org and an AI-gullible org.

### 1. Question

Before accepting any non-trivial AI response, ask:

- **What did I actually ask?** (Did the model answer my real question, or a nearby question?)
- **What assumptions is this response baked on?** (Stack version, library version, threat model, scale, region, budget.)
- **What's the most likely way this is wrong?** (Hallucinated API, out-of-date pattern, plausible-sounding-but-fake citation, edge case ignored.)
- **What's the source?** (Is it citing? Is the citation real? Have I checked?)
- **Would a skeptical Staff engineer push back on this?** (If yes — what would they push back on? Push back on it yourself.)

Questioning is not hostility. It is **respect** — the same respect a senior engineer shows a peer's design by actually engaging with it.

### 2. Verify

For any AI output that will touch production, customers, money, or trust, **verify before you trust**. The verification ladder, in increasing rigor:

| Stake | Verification |
|---|---|
| Throwaway script, local experiment | Read it. Run it. |
| Internal tool, low blast radius | Read it. Run it. Write a quick test. |
| Production code, no customer impact yet | Read it. Test it. Get human review. Run it through the same gates as hand-written code. |
| Customer-facing, money-handling, security-sensitive | All of the above + an eval suite + a second human approver + a rollback plan ([AI policy](ai-assisted-development-policy.md)). |
| Model-as-product (AI features your customers see) | All of the above + offline benchmark + LLM-as-judge + human review + red-team ([eval template](../templates/ai-feature-eval-template.md)). |

**Specific verification reflexes everyone learns:**

- **Citations are checked.** If an AI cites a paper, RFC, API, or doc — open it. AI invents citations regularly.
- **APIs are tested, not believed.** "This library has a `retry_with_backoff()` method" — does it? Run it.
- **Numbers are recomputed.** Latency claims, cost claims, percentile claims. Don't quote AI math in a leadership deck without rechecking.
- **Architecture diagrams are interrogated.** Is the data flow physically possible given the network boundaries? Is the failure mode actually handled?
- **Security claims are independently confirmed.** "This is safe from SQL injection" is a claim, not a proof. Read the code.

### 3. Push Back

Push back on AI the way you push back on a teammate whose proposal you respect but don't yet agree with:

- **"Why this and not the obvious alternative?"** Force a comparison.
- **"What's the failure mode at 10× scale? At 1/10× scale?"**
- **"What are the downsides of your recommendation?"** (Many models will sycophantically agree with whatever framing you gave them. Force them to argue against themselves.)
- **"Show me three reasons this is wrong."**
- **"What would [a respected named author / pattern] say about this?"** Force a perspective shift.
- **"Try again, optimizing for [different criterion] this time."**

Push-back is not adversarial — it's how senior engineers help each other find better answers, and it's how you extract a better answer from AI. The model will often produce a meaningfully better response when challenged. If yours doesn't, your prompt was too narrow.

---

## Sycophancy is a known failure mode — design around it

Modern LLMs are trained, in part, on signals that reward sounding agreeable. They will:

- Agree with the framing you presented, even when the framing is wrong.
- Soften their pushback because you wrote your prompt with confidence.
- Tell you your code is "great" before identifying a real bug.
- Validate your strategy because you asked "is this strategy good?" instead of "what's wrong with this strategy?"

This is not malice; it is a property of the system. We design around it:

- **Prompt for dissent, not validation.** Ask "what's wrong with this?" before asking "is this right?"
- **Ask the same question from multiple framings.** If the answers diverge meaningfully, the model is being influenced by *how you asked*, not the underlying truth.
- **Ask for the strongest case against your idea.** Then evaluate it on its merits.
- **Treat unqualified agreement as a red flag.** If a model agrees with everything you've ever proposed, the model is not thinking — you are just typing.

---

## Calibrated trust by domain

Trust is not binary. Calibrate it by where the model is strong and where it is weak.

| Domain | Default trust | Reasoning |
|---|---|---|
| Boilerplate code, well-known patterns, ubiquitous APIs | High | Massive, well-represented training data. Easy to verify. |
| Translating between known formats (JSON ↔ YAML, SQL ↔ ORM) | High | Mechanical, well-defined. |
| Generating tests for code in front of it | Medium-high | Verify the tests *actually fail* when the code is broken. |
| Documentation drafts, summarization, brainstorming | High | But verify factual claims. |
| Novel algorithm design | Medium | Check the math. Check the asymptotics. Check the edge cases. |
| Library APIs (especially recent versions) | Medium-low | Hallucinated method names are extremely common. |
| Security-sensitive code | Low — verify always | Plausibility ≠ safety. |
| Anything depending on data after the model's training cutoff | Low | Versions, deprecations, recent CVEs. |
| Internal-to-your-company context | Very low | Unless explicitly given via retrieval / context, the model is guessing. |
| Numerical or financial calculations | Low | Verify by recomputation. |
| Hot-take opinions about "what is best" | Skeptical | The model averages internet opinion, weighted by its training. |

This table is calibration training. New engineers internalize it by working alongside engineers who already have it.

---

## Practices we install across the org

### In code review

- A reviewer flagging "this looks AI-generated and unread" is a *valid review comment*. The PR author is expected to defend the code as their own — because they are the [author of record](ai-assisted-development-policy.md).
- A standing question in every non-trivial review: *"What did you check that the model was actually right about?"*

### In design discussions

- When AI-generated material is presented (RFC draft, ADR draft, architecture sketch), the human presenter explicitly states:
  - What they used AI for.
  - What they verified.
  - What they're still unsure of.
- This is normal, low-drama, and reinforces the cultural norm.

### In specs

The [spec template](../templates/spec-template.md) requires authors to identify open questions and assumptions. AI-drafted specs are not exempt — they often *increase* the number of open questions, because the model fills in plausible-sounding details that the human now has to either own or remove.

### In incidents

When an incident involves AI-assisted code or an AI feature, the [postmortem](../templates/postmortem-template.md) asks:

- Was AI output verified before deploy? At what level?
- Did sycophancy or rubber-stamping play a role?
- What verification step, added to our standard process, would have caught this?

The answer is never "use less AI" or "use more AI." It is "verify at the appropriate level for the stake."

### In leveling

The [career ladder](career-ladders.md) treats *judgment about AI output* as a senior-engineer differentiator. Specifically:

- **IC3 / mid-level:** uses AI fluently, verifies output proportional to stake.
- **IC4 / senior:** consistently pushes back on weak AI output, teaches juniors to do the same, never ships unread AI code.
- **IC5+ / Staff:** designs the verification systems (evals, gateways, paved-road patterns) that make pushback the easy default for everyone else.

We do not promote engineers who treat AI output as ground truth. They are dangerous at scale.

### In hiring

The [hiring loop](hiring-process.md) includes:

- An **AI-assisted module** where we evaluate not just the output, but how the candidate questioned, verified, and pushed back on the model's suggestions.
- An **AI-not-allowed module** to ensure the candidate can reason from first principles when the model isn't there.

A candidate who silently accepts a wrong AI suggestion in the assisted module does not pass, regardless of how the final code looks.

---

## The cultural rule: pushback is kindness

The most important cultural belief to install:

> **Pushing back is how we help each other — and how we help AI — produce better work. Silence is not kindness. Silence is how mediocre things ship.**

The same way a healthy team norm is "I'm going to challenge your design because I want it to be better, and I trust you to do the same to me" — that norm must extend to AI. The model does not have feelings to bruise. The cost of *not* pushing back is paid by your customers, your on-call, and the next engineer to debug it.

Teams that internalize this become *better at thinking*. AI becomes a sparring partner that makes them sharper, not a soothing voice that makes them lazy.

---

## Anti-patterns to name and kill

- **Vibe-coding into production.** Accepting AI output because the syntax highlights nicely.
- **The "looks fine to me" review.** Reviewer didn't read the code; rubber-stamped because the description was confident.
- **Citation laundering.** Quoting a number, API, or pattern from AI as if you verified it.
- **Prompt-as-conviction.** "I asked the model and it said X" used as evidence in a design debate. It's not.
- **Confidence inflation.** AI doesn't say "I don't know"; humans hearing AI assume the AI doesn't need to.
- **The shrinking pushback.** Engineers gradually push back less because the model is *usually* right. That's how you get bitten by the unusual cases — which are the only ones that matter.
- **AI as authority for org/people decisions.** Performance, leveling, hiring, comp. Not the model's job. Not now, probably not ever.

---

## How this connects

| When you... | Use these together |
|---|---|
| Make any non-trivial decision | [decision-making.md](decision-making.md) + this doc |
| Write or review a spec | [spec-driven-development.md](spec-driven-development.md) + this doc |
| Ship customer-facing AI | [ai-assisted-development-policy.md](ai-assisted-development-policy.md) + [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md) + this doc |
| Run a postmortem | [incident-management.md](incident-management.md) + [postmortem-template.md](../templates/postmortem-template.md) + this doc |
| Hire | [hiring-process.md](hiring-process.md) + this doc |
| Promote | [career-ladders.md](career-ladders.md) + this doc |

---

## Further reading

- Anthropic — [*Towards Understanding Sycophancy in Language Models*](https://arxiv.org/abs/2310.13548) (Sharma et al., 2023) — the empirical case that LLM sycophancy is a measurable, generalizable failure mode.
- OpenAI — [Model Spec](https://model-spec.openai.com/) — public articulation of intended model behavior, including honesty and pushback expectations.
- Daniel Kahneman — *Thinking, Fast and Slow* — System 1 vs System 2; why "looks right" is the most expensive cognitive default.
- Hubert Dreyfus & Stuart Dreyfus — *Mind Over Machine* — the five-stage skill acquisition model; why beginners over-trust rules and experts know when rules don't apply.
- Cal Newport — *Deep Work* — the case for sustained, undistracted cognitive effort, which is exactly what AI tooling can erode if used without intent.
- Julia Galef — *The Scout Mindset* — calibrated curiosity vs defensive certainty; the cognitive stance this entire doc tries to instill.
