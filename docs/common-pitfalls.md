# Common Pitfalls — The Antidote Map

> *"You can't 'fix' people, but you can fix systems and processes to better support people making the right choices when designing and maintaining complex systems."* — Google SRE Book, [Postmortem Culture](https://sre.google/sre-book/postmortem-culture/)

Most engineering-org failure modes are not novel. They have been described, post-mortemed, and written about for decades — by Will Larson, Camille Fournier, Charity Majors, Lara Hogan, Gergely Orosz, Patrick Kua, the DORA/Accelerate research team, and the authors of *Team Topologies*, among others.

This document catalogs **48 well-known, avoidable pitfalls** that quietly destroy engineering organizations, grouped into 9 categories. For each, it points to the doc, template, or example in this Engineering Operating System (EOS) that is specifically designed to prevent it.

Read this as a **leading indicator checklist**: if you recognize your org in three or more pitfalls in any single category, that's the section of the EOS to invest in next.

---

## 1. Strategy & focus

Most "execution problems" are strategy problems wearing a disguise.

1. **No written strategy, only a roadmap.** Roadmaps describe *what*; strategy describes *why this and not that*. Without a written strategy, every quarter becomes a re-litigation of priorities. → [engineering-strategy.md](engineering-strategy.md), [one-page-strategy-template.md](../templates/one-page-strategy-template.md)
2. **Strategy that is really a wish list.** "Be the best, fastest, most reliable, most loved" is not a strategy — it's a vibe. A real strategy names the constraint and the trade-off being chosen. → [engineering-strategy.md](engineering-strategy.md)
3. **Confusing the 3-horizon mix.** Treating Horizon 1 (run the business), Horizon 2 (scale the next bet), and Horizon 3 (explore the frontier) as one undifferentiated backlog. Horizon 3 always loses to Horizon 1's urgency. → [engineering-strategy.md](engineering-strategy.md), [mock-q3-engineering-plan.md](../examples/mock-q3-engineering-plan.md)
4. **Mistaking AI adoption for AI strategy.** Buying Copilot seats is procurement. An AI strategy specifies *which workflows* you're rewiring, *what evidence* qualifies a feature as shippable, and *how you measure value, not activity*. → [ai-first-stance.md](ai-first-stance.md), [ai-assisted-development-policy.md](ai-assisted-development-policy.md)

---

## 2. Org design & topology

Conway's Law is undefeated. Your architecture will resemble your org chart, whether you planned it or not.

5. **Reorging without a thesis.** Reorgs without a stated hypothesis ("we expect this to reduce X handoff and increase Y flow") are just shuffling. They incur all the cost of change with none of the learning. → [org-design.md](org-design.md)
6. **Stream-aligned teams with platform responsibilities glued on.** When a product team also owns shared infra, every roadmap conversation becomes a tax debate. *Team Topologies* names four team types for a reason. → [team-topologies.md](team-topologies.md), [sample-platform-team-charter.md](../examples/sample-platform-team-charter.md)
7. **Platform team as ticket queue.** Treating the platform team as an internal IT helpdesk instead of as a product team with users, SLAs, and a roadmap. → [team-topologies.md](team-topologies.md), [sample-platform-team-charter.md](../examples/sample-platform-team-charter.md)
8. **Cognitive load ignored.** Stacking 11 services, 4 languages, and 3 cloud accounts onto a 6-person team and then wondering why velocity collapsed. *Team Topologies* makes cognitive load a first-class design constraint. → [team-topologies.md](team-topologies.md), [org-design.md](org-design.md)
9. **Manager-to-engineer ratios outside 1:5–1:8.** Below that, managers become bottlenecks or micromanagers; above it, ICs feel unsupported and growth stalls. → [org-design.md](org-design.md), [career-ladders.md](career-ladders.md)

---

## 3. Planning & execution

The point of planning is the *plan-making*, not the plan.

10. **Annual plans no one revisits.** Plans built in October for the next 12 months, then never opened again until the next October. The annual artifact should be a *living* north star, not a tombstone. → [planning-rhythm.md](planning-rhythm.md), [quarterly-planning-template.md](../templates/quarterly-planning-template.md)
11. **Quarterly planning that ignores capacity for KTLO and incidents.** Booking 100% of engineer time against features and being shocked when neither features nor reliability ship. → [planning-rhythm.md](planning-rhythm.md), [execution-model.md](execution-model.md)
12. **Skipping discovery and going straight to JIRA.** Without a discovery step, you build the right solution to the wrong problem — at full velocity. → [execution-model.md](execution-model.md), [spec-driven-development.md](spec-driven-development.md)
13. **No durable spec artifact.** "We discussed it in standup" is not a spec. Without a written spec, the work cannot be parallelized, reviewed by domain experts, or handed to AI tooling. → [spec-driven-development.md](spec-driven-development.md), [spec-template.md](../templates/spec-template.md), [sample-spec-checkout-idempotency.md](../examples/sample-spec-checkout-idempotency.md)

---

## 4. Measurement

What you measure becomes what you optimize. Measure the wrong things and people will dutifully optimize them.

14. **Single-metric tyranny.** Picking *one* metric (deploy frequency, lines of code, story points) and watching it get gamed within 90 days. Goodhart's Law is a tax on naïveté. → [productivity-measurement.md](productivity-measurement.md), [metrics-scorecard.md](metrics-scorecard.md)
15. **Productivity ≠ business outcome.** Improving DORA without improving customer outcomes (CSAT, NPS, time-to-value) just means you're shipping faster things customers don't want. → [productivity-measurement.md](productivity-measurement.md), [metrics-scorecard.md](metrics-scorecard.md), [sample-okr-scorecard.md](../examples/sample-okr-scorecard.md)
16. **Per-individual productivity dashboards.** AI-usage rankings, lines-of-code leaderboards, PR-count leaderboards. These destroy collaboration, distort behavior, and (per DORA, SPACE, and DX Core 4 research) do not predict org performance. → [productivity-measurement.md](productivity-measurement.md), [ai-assisted-development-policy.md](ai-assisted-development-policy.md)
17. **No customer-value metric in the scorecard.** A scorecard with DORA + SPACE but no CSAT, NPS, CES, retention, or time-to-value is a *delivery* scorecard, not a *value* scorecard. → [metrics-scorecard.md](metrics-scorecard.md), [sample-okr-scorecard.md](../examples/sample-okr-scorecard.md)

---

## 5. People, career, and hiring

The most expensive failure modes are the human ones, because they compound.

18. **Management as the only promotion path.** Forcing your best ICs into management to get a raise. They become reluctant managers, you lose your strongest builder, and the team gets a worse leader. (See Charity Majors, *[The Engineer/Manager Pendulum](https://charity.wtf/2017/05/11/the-engineer-manager-pendulum/)*: "Management is not a promotion, management is a change of profession.") → [career-ladders.md](career-ladders.md)
19. **No Staff+ scope clarity.** Staff and Principal engineers without explicit scope and sponsorship drift into "senior senior engineer" — high-paid IC4s with imposter syndrome. → [career-ladders.md](career-ladders.md), [staff-engineer-scope-template.md](../templates/staff-engineer-scope-template.md)
20. **Hiring loops with no calibration.** Every interviewer freelancing their own bar. Result: hires correlate with interviewer mood, not with role success. → [hiring-process.md](hiring-process.md)
21. **No bar raiser, no veto.** Without a hire/no-hire owner empowered to say no over a hiring manager who is desperate to fill, urgency wins and quality erodes. → [hiring-process.md](hiring-process.md)
22. **Hiring without an AI module — or only with one.** If your interview never tests how a candidate works with AI tools, you're hiring for the 2018 job. If it *only* tests AI-assisted work, you're hiring people who cannot reason without a copilot. → [hiring-process.md](hiring-process.md), [ai-first-stance.md](ai-first-stance.md)
23. **No team-health signal.** Discovering attrition risk via resignation emails. A lightweight quarterly pulse catches drift months earlier. → [team-health-survey.md](../templates/team-health-survey.md), [operating-principles.md](operating-principles.md)

---

## 6. Reliability & engineering practice

The technical pitfalls are well-documented. The reason they recur is cultural.

24. **Blameful postmortems.** Naming an individual as root cause guarantees the next incident gets hidden, not learned from. Google's SRE book traces blameless culture back to healthcare and avionics for the same reason. → [incident-management.md](incident-management.md), [postmortem-template.md](../templates/postmortem-template.md), source: [sre.google/sre-book/postmortem-culture](https://sre.google/sre-book/postmortem-culture/)
25. **Postmortems with no follow-through.** A postmortem doc nobody re-reads. Per Google SRE: *"No postmortem left unreviewed."* Action items need owners, due dates, and prioritization on real backlogs. → [incident-management.md](incident-management.md), [postmortem-template.md](../templates/postmortem-template.md)
26. **Architecture decisions made in Slack.** No ADR, no RFC, no durable record of *why*. Six months later, the rationale is gone and the next team rewrites it. → [architecture-review-process.md](architecture-review-process.md), [architecture-decision-record.md](../templates/architecture-decision-record.md)
27. **Architecture Review Board as a gate, not a service.** ARB that *approves* designs becomes a queue and a bottleneck. ARB that *consults on* designs accelerates and educates. → [architecture-review-process.md](architecture-review-process.md)
28. **No SLOs.** Without explicit service level objectives, every reliability conversation is a feeling. With SLOs (and error budgets), it becomes a number both eng and product agree on. → [metrics-scorecard.md](metrics-scorecard.md), [incident-management.md](incident-management.md)

---

## 7. AI-specific

These are the new ones. They are also the most expensive in 2026.

29. **Shipping AI features without an eval harness.** No offline benchmark, no LLM-judge, no human review, no red-team. The first regression ships to production and you find out via Twitter. → [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md), [spec-driven-development.md](spec-driven-development.md)
30. **No rollback criteria for AI features.** Knowing how to launch but not how to retreat. Quality drift in LLM-backed features is silent until it isn't. → [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md), [incident-management.md](incident-management.md)
31. **No AI usage policy at all.** Engineers paste customer PII into public model endpoints because nobody told them what's in/out of bounds. → [ai-assisted-development-policy.md](ai-assisted-development-policy.md)
32. **AI policy that's just a prohibition.** "No AI tools" in 2026 is the equivalent of "no internet at work" in 2003. It doesn't stop use; it stops the *governed* use. → [ai-assisted-development-policy.md](ai-assisted-development-policy.md), [ai-first-stance.md](ai-first-stance.md)
33. **Measuring AI adoption by seat count.** Seats activated is not a value metric. Time-saved, defect-rate-on-AI-authored-PRs, cycle-time-on-AI-assisted-stories, and customer outcomes are. → [productivity-measurement.md](productivity-measurement.md), [ai-assisted-development-policy.md](ai-assisted-development-policy.md)
34. **Specs treated as throwaway.** Spec-driven development is the unlock for AI-augmented engineering: a written spec is the highest-leverage artifact an AI agent can consume. Treating specs as "documentation we'll do later" forfeits the leverage. → [spec-driven-development.md](spec-driven-development.md), [spec-template.md](../templates/spec-template.md)

---

## 8. Decision-making & AI gullibility

The newest — and least-discussed — category. These are the failure modes that quietly compound in an AI-first org until something breaks publicly.

35. **No named Approver.** "We" decided. Which means nobody decided, and nobody is accountable when the decision turns out to be wrong. Every significant decision has *one* Approver. → [decision-making.md](decision-making.md), [decision-record-template.md](../templates/decision-record-template.md)
36. **Confusing Type 1 and Type 2 decisions.** Debating a reversible decision for a quarter, or making an irreversible one in Slack. The bucket determines the process; misclassification is the most common cause of either over-deliberation or under-deliberation. → [decision-making.md](decision-making.md)
37. **No pre-mortem on Type 1 decisions.** Big bets made without anyone asked "how will this fail?" Pre-mortems surface what group dynamics suppress. → [decision-making.md](decision-making.md)
38. **No decision log.** Two years later, the next leader inherits the architecture, the process, the org shape — with no record of *why*. They rebuild the same wrong thing because the reasoning evaporated. → [decision-making.md](decision-making.md), [architecture-decision-record.md](../templates/architecture-decision-record.md), [decision-record-template.md](../templates/decision-record-template.md)
39. **Rubber-stamping AI recommendations.** A confident model suggestion + a busy human Approver = a decision the org made without anyone actually thinking. The cost is paid in production, by customers, on someone's pager. → [critical-thinking-with-ai.md](critical-thinking-with-ai.md), [decision-making.md](decision-making.md)
40. **Sycophancy mistaken for correctness.** The model agreed with your framing, so you concluded you were right. Modern LLMs are empirically sycophantic; we design around it by prompting for dissent and pushing back on unqualified agreement. → [critical-thinking-with-ai.md](critical-thinking-with-ai.md)
41. **Unverified AI citations and APIs.** Numbers, papers, library methods quoted from a model and used as evidence — without a single click to confirm they exist. Hallucinated citations are a known, daily failure mode. → [critical-thinking-with-ai.md](critical-thinking-with-ai.md), [ai-assisted-development-policy.md](ai-assisted-development-policy.md)
42. **Shrinking pushback over time.** Engineers gradually challenge AI less because it's *usually* right. Then the unusual cases — which are the only ones that matter — ship unread. → [critical-thinking-with-ai.md](critical-thinking-with-ai.md)

---

## 9. Leadership behaviors

The pitfalls leaders most often blame on "the org" are usually the leader's own.

43. **The hero CTO.** Every important decision routes through one person. The org's throughput is capped at that person's calendar, and succession is impossible. → [operating-principles.md](operating-principles.md), [career-ladders.md](career-ladders.md)
44. **Status-meeting theater.** Weekly meetings whose only output is more meetings. The cure: standing written updates, async by default, meetings reserved for decisions. → [planning-rhythm.md](planning-rhythm.md), [operating-principles.md](operating-principles.md)
45. **No operating principles, or principles that are wallpaper.** Principles that nobody can recite and nobody uses in actual decisions. Principles must be invoked when trading off, or they're decoration. → [operating-principles.md](operating-principles.md)
46. **Treating engineering as a cost center.** Reporting engineering only as headcount and burn, never as throughput, reliability, and customer-value creation. Boards then optimize for the only thing they can see — cost. → [metrics-scorecard.md](metrics-scorecard.md), [productivity-measurement.md](productivity-measurement.md)
47. **Optimizing for activity over outcomes.** Velocity, story points, PR counts. The DORA program has, year over year, shown that *outcome* metrics (delivery + reliability + org performance) are what predict business results. → [productivity-measurement.md](productivity-measurement.md), source: [DORA Research Program](https://dora.dev/research/)
48. **No learning loop.** Quarterly reviews that celebrate hits and bury misses. Without an honest retrospective, the org learns nothing and the same pitfalls return — which is why this document exists. → [planning-rhythm.md](planning-rhythm.md), [incident-management.md](incident-management.md), [operating-principles.md](operating-principles.md)

---

## How to use this list

- **For self-assessment:** Score each pitfall 0 (we don't do this) / 1 (we sometimes do this) / 2 (we routinely do this). Anything ≥1 in three pitfalls of the same category indicates a systemic gap, not a one-off.
- **For onboarding new leaders:** Hand this to a new VP/director in their first week alongside [operating-principles.md](operating-principles.md). Ask them which 5 they've personally caused or witnessed. The conversation calibrates faster than any leveling guide.
- **For board / exec reviews:** When asked "what could go wrong with the eng org?", this is the honest answer in 48 bullets — and the EOS column shows the standing prevention mechanism for each.

---

## Further reading

The pitfalls and antidotes catalogued here draw on a public body of work. The most useful sources:

- **Will Larson** — [*An Elegant Puzzle*](https://lethain.com/elegant-puzzle/), [*Staff Engineer*](https://staffeng.com/), and [lethain.com](https://lethain.com/) — engineering strategy, org design, Staff+ archetypes.
- **Camille Fournier** — *The Manager's Path* — engineering leadership progression from tech lead to CTO.
- **Charity Majors** — [charity.wtf](https://charity.wtf/), particularly *[The Engineer/Manager Pendulum](https://charity.wtf/2017/05/11/the-engineer-manager-pendulum/)* — career path, ops culture, observability.
- **Lara Hogan** — [larahogan.me](https://larahogan.me/) — manager skills, feedback, resilience.
- **Gergely Orosz** — [The Pragmatic Engineer](https://newsletter.pragmaticengineer.com/) and *The Software Engineer's Guidebook* — industry patterns, leveling, comp.
- **Patrick Kua** — [patkua.com](https://www.patkua.com/) — tech leadership, learning organizations.
- **Forsgren, Humble, Kim** — *Accelerate* and the ongoing [DORA Research Program](https://dora.dev/research/) — the empirical case for the four key metrics and the capabilities that drive them.
- **Skelton & Pais** — *Team Topologies* and [teamtopologies.com/key-concepts](https://teamtopologies.com/key-concepts) — four team types, three interaction modes, cognitive load.
- **Forsgren, Storey, Maddila, Zimmermann, Houck, Butler** — *[The SPACE of Developer Productivity](https://queue.acm.org/detail.cfm?id=3454124)* (ACM Queue, 2021) — the case against single-metric productivity.
- **Google SRE Book** — [sre.google](https://sre.google/sre-book/table-of-contents/), particularly [Postmortem Culture](https://sre.google/sre-book/postmortem-culture/) — blameless postmortems, SLOs, error budgets.
- **DX Core 4** — [getdx.com/research/measuring-developer-productivity-with-the-dx-core-4](https://getdx.com/research/measuring-developer-productivity-with-the-dx-core-4/) — combining DORA + SPACE + DevEx into four scorecard dimensions.

If you see a pitfall recurring in your org that isn't on this list, please open a PR. The point of an operating system is that it learns.
