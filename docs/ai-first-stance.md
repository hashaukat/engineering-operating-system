# AI-First Engineering: The Stance

> "AI-first" is a leadership claim that has to be earned with a thousand operational decisions. This doc defines what I mean by it, what changes because of it, and what does *not*.

## What "AI-first" means here

**AI-first** is not "we use Copilot." Every team uses Copilot. AI-first means:

1. **Specs, not code, are the durable artifact** ([spec-driven development](spec-driven-development.md)).
2. **AI is in the default path** for every stage of the [execution model](execution-model.md), not a bolted-on tool.
3. **Productivity is measured in customer value delivered**, with AI as a multiplier, not as a separate scorecard ([productivity measurement](productivity-measurement.md)).
4. **Trust is engineered**: every AI-touched artifact has provenance, evals, and a human author of record ([AI policy](ai-assisted-development-policy.md)).
5. **Engineers grow into AI orchestrators**: the career ladder rewards judgment about *when not to ship*, not just shipping ([career ladders](career-ladders.md)).
6. **The org structure has an AI function from day one**, not a tiger team ([org design](org-design.md)).

## What changes in an AI-first org

| Domain | Before | After |
|---|---|---|
| Unit of work | Ticket | Spec |
| Definition of done | Code merged | Acceptance spec passing in prod + telemetry |
| Code review | "Does this look right?" | "Does this satisfy the spec? Is the spec right?" |
| Onboarding | Read the code | Read the specs |
| Hiring loop | Coding test | Coding test + AI-assisted module + judgment module |
| Staff engineer value | Designs systems | Designs systems *and authors high-leverage specs* |
| Incident response | Human triage first | AI-summarized timeline, human IC decides |
| Cost line item | Mostly people | People + AI usage + agent runtime |

## What does *not* change

These are easy to get wrong in the excitement of AI:

- **Accountability** — humans are still the author of record on every shipped artifact.
- **Customer outcomes** — the scoreboard is still CSAT, NPS, TTV, reliability. AI does not change what "good" means.
- **Quality bar** — the same security, privacy, and review gates apply regardless of how the code was generated.
- **Humane operations** — sustainable pace, on-call respect, calm engineering culture. AI does not justify a sweatshop.
- **The job of leaders** — to make decisions clear, to remove friction, to protect the people doing the work.

## The five capability investments

An AI-first org has to actually invest in capability — not just adopt tools. The five non-negotiable investments:

1. **A spec registry** — versioned, in-repo, searchable. The substrate for everything else.
2. **An eval harness** — shared across all customer-facing AI features. Treated as critical infrastructure.
3. **A prompt and model registry** — versioned, owned, rollback-able.
4. **An AI gateway** — one place where API calls to model providers go, with rate limits, cost tracking, audit logging, and policy enforcement.
5. **An internal developer platform** that exposes #1–#4 as a paved road.

Without these, "AI-first" is a slogan.

## The five cultural investments

Equally important, harder to ship:

1. **Engineers are paid to think, not to type.** Reward the rejection of a bad AI suggestion as visibly as the acceptance of a good one.
2. **The team is the unit of AI adoption.** Not individuals. Teams set norms, measure together, learn together.
3. **Failure modes are first-class learning.** When an AI-assisted change causes an incident, the postmortem studies the *judgment failure*, not the tool.
4. **Skepticism is a senior skill.** Staff+ engineers are the org's immune system against confident wrongness.
5. **Customers are the only scoreboard.** Speed without satisfaction is theater.

## How this stance shows up across the EOS

| Doc | AI-first implication |
|---|---|
| [Engineering strategy](engineering-strategy.md) | AI is treated as a horizon-2 multiplier and a horizon-3 disruptor — both invested in |
| [Operating principles](operating-principles.md) | Principle 7: "AI is a power tool, not an oracle" |
| [Org design](org-design.md) | Director of AI & ML Engineering on the leadership team from day one |
| [Team topologies](team-topologies.md) | Applied AI as a complicated-subsystem team; AI Adoption as an enabling team |
| [Planning rhythm](planning-rhythm.md) | Each plan states the spec-shipping target and the AI-leverage assumption |
| [Execution model](execution-model.md) | Spec-first, AI-in-the-loop at every stage |
| [Metrics scorecard](metrics-scorecard.md) | Customer-value lens includes AI-feature quality; productivity lens includes spec throughput |
| [Incident management](incident-management.md) | AI assists; humans command and decide |
| [Architecture review](architecture-review-process.md) | RFCs state how AI agents/features are evaluated and governed |
| [Career ladders](career-ladders.md) | AI fluency is table stakes; AI judgment is the senior-level differentiator |
| [Hiring](hiring-process.md) | One AI-allowed module, one AI-not-allowed module |

## How I would explain this to a board

> "Our engineering organization is built so that AI makes our customers' lives better, faster, and more reliably than competitors who treat AI as a feature checkbox. We do this by making **specifications**, **evaluations**, and **customer outcomes** the durable artifacts we manage — and treating code, models, and prompts as the (replaceable) means by which those artifacts get realized. The result is an organization that ships in days what used to take quarters, with measurable quality and a humane culture."

That is the version I would put on the slide. The rest of this repo is what makes it true.
