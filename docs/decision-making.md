# Decision-Making as a Core Engineering Skill

> *"The quality of an organization is the quality of the decisions it makes, divided by the time it takes to make them."*

Most engineering "execution problems" are decision-making problems wearing a disguise. Teams stall not because the work is unclear, but because **who decides, how they decide, and how they live with the decision** is unclear.

In an AI-first world this matters even more. AI raises the **supply of plausible options** to near-infinite. The scarce resource is no longer "an idea" or "a draft" — it is **judgment**: knowing which option is right, which is safe, which can be reversed, and which to push back on.

This doc defines decision-making as a **first-class engineering skill** that we deliberately teach, measure, and reward at every level.

---

## The five questions for every significant decision

Before any decision worth more than ~1 day of engineering time, the decider answers these — out loud, in writing:

1. **What kind of decision is this?** (See [decision types](#decision-types) below.)
2. **Who is the *single* decider?** (Not a committee. Committees inform; individuals decide.)
3. **What is the smallest reversible step that tests the riskiest assumption?**
4. **What would change my mind?** (Pre-commit to the evidence that would cause a reversal.)
5. **When and how will we review whether this was right?**

If a decision-maker cannot answer all five, the decision is not ready to be made. Pushing it to a meeting will not help.

---

## Decision types

Borrowed from Bezos and sharpened by years of operational reality. Every decision falls into one of three buckets, and the *bucket determines the process*.

| Type | Description | Process | Speed |
|---|---|---|---|
| **Type 1 — One-way door** | Hard or impossible to reverse. Wrong choice has lasting cost. | RFC + ARB + senior decider, written rationale, pre-mortem required. | Slow on purpose. |
| **Type 2 — Two-way door** | Reversible within days/weeks at low cost. | Direct decision by the closest informed person. Decision logged, not debated. | Fast on purpose. |
| **Type 3 — Trap door** | *Looks* reversible but isn't (data migrations, public API shapes, hiring, founding team norms). | Treat as Type 1. Be paranoid about misclassification. | Carefully slow. |

> **Most failures are decisions of the wrong type being made with the wrong process.** Type 2 decisions debated for a quarter. Type 1 decisions made in Slack. Type 3 decisions assumed to be Type 2 until the bill arrives.

The job of a senior engineer or manager is to **classify the door first, then choose the process.**

---

## Roles in a decision: DACI

For any non-trivial decision, name the four roles explicitly:

- **D — Driver.** Runs the process. Schedules the pre-mortem. Writes the decision doc.
- **A — Approver.** The *single* person who says yes/no. Accountable to the org for the outcome.
- **C — Contributors.** Provide expertise, data, or affected-team input. Their concerns must be heard, not necessarily heeded.
- **I — Informed.** Need to know after the decision is made.

**There is exactly one Approver.** If you cannot name one, the decision is unowned.

---

## Decision-making rituals we install

### 1. The written one-pager

For any Type 1 or Type 3 decision, the Driver writes a one-pager (or RFC for larger scope) covering:

- **Context** — what is true that makes this decision necessary now.
- **Options** — at least three, including "do nothing" as a real option.
- **Recommendation** — the Driver's recommendation and why.
- **Risks & reversal cost** — what we lose if we're wrong, and how we'd recover.
- **Decision criteria** — what would make us change our mind.
- **Open questions** — what we don't yet know.

The Approver reads the doc *before* the meeting. The meeting is for the Approver to challenge — not to be briefed.

### 2. The pre-mortem

For any Type 1 decision, before approving, run a 30-minute pre-mortem:

> *"It is 6 months from now. This decision went badly. We are in a postmortem. Each person writes down — silently, for 5 minutes — the most likely cause."*

Then read the answers aloud. Pre-mortems surface risks that group discussion suppresses (because people don't want to be the negative voice). They convert "we should have seen this coming" into "we did see this coming and chose anyway."

### 3. Disagree and commit — with the disagreement on the record

Strong opinions, loosely held only works if the opinions were actually *heard*. The pattern:

1. Concerns are stated in writing in the decision doc.
2. The Approver reads them and writes a response.
3. The decision is made.
4. Contributors execute as if it were their own choice — *and* the original concerns stay in the doc, so we can learn whether they were prophetic or noise.

We do not punish dissent, but we also do not let dissent stop the org. The point of capturing dissent is **learning velocity**, not litigation.

### 4. The decision log

Every Type 1 decision goes in a searchable decision log with:

- Date, Driver, Approver, Contributors
- Link to the one-pager / RFC / ADR
- Decision in one sentence
- Review date (when we revisit this)
- Status: open / in-effect / reversed / superseded

Architectural decisions use the [ADR template](../templates/architecture-decision-record.md). Non-architectural decisions (hiring shape, vendor choice, process change, org change, product trade-off) use the [decision record template](../templates/decision-record-template.md).

The point of the log is not bureaucracy. The point is that **two years from now, the next leader can reconstruct *why*.** Most engineering pain is paid by the team that inherits a decision whose reasoning has evaporated.

### 5. Calibrated confidence

Every estimate, prediction, or claim by a senior engineer or leader carries a **confidence number**: "I'm 80% sure we can hit this date." "I'm 60% sure this is the right architecture."

Once a quarter, we look back at the predictions:

- Were the 90%-confidence claims right 90% of the time?
- Were the 50%-confidence claims right ~50% of the time?

This is calibration training, borrowed from forecasting research (Tetlock, *Superforecasting*). Calibration is teachable. Engineers and leaders who go through this practice for a year become measurably better decision-makers — and stop the corrosive cultural pattern of *false certainty rewarded*.

### 6. The "what would change your mind" question

In every architecture review, planning session, and major decision meeting, a standing question:

> *"What evidence — concretely — would cause you to recommend the opposite?"*

If the answer is "nothing," the position is not a decision, it's an identity. We make space for new evidence; we don't make space for unfalsifiable convictions.

---

## Decision-making in an AI-first world

AI changes the *shape* of decision-making in ways we explicitly design for:

### What AI is good at

- **Generating options.** AI can produce 10 plausible architectures in 10 minutes.
- **Summarizing context.** Drafting the one-pager, surfacing prior ADRs, comparing tradeoffs.
- **Stress-testing.** Playing devil's advocate, finding edge cases, drafting the pre-mortem inputs.
- **Drafting decision docs.** The "blank-page tax" disappears.

### What AI is bad at

- **Knowing what kind of door this is.** Type 1 vs Type 2 vs Type 3 requires organizational context AI does not have.
- **Owning the outcome.** Accountability is not a tool feature. The Approver is human.
- **Telling you what *you* believe.** AI tends to mirror back the framing you gave it. (See [critical thinking with AI](critical-thinking-with-ai.md).)
- **Detecting cultural and political constraints.** "Why we can't do that" is often unwritten.

### The discipline

The AI-first decision pattern:

1. Use AI to **expand** the option space and **draft** the doc.
2. Have a human **classify** the door type.
3. Have a human **name** the single Approver.
4. Use AI to **stress-test** the recommendation (red-team, pre-mortem inputs).
5. Have a human **decide** and **own** the outcome.
6. Log the decision — including any AI-generated material — with the human author of record.

> **The most dangerous failure mode is when AI generates a confident recommendation and the human Approver "rubber-stamps" it without engaging the five questions.** That is not a decision. That is a hand-off. The org pays the bill.

This is why decision-making and [critical thinking with AI](critical-thinking-with-ai.md) are *paired* skills in this operating system.

---

## How decision-making shows up across the EOS

| Practice | Doc / Template |
|---|---|
| Architectural decisions | [Architecture review process](architecture-review-process.md), [ADR template](../templates/architecture-decision-record.md) |
| Quarterly priority decisions | [Planning rhythm](planning-rhythm.md), [Quarterly planning template](../templates/quarterly-planning-template.md) |
| Incident decisions (containment, rollback, comms) | [Incident management](incident-management.md) — explicit IC role |
| Hiring decisions | [Hiring process](hiring-process.md) — bar raiser as the single Approver |
| Career & promotion decisions | [Career ladders](career-ladders.md) — calibration committee with named owner |
| Trade-off decisions in product | [Spec template](../templates/spec-template.md) — explicit "tradeoffs accepted" section |
| AI feature ship/hold decisions | [AI feature eval template](../templates/ai-feature-eval-template.md) — explicit rollback criteria |
| Strategy decisions | [One-page strategy template](../templates/one-page-strategy-template.md) — what we're choosing *not* to do |

Decision-making is not a chapter of this operating system. **It is the operating system**, observed from a different angle.

---

## How we teach this

Decision-making is a skill, which means it is teachable, practiced, and measured.

- **In onboarding:** every new engineer reads this doc and the [critical thinking with AI](critical-thinking-with-ai.md) doc in their first week.
- **In 1:1s:** a recurring prompt — *"What's a decision you're stuck on? Let's classify the door, name the Approver, and identify the pre-mortem."*
- **In the [career ladder](career-ladders.md):** at IC5/Staff and above, *decision quality and decision velocity* are explicit dimensions of the rubric. We promote people who make our org's decisions better.
- **In leadership offsites:** quarterly calibration review of predictions made the previous quarter. Public, honest, blameless ([operating principles](operating-principles.md)).
- **In retros:** when something went wrong, the question is not "who messed up" but *"which of the five questions did we skip, and why?"*

---

## Anti-patterns to name and kill

- **Decision by attendance.** Whoever showed up to the meeting decided. The Approver was never named.
- **Decision by escalation theater.** Manager loops the VP not because the VP needs to decide but to share the blame.
- **Decision by procrastination.** Not deciding *is* a decision — usually the worst one.
- **Decision by AI.** A model recommended it; the human "approved" without engaging. (See [AI policy](ai-assisted-development-policy.md).)
- **Decision by consensus.** Everyone agreed because everyone diluted the proposal until it was meaningless.
- **Decision by HiPPO** (Highest-Paid Person's Opinion). Strong opinions trump evidence because rank trumps argument.

Naming these out loud, in meetings, in writing, is how we kill them. Silence preserves them.

---

## Further reading

- Annie Duke — *Thinking in Bets*, *How to Decide* — the gold standard on separating decision quality from outcome quality.
- Daniel Kahneman — *Thinking, Fast and Slow*; Kahneman, Sibony, Sunstein — *Noise* — cognitive biases and the variance of human judgment.
- Philip Tetlock — *Superforecasting* — calibrated confidence, the IARPA forecasting tournaments.
- Jeff Bezos — [2015 Shareholder Letter](https://www.aboutamazon.com/news/company-news/2016-letter-to-shareholders) — Type 1 / Type 2 doors, high-velocity decision making.
- Will Larson — [*An Elegant Puzzle*](https://lethain.com/elegant-puzzle/) — decision-making in engineering organizations specifically.
- Gary Klein — [*Performing a Project Premortem*](https://hbr.org/2007/09/performing-a-project-premortem) (Harvard Business Review, 2007) — the canonical pre-mortem reference.
- Atlassian — [DACI decision-making framework](https://www.atlassian.com/team-playbook/plays/daci) — a clean, free reference for the role model used here.
