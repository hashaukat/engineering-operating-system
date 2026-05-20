# Incident Management

> Incidents are the most honest signal an engineering org produces. How we respond to them — and what we learn from them — is the clearest statement of our values.

## Goals

1. **Restore service quickly** without making things worse.
2. **Communicate clearly** to customers, support, and leadership.
3. **Learn deeply** so the same class of incident does not recur.
4. **Protect the humans** who responded.

## Severity model

| Sev | Customer impact | Examples | Response |
|---|---|---|---|
| **Sev1** | Major customer-facing outage; revenue or trust at risk | Full site down, data loss, security breach | Page on-call + IC immediately; exec notified; status page within 15 min |
| **Sev2** | Significant degradation; key features broken for many customers | Checkout slow, key API at 50% error rate | Page on-call; status page within 30 min |
| **Sev3** | Limited impact or workaround exists | Single feature degraded for a subset | In-hours response; ticket + monitoring |
| **Sev4** | No customer impact; internal issue | Failed nightly job with retry | Async; track in backlog |

## Roles during a Sev1 / Sev2

We use **Incident Command** explicitly. These are *roles*, not job titles — anyone trained can fill them.

| Role | Job |
|---|---|
| **Incident Commander (IC)** | Owns the response. Makes decisions. Does *not* type at keyboards. |
| **Tech Lead** | Drives technical investigation and fix. |
| **Communications Lead** | Writes status page updates, customer notes, internal updates. |
| **Scribe** | Maintains the incident timeline in real time. |

For Sev1: all four roles staffed within 10 minutes. For Sev2: IC + Tech Lead minimum.

## The first 30 minutes

A printed runbook lives in every team's wiki. The skeleton:

1. **Declare.** Anyone can declare an incident. Over-declaring is fine; under-declaring is a learning event.
2. **Open the channel.** Auto-created bridge + chat channel via incident tool.
3. **Assign IC.** First responder is IC until relieved.
4. **Status page within SLA** (15 min Sev1, 30 min Sev2).
5. **Stop the bleeding before finding the cause.** Rollback, flag flip, scale up, divert traffic — restore first, diagnose second.
6. **Page leadership** if Sev1 reaches 30 minutes without mitigation.

## On-call expectations

- **Rotations:** weekly, primary + secondary. Maximum 1 week in 4 on primary.
- **Pages per shift:** target < 2 actionable pages per night. A team consistently above this triggers a reliability investment, not a hiring request.
- **Comp time:** every page outside business hours earns time off in lieu, tracked by the EM.
- **Newcomers:** no one is on primary for the first 90 days. Shadow rotations come first.
- **No solo on-call below ~6 engineers.** Small teams join a shared rotation.

## Postmortems

Every Sev1 and Sev2 has a written postmortem within 7 business days, using the [postmortem template](../templates/postmortem-template.md).

**Rules:**
- **Blameless.** We criticize systems, not people. Names appear only as role-holders.
- **Public within engineering.** Postmortems live in a shared space everyone can read.
- **Action items have owners and due dates** — and are tracked on the team's roadmap, not a separate backlog that no one looks at.
- **One incident review per month** with the leadership team, walking through 1–2 postmortems for org-wide learning.

## What we measure

| Metric | Why |
|---|---|
| MTTR (mean time to restore) | Are we getting faster at recovery? |
| MTTD (mean time to detect) | Is our observability working? |
| Incident recurrence rate | Are postmortem actions actually closing? |
| Page noise rate (false / actionable) | Are we burning out the on-call? |
| Time-to-postmortem-published | Are we learning while it is fresh? |

These feed the [scorecard](metrics-scorecard.md).

## How AI fits in

AI assistance is genuinely useful in incident response, with limits:

- **Allowed:** first-pass log summarization, drafting status updates (human-approved), suggesting similar past incidents, drafting the postmortem timeline.
- **Required human:** the IC role, the decision to roll back, the decision to send a customer communication, the final postmortem.
- **Tracked:** every AI-assisted action in an incident is logged in the timeline, so we can study where it helped and where it misled.

## What I refuse

- Postmortems that name individuals as root cause.
- "Human error" as a root cause without asking *why* the system allowed the error.
- On-call schedules that punish parents, partners, or anyone outside US business hours.
- Quiet incidents — every Sev1/2 is acknowledged across engineering, never buried.
