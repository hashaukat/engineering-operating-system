# Decision Record — [Short Title]

> **Type:** Decision Record (non-architectural). For architectural decisions, use [ADR template](architecture-decision-record.md) instead.

---

## Metadata

| Field | Value |
|---|---|
| **Decision ID** | DR-YYYY-NNN |
| **Date** | YYYY-MM-DD |
| **Status** | Proposed / Decided / In-Effect / Reversed / Superseded by DR-YYYY-NNN |
| **Driver** | (Name — runs the process, writes this doc) |
| **Approver** | (Single name — the one accountable person) |
| **Contributors** | (Names — provided expertise / data / dissent) |
| **Informed** | (Teams / individuals who need to know after) |
| **Decision type** | Type 1 (one-way door) / Type 2 (two-way door) / Type 3 (trap door) |
| **Review date** | YYYY-MM-DD (when we revisit whether this was right) |

---

## 1. Context

*What is true right now that makes this decision necessary? Why now?*

(2–6 sentences. Avoid history lessons. State the forcing function.)

---

## 2. The decision in one sentence

*If you cannot state the decision in one sentence, it is not ready.*

> We will __________________________________________ in order to ______________________________________.

---

## 3. Options considered

List **at least three**, including "do nothing" as a real option if applicable.

### Option A — [name]
- **Summary:** ...
- **Pros:** ...
- **Cons:** ...
- **Reversal cost:** ...

### Option B — [name]
- **Summary:** ...
- **Pros:** ...
- **Cons:** ...
- **Reversal cost:** ...

### Option C — Do nothing / status quo
- **Summary:** ...
- **Pros:** ...
- **Cons:** ...
- **Reversal cost:** ...

---

## 4. Recommendation

*The Driver's recommended option and why. The Approver may accept, reject, or send back for more analysis.*

**Recommended option:** _____

**Why:** ...

---

## 5. Risks and reversal plan

| Risk | Likelihood | Impact | Mitigation / Reversal |
|---|---|---|---|
| ... | L/M/H | L/M/H | ... |

**If this decision is wrong, the reversal plan is:**

(Specific steps, owner, expected cost, expected timeline.)

---

## 6. What would change our mind

*Pre-commit, in writing, to the evidence that would cause us to revisit.*

- We will reverse this decision if: ...
- We will revisit this decision (regardless of outcome) on: YYYY-MM-DD

---

## 7. Dissent on the record

*Concerns raised by Contributors that were heard and not adopted. Capture them honestly — both so we can learn from them later and so dissenters know they were heard.*

| Contributor | Concern | Approver's response |
|---|---|---|
| ... | ... | ... |

---

## 8. AI assistance disclosure

*If AI was used in drafting this decision, briefly state how and what the Driver verified.*

- **AI used for:** (e.g., drafting options, summarizing prior decisions, stress-testing recommendation)
- **Driver verified:** (e.g., reread all options, recomputed cost estimate, validated cited prior decisions exist)
- **Human author of record:** (Driver name)

---

## 9. Decision

*Filled in by the Approver.*

- **Decision:** Accept Option ___ / Reject / Send back for more analysis
- **Approver:** ___
- **Date:** YYYY-MM-DD
- **Rationale (in Approver's own words, 1–3 sentences):**

---

## 10. Follow-up

- [ ] Decision logged in the central decision log
- [ ] Informed list notified
- [ ] Review date on calendar
- [ ] Related ADRs / RFCs / specs linked
