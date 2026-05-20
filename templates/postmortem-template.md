# Postmortem: <Incident Title>

> Blameless. Public within engineering. Written within 7 business days of incident close. See [incident management](../docs/incident-management.md).

| Field | Value |
|---|---|
| Incident ID | `INC-YYYY-NNN` |
| Severity | Sev1 \| Sev2 \| Sev3 |
| Date / time of detection | `YYYY-MM-DD HH:MM UTC` |
| Duration | `<HH:MM>` |
| Incident Commander | `<name>` |
| Tech Lead | `<name>` |
| Author of this document | `<name>` |
| Status | Draft \| Reviewed \| Closed |

## Summary
2–3 sentences. What happened, what was the impact, what fixed it. The version a busy executive would read.

## Customer impact
- Customers affected: `<count or %>`
- Functionality affected: `<list>`
- Duration of impact: `<HH:MM>`
- Financial impact (if known): `<$>`
- SLO budget consumed: `<%>`
- Status page updates posted: `<count>`

## Timeline

All times UTC. **Stick to facts, not interpretation.** Interpretation goes in "Analysis."

| Time | Event | Source |
|---|---|---|
| HH:MM | Deploy of `<service>` v`<n>` | CI |
| HH:MM | Alert fires: `<alert>` | Monitoring |
| HH:MM | On-call paged | PagerDuty |
| HH:MM | IC declared, channel opened | Incident tool |
| HH:MM | Hypothesis: `<X>` | Investigator |
| HH:MM | Mitigation attempted: `<Y>` | IC |
| HH:MM | Service restored | Monitoring |
| HH:MM | Customer comms sent | Comms Lead |
| HH:MM | All-clear declared | IC |

## What went well
3–5 things. The org needs to see what to keep doing.

## What went badly
3–5 things. Specific. Systemic — not "a person did X."

## What we got lucky on
The near-misses. The "if Y had happened too, this would have been Sev1." These are the most valuable lessons.

## Analysis

### Trigger
The change or event that started the incident.

### Contributing factors
Multiple — there is rarely one cause. Use the "5 whys" or causal chain.

### Detection
How did we find out? Was the detection time acceptable? What would have detected it earlier?

### Response
Did the response process work as designed? Where did it break down?

### Resolution
What action restored service? Was it the *right* action, or did we get lucky?

## Action items

Each must have an owner and a due date. Tracked on the team's roadmap, not a separate backlog.

| ID | Action | Owner | Due | Priority | Status |
|---|---|---|---|---|---|
| AI-1 | | | | P0/P1/P2 | |

**Categorize each action:**
- **Prevent** — stops this class of incident from happening again
- **Detect** — finds it earlier next time
- **Respond** — makes us faster when it does happen
- **Mitigate** — reduces customer impact when it does happen

A postmortem with only "respond" actions has not been deep enough.

## AI usage during this incident
Per the [AI policy](../docs/ai-assisted-development-policy.md):
- AI tools used: `<list>`
- Where AI helped: `<specific moments>`
- Where AI misled or wasted time: `<specific moments>`
- Pattern to learn: `<what this teaches us about AI-in-the-loop response>`

## Process check
- Did we follow the [incident process](../docs/incident-management.md)? Y/N + notes
- Was the on-call burden reasonable? Y/N + notes
- Were postmortem actions from prior incidents in this area completed? List unfinished ones.

## Sign-off
| Role | Name | Date |
|---|---|---|
| Author | | |
| EM of affected team | | |
| Director (for Sev1) | | |
