# Data & Privacy Governance

> Data is the substrate of every modern product, and the substrate of every AI feature. The org that handles data well — *classifying, protecting, retaining, and respecting* — ships AI features faster, because the guardrails are already in place. The org that doesn't, ships once and then spends two quarters cleaning up.

---

## The four guarantees

For every piece of data we touch:

1. **Classification** — we know how sensitive it is.
2. **Provenance** — we know where it came from and on what basis we hold it.
3. **Purpose limitation** — we use it only for purposes the customer consented to.
4. **Retention** — we keep it only as long as needed, and we can prove we deleted it on request.

If any of the four can't be answered for a dataset, that's a finding logged with an owner and a date.

---

## Data classification

A minimum scheme; tune labels for your domain:

| Class | Examples | Defaults |
|---|---|---|
| **Public** | Marketing pages, open-source code | No special handling |
| **Internal** | Roadmaps, internal docs, non-customer telemetry | SSO-restricted; not for public AI tools |
| **Confidential** | Customer-attributable usage data, contracts, financials | Encrypted at rest + in transit; access auditable; approved tools only |
| **Restricted / Regulated** | PII, PHI, payment data, credentials, customer secrets | Tokenized / encrypted with field-level controls; access just-in-time; explicit allowlist for processing; no AI processing without dedicated review |

**Every dataset and column** is tagged with a classification. Untagged is treated as Confidential by default — secure first, declassify later.

---

## PII / PHI handling

- **Collect the minimum needed.** Data you don't have can't leak.
- **Tokenize or hash at boundary.** Logs, analytics, and most internal tools should never see raw PII.
- **Field-level encryption** for restricted fields in production stores.
- **Row-level access control** for tenant-scoped data.
- **Production access** to restricted data is JIT, approved, audited, and time-bounded.
- **Synthetic / masked data** for dev and test environments. Real PII in dev is a finding.
- **DSAR (Data Subject Access Request) and deletion** paths are operational, tested quarterly, and meet the regulatory clock (e.g., 30 days under GDPR).

---

## Consent & purpose

- **Consent is recorded with the data**, including version of the consent text.
- **Purpose tags** on datasets describe what they may be used for (e.g., "billing," "product analytics," "model training-eligible," "marketing").
- **Cross-purpose use requires re-consent or explicit legal basis.** Quietly using billing data to train a model is a serious incident, not an oversight.
- **Customer opt-outs** propagate to all downstream systems within an agreed SLA (e.g., 30 days).

---

## Retention & deletion

- **Default retention** is set per data class and per dataset, not per service.
- **Automated lifecycle** moves data hot → warm → cold → delete on schedule.
- **Backups have retention too.** A 7-year backup of "deleted" data is not deletion.
- **Right to be forgotten** flows through: production stores, backups, search indexes, caches, analytics warehouses, vector embeddings, fine-tuned model artifacts.
- **Proof of deletion** is auditable.

---

## Data in the AI era — additions

The big new questions, with our defaults:

### Data sent to AI providers

- **Approved tools only**, with a data processing agreement that prohibits training on our data unless explicitly allowed.
- **Restricted data is not sent** to general-purpose model APIs without dedicated approval.
- **DLP-style controls** on the egress path where feasible.
- **Audit logging** of which payload went to which provider (for incident triage).

### Training & fine-tuning on customer data

- Requires Security + Legal + relevant product owner approval ([AI policy](ai-assisted-development-policy.md)).
- Data is sampled, de-identified, and purpose-tagged before any training pipeline.
- The resulting model artifact is treated as a derivative of that data — same retention, same deletion obligations.
- **Per-customer opt-outs** of training are honored; the system can demonstrate which customers' data is in which model version.

### Retrieval-Augmented Generation (RAG)

- Indexed documents inherit the classification of the source data.
- Per-user retrieval respects row-level / document-level access. RAG is a common source of access-control bypasses — *don't index what the user isn't entitled to read*.
- Embeddings carry the same sensitivity as the source text. Treat the vector store like the source DB.

### Memory / persistence in AI features

- Whatever a feature "remembers" about a user is data subject to all of the above: classification, retention, deletion, export.
- Memory has a retention policy and a "delete my memory" affordance.

### Agent data access

- Agents access data through scoped credentials with the minimum permissions needed ([ai-agent-governance.md](ai-agent-governance.md)).
- Agent actions on data are logged and reviewable.

---

## Regulatory baseline

This operating system is designed to make the following defensible, even if your specific scope varies:

- **GDPR** (EU) — lawful basis, consent, DSAR, deletion, DPIA for high-risk processing.
- **CCPA / CPRA** (California) — sale/sharing opt-outs, consumer rights.
- **HIPAA** (US health) — where applicable, BAAs and PHI handling.
- **PCI-DSS** — where payment data is in scope; reduce scope wherever possible.
- **EU AI Act** — risk classification for AI systems, transparency obligations, high-risk system controls.
- **Sector-specific** (financial services, gov, education) — handled per-org.

Compliance is **codified** (policy-as-code, automated controls, continuous evidence collection) wherever possible. See the security doc for posture: [security-and-supply-chain.md](security-and-supply-chain.md).

---

## Data quality & lineage

Adjacent but real:

- **Data lineage** — for any analytics or AI-input dataset, we can trace it back to source systems and transformations.
- **Data quality SLAs** — completeness, freshness, accuracy targets per critical dataset.
- **Schema changes are reviewed** through the architecture process if they break downstream contracts.
- **Data contracts** between producing teams and consuming teams (analytics, ML, billing) are explicit and versioned.

---

## Roles

- **Data Governance** (a small enabling team or named individuals when org is small) — owns classification, retention defaults, DPIA process, vendor data agreements.
- **Privacy / Legal counsel** — partners on consent, DSAR, regulator engagement.
- **Each team** owns the data classifications, lineage, and retention of the datasets it produces or consumes.
- **Security engineering** ([security-and-supply-chain.md](security-and-supply-chain.md)) — provides the technical controls (encryption, IAM, DLP, audit).
- **Director / VP of Engineering** — accountable for data posture at the board.

---

## Anti-patterns to name and kill

- **"We'll tag the data later."** Once a TB is ingested untagged, you're paying down debt for years.
- **Prod data in dev.** "Just for this debugging session." It will be there in six months.
- **The forgotten backup.** Retention policy in the live store, no policy on the backups.
- **Quiet repurposing.** Using customer data for a purpose the customer didn't consent to. Catastrophic when discovered.
- **RAG over everything.** Indexing internal docs into a shared RAG with no access controls. Predictable PII / IP leak.
- **Fine-tuning on data you "had lying around."** Don't.
- **Treating data governance as a one-team problem.** It's a property of how every team works.

---

## Further reading

- **GDPR** — [official text](https://gdpr-info.eu/) and [EDPB guidelines](https://edpb.europa.eu/).
- **NIST** — [Privacy Framework](https://www.nist.gov/privacy-framework), [AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework).
- **EU AI Act** — [official text](https://artificialintelligenceact.eu/) and risk classification.
- **OWASP** — [Top 10 for LLM Apps](https://owasp.org/www-project-top-10-for-large-language-model-applications/) (data leakage and training data poisoning sections).
- **DAMA-DMBOK** — *Data Management Body of Knowledge* — the practitioner reference for data governance overall.
- **Andrew Ng** — [Data-Centric AI](https://www.deeplearning.ai/the-batch/issue-78/) — the case for data quality as the primary AI lever.
