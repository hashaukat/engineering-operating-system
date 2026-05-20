# Technical Writing

> The org operates at the speed of its writing. In an AI-first, async-default, spec-driven world, the engineer who writes well has 2–3× the leverage of one who doesn't — because their reasoning compounds across people, time zones, and AI tools.

---

## Purpose

You can write a clear, complete, scannable document that lets a reader make a decision, take an action, or build the thing — without scheduling a meeting with you. You match the document's depth and length to the stakes, and you treat editing as the work, not the chore.

---

## Why it matters in an AI-first org

- **Specs are the durable artifact** ([spec-driven-development.md](../docs/spec-driven-development.md)). The spec is the input to humans *and* AI tooling. Vague specs produce vague code.
- **Decisions need rationale**, written down ([decision-making.md](../docs/decision-making.md)). Two years later, only the writing survives.
- **Meetings get expensive at scale.** A 30-minute meeting for 8 people is 4 person-hours and a context switch each. A 5-minute read is 40 person-minutes, no context switch, and is searchable. The math is brutal.
- **AI generates fluent prose.** What's scarce is *clear thinking shaped into prose by a human.* Writing well is increasingly how you signal that you actually thought.

---

## The practice

### Before you write

- **State the purpose in one sentence.** "This doc exists so [audience] can [decide / understand / do] X." If you can't write it, you're not ready to write.
- **Know the audience and the decision.** A spec for engineers is different from an update for an exec.
- **Choose the format** to match the stakes: a Slack message, a paragraph, a one-pager, a full spec, an RFC. Don't over- or under-shoot.
- **Decide what you're cutting** before you draft. Most drafts are too long because they include everything the writer thought, not what the reader needs.

### The shape that almost always works

1. **TL;DR / Decision asked / Bottom line up front.** What you'd want them to remember if they read nothing else.
2. **Context** — just enough for the reader to evaluate the rest. Not your life story.
3. **The thing itself** — proposal, decision, plan, finding.
4. **Trade-offs / risks / alternatives considered** — what you didn't pick and why.
5. **Decision asked / next step** — who needs to do what by when.

This shape works for specs, ADRs, decision records, status updates, exec briefings, postmortems. Customize sections; keep the order.

### Sentence-level craft

- **Lead with the verb.** "Decide X by Friday" not "It would be helpful if a decision could be made about X."
- **One idea per sentence.** Long sentences hide reasoning errors.
- **Prefer concrete to abstract.** "Cut p99 latency from 800ms to 200ms" beats "improve performance."
- **Quantify.** Numbers beat adjectives. "3 weeks late" beats "delayed."
- **Cut hedges.** "We think we might possibly want to consider" → "We propose." Hedge in the *uncertainty calibration*, not in every verb.
- **Be specific about ownership and time.** Passive voice hides who and when. "It will be reviewed" → "Maya will review by Tuesday."
- **Cut ~30% on every edit pass.** The first cut is almost always pure improvement.

### Structural craft

- **Headings are a table of contents.** Make them scannable; a reader should grok the shape from headings alone.
- **Bold the load-bearing sentences.** In a long doc, the reader should be able to read only the bold and still get the argument.
- **Tables for comparison.** Prose for narrative. Don't mix.
- **Lists for parallel structure.** If items aren't parallel, they don't belong in the same list.
- **Diagrams for relationships.** If you're describing connections between things, draw them.

---

## Drills

- **Daily — the TL;DR drill.** Before any doc, write the one-sentence TL;DR. If it's hard, your thinking isn't done.
- **Weekly — the 50% cut.** Take one of your own docs and cut it in half without losing content. Do this until cutting becomes reflexive.
- **Weekly — read good writing.** Pick one essay or memo from a writer you admire (Will Larson, Charity Majors, Patrick McKenzie, Bezos shareholder letters). Note what makes it work.
- **Monthly — rewrite an old doc.** Take something you wrote 6+ months ago. Rewrite it with current craft. The delta is your growth.
- **With a peer — paired editing.** Edit each other's drafts. The asymmetry of "I see your blind spots, you see mine" makes both better fast.
- **With AI:** ask the model "what's confusing in this draft?" — but never "rewrite it for me." The first sharpens your judgment; the second atrophies it.

---

## Common failure modes

- **Burying the lede.** TL;DR at the bottom, context for two pages, the actual ask in the last paragraph. Readers stop before they get there.
- **Length as effort signal.** "I wrote 12 pages so they'll know I thought hard." Length signals length. Brevity signals thought.
- **AI prose smell.** Hedged, listy, even cadence, "it's worth noting that...", "comprehensive," "robust," "leverage." Edit it out.
- **One doc for two audiences.** Exec summary and engineer-level detail in one artifact that serves neither. Split them.
- **No decision asked.** A long doc that doesn't say what the reader is supposed to do with it. Always close with the ask.
- **Passive voice everywhere.** "Mistakes were made." By whom?
- **Jargon as armor.** Using terminology to sound expert when plain language would land better.
- **No editing.** First draft = shipped draft. The skill is in the edit.

---

## Tune for your context

- **Distributed / async orgs:** lean harder on this skill across all roles; writing replaces synchronous discussion.
- **Earlier-stage orgs:** smaller docs, more bias to ship; over-investing in long-form writing slows things down.
- **Larger orgs:** invest in *standardized* formats (one-pager, spec, RFC, postmortem) so readers know what to expect.
- **Regulated domains:** specifics tighten — required sections, retention, sign-off; structure becomes mandatory.
- **Customer-facing writing** (release notes, status pages, support replies) is its own sub-skill; the core craft transfers.

---

## Further reading

- **William Zinsser** — *On Writing Well* — the foundational text for nonfiction prose.
- **Strunk & White** — *The Elements of Style* — sentence-level discipline.
- **Jeff Bezos** — [annual shareholder letters](https://www.aboutamazon.com/news/company-news/2021-letter-to-shareholders) and the Amazon 6-pager / PR FAQ practice.
- **Will Larson** — [lethain.com](https://lethain.com/), particularly on writing eng strategy.
- **Patrick McKenzie** — [Bits About Money](https://www.bitsaboutmoney.com/) — long-form done right.
- **Julian Shapiro** — [Writing Guide](https://www.julian.com/guide/write/intro) — modern, practical, web-native.
- **Bottom Line Up Front (BLUF)** — US military communication standard; the shape this skill borrows from.
