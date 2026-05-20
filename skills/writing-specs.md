# Writing Specs

> A spec is the artifact that lets someone else — a teammate, a reviewer, an AI assistant, your future self — build the right thing without you in the room. In an AI-first org, the spec *is* the engineering work; the code is increasingly downstream.

This is the practical companion to [spec-driven-development.md](../docs/spec-driven-development.md) and [spec-template.md](../templates/spec-template.md).

---

## Purpose

You can take a problem — vague, contested, partially understood — and turn it into a written spec that names the user, the goal, the non-goals, the design, the alternatives, the risks, the rollout, the rollback, and the success criteria. Reviewers can find the holes; builders (human or AI) can implement; future readers can understand why.

---

## Why it matters in an AI-first org

- **Specs are the durable artifact**; code is generated and regenerated. The spec is what you actually own.
- **AI code quality scales with spec quality.** Vague spec in, vague code out — at machine speed.
- **Async review at scale** requires written specs; you cannot whiteboard with 8 people in 6 time zones.
- **Postmortems trace failures back to spec gaps** more often than to coding errors. A good spec prevents whole classes of incidents.

---

## The practice

### Before writing

- **Talk to the user / customer / requester.** Spec writing without discovery produces beautifully-shaped solutions to the wrong problem.
- **Read the existing code and adjacent specs.** You're not the first person to think about this corner of the system.
- **Frame the problem in one paragraph** before you propose a solution. If you can't, you haven't understood it.
- **Decide the spec's weight class** ([spec-driven-development.md](../docs/spec-driven-development.md)): tiny change → paragraph in a PR; significant feature → full spec; load-bearing architecture → spec + [ADR](../templates/architecture-decision-record.md).

### The sections that matter

A well-formed spec answers, in roughly this order:

1. **Problem & user** — whose problem, why now, what evidence.
2. **Goals & non-goals** — what done looks like, *and what you are explicitly not doing.* Non-goals are the most useful section and the most often skipped.
3. **Proposal** — the design at the level a peer can challenge. APIs, data shapes, sequence, dependencies.
4. **Alternatives considered** — at least two real ones, with why-not. If you couldn't write one, you haven't thought enough.
5. **Risks & open questions** — what would make this fail, what you don't know yet, what's a one-way door.
6. **Rollout & rollback** — how it ships, how you'd undo it ([release-engineering.md](../docs/release-engineering.md)).
7. **Success criteria** — metrics, evals, SLOs. How you'd know in 90 days whether it worked.
8. **Owner, reviewers, decision asked** — names; dates; what the reader is being asked to do.

### Craft-level moves

- **Lead with the user, not the system.** "Customers can't recover an abandoned checkout" beats "Refactor the cart service."
- **Quantify where you can.** "Cut p95 from 800ms to 200ms" beats "improve performance."
- **Diagram the load-bearing piece.** One sequence diagram or data-flow beats three paragraphs.
- **Name the trade-off explicitly.** "We're picking simpler operations over lower latency because…"
- **Pre-mortem in the risks section.** "If this is rolled back in 6 weeks, the cause will likely be X."
- **Be honest about what you don't know.** Open questions are not weakness; their absence is.
- **Edit ruthlessly.** A great 4-page spec beats a sprawling 12-page one every time. See [technical-writing.md](technical-writing.md).

---

## Drills

- **Daily — the one-paragraph spec.** Before any non-trivial change, write a paragraph: user, problem, proposal, success criteria. Most "I'll just hack it" sessions improve enormously from 5 minutes of this.
- **Weekly — review three specs.** Pick three from your team or org. Note one thing each does well and one thing each is missing. Calibrates your bar.
- **Monthly — write one full spec.** Even when you don't strictly need to. Use it to think through something hard before building. Reviewers will give you free design help.
- **Quarterly — postmortem your specs.** Pull specs from a quarter ago. Which predicted the outcome? Which were wrong about risks, scope, alternatives? Pattern-spot your spec blind spots.
- **With AI:** use a model to generate a *first-pass critique* of your spec — "what's missing?" "where would this fail?" "what alternative did the author dismiss?" Use as input, not as output. Never ask AI to write the spec for you; the *thinking* is the work.

---

## Common failure modes

- **Solution before problem.** Spec opens with the design; the problem section is two sentences of context. Almost always means you're solving the wrong thing.
- **Missing non-goals.** Without them, every reviewer adds scope and every implementer has to guess.
- **Alternatives section that's a strawman.** "We could do X (bad), Y (worse), or Z (our proposal)." Reviewers see right through it. Write the alternatives *fairly*.
- **No rollback plan.** Means the team will invent one at 3am during the incident.
- **No success criteria.** You will ship it, declare victory, and never know whether it worked.
- **AI-generated spec, unedited.** Generic structure, generic risks, no specifics about *your* system. Embarrassing in review.
- **Spec as performance art.** 18 pages, every section, no decision asked. Length is not quality.
- **Spec that doesn't say who decides.** It will sit unreviewed for two weeks.
- **Spec written after the code is done.** Now it's documentation, not a spec, and the design conversation never happened.

---

## Tune for your context

- **Smaller / faster orgs:** lean on the one-paragraph spec for most things; reserve the full spec for genuinely load-bearing work.
- **Regulated domains:** required sections, evidence retention, formal sign-off; the spec is also an audit artifact.
- **Heavy AI codegen:** invest harder in success criteria and rollback; the speed of generation makes mistakes scale fast.
- **ML / AI feature work:** add eval criteria and an [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md) link.
- **Platform / infra work:** include adoption plan and migration path; the spec needs to address how users get there.

---

## Further reading

- **Sean Goedecke** — [Why I write design docs](https://www.seangoedecke.com/why-i-write-design-docs/) — practical case for the practice.
- **Will Larson** — [Writing an engineering strategy](https://lethain.com/eng-strategies/) and his broader writing on engineering documents.
- **Google** — [Design Docs at Google](https://www.industrialempathy.com/posts/design-docs-at-google/) (Malte Ubl) — what the discipline looks like at scale.
- **Amazon** — the 6-pager and PR FAQ tradition; widely written about in Bezos's letters and ex-Amazon writing.
- **Joel Spolsky** — [Painless Functional Specifications](https://www.joelonsoftware.com/2000/10/02/painless-functional-specifications-part-1-why-bother/) — older but still useful on why specs.
- **GitHub's RFC process** and **Rust RFCs** — public examples of mature spec/RFC traditions you can model on.
