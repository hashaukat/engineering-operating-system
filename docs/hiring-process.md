# Hiring Process

> Hiring is the single highest-stakes decision an engineering leader makes. Every hire either raises the median or lowers it. The job of the process is to make raising the median the *default outcome*.

## Principles

1. **Hire for the team you are becoming, not the team you have.** A 40-person org hires very differently from a 120-person org. Define the topology first, the role second, the candidate third.
2. **Bar raisers, not bar matchers.** Every hire should make the group they join stronger.
3. **Calibrate the loop, not the candidate.** When loops drift, it is almost always our problem, not the market's.
4. **Move fast or get out of the way.** Top candidates are off the market in 10–14 days. A loop that takes 6 weeks is a loop that loses.
5. **No surprises in compensation.** Bands published internally; ranges shared with candidates early.

## Loop design

A standard senior IC loop has **5 modules**, ~5 hours of candidate time.

| Module | Duration | Signal | Interviewer |
|---|---|---|---|
| Recruiter screen | 30 min | Motivation, comp, logistics | Recruiter |
| Hiring manager screen | 45 min | Scope fit, motivation, red flags | HM |
| Coding / system work | 75 min | How they actually build | 2 ICs |
| System design | 60 min | How they reason about ambiguity at scale | Staff+ engineer |
| Values / leadership | 45 min | Collaboration, conflict, ownership | Cross-team interviewer |
| Bar raiser | 45 min | Calibration across the org | Trained bar raiser, not on the team |

**The bar raiser has veto power.** They are not the team. Their job is the *org*.

## AI in interviewing

We do not pretend candidates will work without AI. So:

- **One loop module is explicitly AI-allowed.** Candidate uses Copilot or equivalent. We evaluate *judgment*: what they accepted, what they edited, how they validated.
- **One module is AI-not-allowed.** A small, contained problem where we see how they think unaided.
- **The system design and leadership modules are AI-irrelevant** — we are looking at reasoning, not output.

This mirrors the actual job.

## Debrief

Within **24 hours of the last interview**:

1. Each interviewer submits a written written report *before* reading anyone else's. No "I agree with X" allowed.
2. The hiring manager runs a 30-min debrief. Disagreements are aired; the bar raiser has the final escalation.
3. Decision: **Strong Hire / Hire / No Hire / Strong No Hire.** A single "Strong No Hire" requires explicit override by the hiring manager *and* the bar raiser to proceed.
4. Reference checks for Staff+ and EM+ roles before offer.

## Offer & close

- **Same-day verbal** once decision is made. Written offer within 48h.
- **Hiring manager owns the close**, not the recruiter. The HM calls the candidate within 24h of the offer.
- **No exploding offers.** Candidates get at least 5 business days to decide.
- **Counter-offer policy** stated to recruiters up front: we make our best offer, we don't bidding-war.

## Onboarding (the other half of hiring)

A great loop and a bad onboarding cancels out. The standard:

- **Day 0:** equipment ready, accounts provisioned, buddy assigned.
- **Day 1:** team welcome, environment running locally, first PR merged (a trivial one — the point is to validate the path).
- **Week 1:** completes onboarding checklist with buddy; meets all team members 1:1.
- **Week 2:** first non-trivial PR in production.
- **Day 30:** first meaningful feature or fix shipped; 30-day check-in with EM and HM.
- **Day 90:** "is this working" review; both sides decide if there is anything to adjust.

Time-to-first-prod-merge is on the [scorecard](metrics-scorecard.md). Target: < 14 days.

## Sourcing

- **Referrals are the highest-yield channel** at every level. Pay generously; respond to every referral within 48h.
- **Public talks, OSS, conference presence** are sourcing investments, not vanity.
- **Build a "we want to talk to you in 6 months" list.** Engineering leadership maintains this personally.

## What I refuse

- Loops longer than 5 onsite modules.
- Take-home assignments over 4 hours of candidate time.
- "Cultural fit" as a debrief comment. Replace with specific value-based observations.
- Hiring against a hard deadline ("we have to hire someone by end of Q"). The cost of a bad hire dwarfs the cost of a slow hire.
- Skipping the bar raiser because "we really like this one."
