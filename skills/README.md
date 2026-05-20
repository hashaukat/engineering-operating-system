# Skills — The Tunable Practice Library

> The Engineering Operating System tells you *what* the org does. The skills library is *how each person gets good at the work the OS demands*.

This folder is a library of **essential, generic skills** that an AI-first engineering organization depends on. They are written to be **tuned**, not adopted verbatim — your domain, stage, team size, and customer base will change the specifics. The *shape* of each skill — the practice, the failure modes, the drills — is portable.

---

## How this fits the rest of the EOS

| The EOS doc says... | The skill explains how... |
|---|---|
| [decision-making.md](../docs/decision-making.md) — every decision has a named Approver and rationale | An individual *thinks*, *writes*, and *defends* a decision well |
| [spec-driven-development.md](../docs/spec-driven-development.md) — specs are the durable artifact | An engineer *writes* a spec someone else (or an AI) can build from |
| [incident-management.md](../docs/incident-management.md) — blameless, learning postmortems | An IC, an IC-on-call, and a commander actually *run* an incident |
| [hiring-process.md](../docs/hiring-process.md) — calibrated loops, bar raiser | An interviewer *evaluates* candidates consistently |
| [career-ladders.md](../docs/career-ladders.md) — IC and management tracks | A manager *coaches* growth and *gives* feedback that lands |
| [critical-thinking-with-ai.md](../docs/critical-thinking-with-ai.md) — question, verify, push back | An individual *practices* the discipline daily |

If the docs are the policy, the skills are the muscle memory.

---

## How each skill is structured

Every skill in this folder follows the same shape, so you can scan, lift, and tune:

1. **Purpose** — what good looks like, in one paragraph.
2. **Why it matters in an AI-first org** — what's different now, and what's the same.
3. **The practice** — concrete, observable behaviors. Things you'd see if you watched someone good do this.
4. **Drills** — how to develop the skill deliberately. Solo, with peers, with manager.
5. **Common failure modes** — how this skill goes wrong, named precisely.
6. **Tune for your context** — the dials to turn for your org's stage, size, and domain.
7. **Further reading** — named authors and canonical sources.

---

## The skills

### Foundational — everyone, every level

- [critical-thinking-and-judgment.md](critical-thinking-and-judgment.md)
- [working-with-ai.md](working-with-ai.md)
- [technical-writing.md](technical-writing.md)
- [giving-and-receiving-feedback.md](giving-and-receiving-feedback.md)

### Engineering craft — every engineer, weighted by level

- [writing-specs.md](writing-specs.md)
- [code-review.md](code-review.md)
- [debugging.md](debugging.md)
- [incident-response.md](incident-response.md)
- [estimation-and-forecasting.md](estimation-and-forecasting.md)

### Management craft — every manager, M3 and up

- [running-one-on-ones.md](running-one-on-ones.md)
- [coaching-and-growth.md](coaching-and-growth.md)
- [hiring-and-interviewing.md](hiring-and-interviewing.md)
- [running-effective-meetings.md](running-effective-meetings.md)

### Leadership craft — senior managers, directors, executives

- [strategic-thinking.md](strategic-thinking.md)
- [prioritization-and-saying-no.md](prioritization-and-saying-no.md)
- [influence-and-executive-communication.md](influence-and-executive-communication.md)

---

## How to use this library

**As an individual:**
- Pick two skills per quarter to deliberately practice. More than two is wishful thinking.
- Use the **Drills** section in your 1:1s — most of them are designed to be done with a manager or peer.
- Score yourself honestly against the **Common failure modes**; that's the leading indicator.

**As a manager:**
- Map each person on your team to the 2–3 skills most important for their next level ([career-ladders.md](../docs/career-ladders.md)).
- Use the relevant skill doc as the **shared language** in your 1:1s and reviews. "What practice on the writing-specs skill did you do this sprint?" is a better question than "How's it going?"
- Coach against the *practice* and the *drills*, not against vague impressions.

**As a leader installing the EOS:**
- Decide which 6–8 skills are **org-wide expectations** for everyone. The other ~10 are role-specific.
- Build the **Drills** into onboarding, into 1:1 cadences, and into promotion criteria.
- Revisit the **Tune for your context** sections quarterly — your stage will change what "good" looks like.

---

## How to tune

This library is deliberately written for the **median software org in 2026**, AI-first by default. To tune:

- **Stage:** earlier-stage orgs lean harder on individual judgment and lighter on process. Add structure as the org grows; don't front-load it.
- **Domain:** regulated industries (health, finance, gov) tighten the *gates* in most skills (specs, code review, incident response). Consumer / experimentation orgs loosen them.
- **Team distribution:** remote / async-heavy orgs lean harder on the *writing* skills (specs, technical writing, executive communication).
- **AI maturity:** orgs newer to AI should over-invest in `critical-thinking-and-judgment` and `working-with-ai` for two quarters before scaling everything else.

If a skill doesn't match how you operate, **edit it in-place**. That's the point.

---

## A note on what's *not* here

This library is the **generic core**. It deliberately omits:

- Language- or framework-specific skills (React, Go, Kubernetes) — those belong in your internal learning paths.
- Domain expertise (fintech, healthcare, ML research) — those are role-specific.
- Soft-skill catch-alls ("be a good teammate") — they aren't practicable; the skills here are.

If you need one of those, build it in your org's flavor and link it from here.
