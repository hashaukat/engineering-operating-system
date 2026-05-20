# Operating Principles

> Principles exist so that decisions are consistent without consultation. If two engineers in different teams hit the same fork in the road, they should choose the same path for the same reason.

These are the 10 principles I install and defend.

---

### 1. Customers are the only scoreboard that matters
Internal metrics serve customer outcomes or they are vanity. When in doubt, ask: *what changes for the customer?*

### 2. Default to writing it down
Verbal decisions decay. Written decisions compound. ADRs, RFCs, postmortems, one-pagers — the cost of writing is paid once; the cost of *not* writing is paid forever.

### 3. Make the right thing the easy thing
If we want secure code, the secure path must be the shortest path. Platforms, paved roads, and defaults are how culture scales — not exhortation.

### 4. Reliability is a feature, not a department
SLOs belong in product planning. Error budgets gate feature work. On-call is a craft, not a punishment.

### 5. Optimize for the next decision, not this one
Architectures, processes, and orgs should leave the *next* leader with more options, not fewer. Reversible decisions get made fast; irreversible ones get made carefully.

### 6. Strong opinions, loosely held — and *written down*
Disagree and commit only works if the disagreement was actually heard. Every significant decision has an author of record.

### 7. AI is a power tool, not an oracle
Use AI to raise the floor of every engineer's productivity. Never delegate accountability. Every AI-assisted output passes through the same review, test, and security gates as human output. See [AI policy](ai-assisted-development-policy.md).

### 8. Promote the behavior, not just the result
We reward engineers who *make the org better*, not only those who ship the loudest. Mentoring, paved roads, and incident-learning count.

### 9. Teams are the unit of delivery
We design work, planning, and architecture around durable teams ([team topologies](team-topologies.md)) — not projects, not individuals. Resourcing a team is a multi-quarter commitment.

### 10. Calm is a competitive advantage
Heroics signal a broken system. Sustainable pace, on-call rotations that respect humans, and humane escalation paths produce better software than panic ever has.

---

## How principles are used

- **In reviews:** "Which principle does this trade against?" is a standard ARB question.
- **In hiring:** loops are calibrated against principles 7, 8, and 9.
- **In disagreement:** when two leaders disagree, we identify which principle each is optimizing and decide which dominates for *this* decision.
- **In retros:** when something goes wrong, we ask which principle the system failed to honor.

## How principles change

Once a year, the engineering leadership team reviews this list. Principles can be added, sharpened, or retired — but never quietly. Every change is recorded with the reason.
