# Working with AI

> AI is a power tool, not an oracle, not a colleague, not a search engine. People who get disproportionate leverage from it have a specific, learnable practice — and so do the people who repeatedly get burned by it.

This is the daily-practice companion to [critical-thinking-with-ai.md](../docs/critical-thinking-with-ai.md) and the [AI policy](../docs/ai-assisted-development-policy.md). Critical thinking tells you *why*; this skill tells you *how*.

---

## Purpose

You can get high-quality, verifiable output from AI tools for the work you do — code, writing, analysis, planning, search — and you know when *not* to use them. You treat AI output as a draft from a fast, well-read, occasionally-wrong collaborator, and you ship only what you can defend yourself.

---

## Why it matters in an AI-first org

Productivity differences between AI-fluent and AI-naive engineers are now 2–5× on many tasks. But the *quality* differences run the opposite direction when AI-naive users ship unverified output. The two failure modes — "doesn't use it enough" and "trusts it too much" — are both expensive. This skill is the middle path.

---

## The practice

### How to ask

- **Front-load context.** Goal, constraints, audience, format, what good looks like, what to avoid. The single biggest quality lever.
- **Show, don't just tell.** Examples of what you want and what you don't want beat any description.
- **Constrain the answer shape.** "Give me three options with trade-offs" beats "what should I do?" by a wide margin.
- **Ask for the reasoning, then the answer.** Shifts the model into a more careful mode and gives you something to audit.
- **Specify what's outside scope.** Stops the long tangent before it starts.
- **Iterate, don't restart.** The second turn — "now apply X constraint" — is where most of the quality compound is.

### How to verify

- **Treat the output as a hypothesis.** Default disposition: this is wrong somewhere; my job is to find where.
- **Click every citation.** If it claims a paper, a library, an API method, a number — verify. Hallucinated references are the single most common failure.
- **Run the code.** Reading is not verifying. Especially for anything beyond a one-liner.
- **Sample the edge cases yourself.** Models are most wrong on the boundary cases they didn't see in training.
- **Ask the inverse question.** "What's wrong with this answer?" "What would make this fail?" Often surfaces what the first answer hid.
- **Cross-check across providers** for high-stakes claims. Two independent models disagreeing is a strong signal.

### When *not* to use AI

- When the cost of being wrong > the cost of doing it yourself. The math is rarely close on irreversible decisions, customer-visible writing, or security-sensitive code.
- When the task is your own thinking. AI ghost-writes feelings, retrospectives, and judgment calls badly; using it here atrophies the muscle you're paid for.
- When you'd be embarrassed to defend the source. If you can't say "I verified this and I stand behind it," don't send it.
- When confidential data shouldn't leave your environment. See [data-and-privacy-governance.md](../docs/data-and-privacy-governance.md) and the [AI policy](../docs/ai-assisted-development-policy.md).

### How to compose

- **AI for the draft, you for the judgment.** Generate, then heavily edit. Ship your voice, your structure, your conclusions.
- **AI for breadth, you for depth.** Use it to enumerate options; do the actual reasoning yourself.
- **Pair model strength with model strength.** A reasoning model for analysis; a fast model for transformation; a code model for code. One tool ≠ one model.

---

## Drills

- **Daily — the verification log.** For one week, write down every AI output you used. Mark which ones you verified. Notice the gap. Close it.
- **Weekly — adversarial prompt.** After getting an answer you like, ask the model to argue against itself. Note what changes.
- **Weekly — the no-AI day (or no-AI task).** Once a week, do one substantive task without AI. The skill it builds is judgment about *when* the tool helps and when it crutches.
- **Monthly — prompt library audit.** Keep your most-used prompts. Refine them quarterly. Treat them like code: versioned, reusable, tested.
- **With a peer — paired prompting.** Sit with a colleague and watch each other use AI on a real task. The patterns you each don't realize you have become visible.

---

## Common failure modes

- **Vibe-shipping.** Pasting AI output into production / a doc / a customer reply without reading it carefully. The fastest path to embarrassment.
- **Inheriting the model's voice.** Hedged, listy, over-structured, neutral. Distinctively LLM-shaped. Edit it out.
- **Asking the wrong question well.** Sophisticated prompting around the wrong framing. Restate the question before optimizing the prompt.
- **One-shot disease.** Accepting the first answer instead of iterating. The compound lives in turns 2–5.
- **Citation theater.** Claiming "the model said" as if that's evidence. It is not evidence. The cited source is evidence.
- **Stack overflow but worse.** Pasting in code, getting a plausible fix, shipping it without understanding it. You now own code you can't maintain.
- **Forgetting it's recording.** Putting customer PII, secrets, or unreleased strategy into a public model endpoint. See the AI policy.
- **AI as therapist for hard conversations.** Using AI to draft feedback, performance docs, or reorg messages. The output reads as exactly what it is.

---

## Tune for your context

- **Coding-heavy roles:** invest in editor-integrated assistants, the verification practice, and a personal eval set of "tasks the model often gets wrong on our codebase."
- **Writing-heavy roles:** invest in prompt-as-style-guide and heavy editing; ship in your voice.
- **Analyst / strategy roles:** invest in the adversarial-prompt practice; the worst failure mode is plausible analysis that's quietly wrong.
- **Regulated / sensitive domains:** tighten "when not to use" significantly. Make the allow-list explicit, not the deny-list.
- **As tools change:** rebuild your practice every ~6 months. The capability frontier moves; what was a good use case last quarter may be a wasted step now (or vice versa).

---

## Further reading

- **Simon Willison** — [simonwillison.net](https://simonwillison.net/) — daily, practical writing about using and being skeptical of LLMs.
- **Ethan Mollick** — *Co-Intelligence* and [oneusefulthing.org](https://www.oneusefulthing.org/) — frameworks for working with AI as a collaborator.
- **Anthropic** — [Prompting documentation](https://docs.anthropic.com/) and research on sycophancy / constitutional AI.
- **OpenAI** — [GPT best practices](https://platform.openai.com/docs/guides/prompt-engineering) — provider-specific but the patterns generalize.
- **Andrej Karpathy** — public talks on how LLMs actually work; calibrates what to expect of them.
- **Hamel Husain** — [hamel.dev](https://hamel.dev/) — practitioner writing on evals and LLM application quality.
