# Code Review

> Code review is the single highest-leverage moment in the engineering process: it is where defects are caught, mentorship happens, design is debated, and the team's standards are continuously calibrated. In an AI-first org, it is also the gate where AI-generated code becomes human-owned code.

---

## Purpose

You can review a PR — your peer's, a senior's, a junior's, or one drafted by AI — and leave it better than you found it: catching real defects, improving design, sharing context, and helping the author grow, without becoming a bottleneck.

---

## Why it matters in an AI-first org

- The volume of code is going up; the cost of low-quality review is going up with it.
- AI-generated PRs are *plausible by default*. The reviewer is the place where plausibility meets verification.
- Code review is one of the few places where mentorship happens at scale. Stop doing it well and the junior pipeline atrophies.
- Tone in code review is a recruiting and retention signal. Toxic reviews are a top-3 reason people leave teams.

---

## The practice

### As the author (before review)

- **Self-review your diff first.** Read it as if you're the reviewer. You'll catch half your own issues and shrink the review for everyone else.
- **Write the PR description as a mini-spec.** What problem, what change, what's intentionally out of scope, what to look at carefully, how it was tested. A two-minute write saves twenty minutes of reviewer time.
- **Keep PRs small.** < 400 lines is the well-documented sweet spot. Big PRs get rubber-stamped or sit forever; both are worse than smaller, sequential PRs.
- **Mark AI-generated portions.** Per the [AI policy](../docs/ai-assisted-development-policy.md). Reviewers should know what was generated so they review it accordingly.
- **Run the tests, lint, types yourself.** Don't burn reviewers' time on what CI would have told you.
- **Pre-empt the obvious questions** in the description: "why this approach vs the existing X helper", "this is intentionally not handling case Y because…"

### As the reviewer

- **Triage first.** What is this PR doing, at what level of risk? A typo fix, a refactor, and a new public API need different review depths.
- **Review in layers:**
  1. **Correctness** — does it do what it claims? edge cases, error paths, concurrency, security.
  2. **Design** — is this the right shape? does it fit the system? are there hidden coupling / future-pain choices?
  3. **Readability** — names, structure, comments where reasoning isn't obvious from code.
  4. **Tests** — do they actually exercise the change? are they meaningful or theater?
  5. **Style / nits** — last; mostly delegated to linters and formatters.
- **Explicitly review AI-generated portions for the AI failure modes:** hallucinated APIs that don't exist, security anti-patterns that look idiomatic, plausible-but-wrong concurrency, copy-pasted-from-elsewhere licensing concerns, missing error handling that the original prompt didn't ask about.
- **Run the code where it matters.** Reading is not verifying. For non-trivial changes, pull the branch.
- **Ask, don't assert, on judgment calls.** "What made you pick the linked-list here?" beats "This should be a hashmap." You may be missing context.
- **Distinguish blocking from non-blocking.** Prefix `nit:`, `optional:`, `question:`, `blocking:` so the author knows what they have to address. Reviewers who treat every comment as blocking are unreviewable.
- **Approve when the bar is met**, not when the code is perfect. Perfect is the enemy of shipped, and the enemy of the next PR which will iterate.
- **Be kind, be specific, be on time.** Same-day on small PRs, < 24h on most, < 48h on the largest. Latency is the single most-complained-about reviewer behavior.

### Norms the team agrees on

- **Two-person review for high-risk paths** (auth, payments, data deletion, regulated). One reviewer otherwise.
- **Author merges**, not reviewer. Approval ≠ obligation to merge if author isn't ready.
- **Stale PRs (> 5 days) get a ping or are closed.** Stale PRs are a quiet morale tax.
- **Disagreements escalate explicitly.** If author and reviewer can't agree, name a tiebreaker (tech lead, Staff+, ADR). Don't let it die in comments.

---

## Drills

- **Daily — the self-review pass.** Spend 5 minutes reviewing your own diff before publishing. Track for two weeks how often you catch real issues.
- **Weekly — the small-PR rule.** Aim for every PR under 400 lines. When tempted to go over, ask "can this be split?"
- **Weekly — the review-quality retro.** Look at one of your reviews from the week. Was a comment kind? specific? actionable? On time?
- **Monthly — review a senior's PR.** Reviewing up-level is the fastest way to grow. You'll learn things their PR description doesn't say.
- **Monthly — review your own old code.** Pick a PR you wrote 6 months ago. What would you flag if you were reviewing it now? Calibrates growth.
- **With a peer — paired review.** Sit together for one review. The patterns you each don't know you have become visible.
- **For AI-heavy work:** maintain a personal list of "things the model gets wrong in our codebase." Use it as a checklist on AI-generated PRs.

---

## Common failure modes

- **Rubber-stamping AI PRs.** LGTM in 30 seconds. You now co-own the bugs without seeing them.
- **Bikeshedding.** A 40-comment thread about variable names while a real concurrency bug ships. Spend reviewer attention on what matters.
- **The hostile review.** Snark, condescension, "this is fundamentally wrong." Even when technically right, the relational cost makes future reviews worse.
- **Latency.** A reviewer who takes 4 days kills throughput across the team. This is a management issue, not just a habit.
- **Review-as-gatekeeping.** Senior reviewer who blocks everything to "maintain quality" — actually maintains personal control. Recognized in good orgs as a problem.
- **Approve-and-leave.** Approval without any comment on a meaningful change. Did you actually review it?
- **Inconsistent bar.** Same kind of issue blocking for one author, ignored for another. Erodes trust in the process.
- **Author defensiveness.** Arguing every comment instead of taking the signal. Same dynamic as feedback: see [giving-and-receiving-feedback.md](giving-and-receiving-feedback.md).
- **Hiding AI-generated changes.** Per the [AI policy](../docs/ai-assisted-development-policy.md), this is a process violation. Disclosure is the deal.

---

## Tune for your context

- **High-risk domains** (security, financial, life-critical): require two reviewers, mandate a security checklist, slow down on critical paths.
- **Early-stage / small teams:** smaller PR latency targets matter more; you have fewer reviewers, so a slow one stalls everything.
- **Distributed teams:** "next business day" beats "synchronous review" but requires great PR descriptions. The author's investment in writing the PR matters more.
- **Heavy AI codegen:** lengthen review time per line generated; the cost of skipping is asymmetric.
- **Junior-heavy teams:** weight mentorship higher; weight scope-of-comments lower (don't fix every nit; pick the 2–3 most valuable).

---

## Further reading

- **Google** — [Engineering Practices: Code Review Developer Guide](https://google.github.io/eng-practices/review/) — the most-cited public standard.
- **Microsoft Research / others** — research on [optimal PR size](https://smallbusinessprogramming.com/optimal-pull-request-size/) (~200–400 lines; defect detection drops sharply after).
- **SmartBear** — [code-review research](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/) — empirical findings from large-scale industry data.
- **Michaela Greiler** — [michaelagreiler.com](https://www.michaelagreiler.com/) — long-running research and writing specifically on code review.
- **Joel Spolsky** — *The Joel Test*, item 9 — reviews as a baseline expectation.
- **Conventional Comments** — [conventionalcomments.org](https://conventionalcomments.org/) — `nit:`, `question:`, `suggestion:` labels for review hygiene.
