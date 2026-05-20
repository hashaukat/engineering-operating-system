# Security & Supply-Chain Engineering

> Security is a property of the system, not a department. In an AI-first org where code, dependencies, prompts, and agent actions all flow continuously, security must be **shifted left, codified, and automated** — or it doesn't happen at all.

This doc defines the security and supply-chain posture every team is held to, with explicit treatment of AI-specific threats.

---

## The three guarantees

Every team, every service, every release must guarantee:

1. **Provenance** — we know where every line of code, dependency, model, and prompt came from, who approved it, and when.
2. **Least privilege** — every human, service, and agent has the minimum access needed and nothing more.
3. **Verifiability** — every claim about security (this is encrypted, this is patched, this is reviewed) is backed by an automated check, not a checkbox.

If a guarantee cannot be made for a system, that gap is logged as a risk on the [scorecard](metrics-scorecard.md) with an owner and a date.

---

## Software supply chain

### Dependency hygiene

- **SBOMs are generated on every build** (SPDX or CycloneDX) and stored with the artifact.
- **Dependencies are pinned and lock-filed.** No floating versions in production.
- **Renovate/Dependabot or equivalent runs daily.** Critical/high CVEs become PRs automatically.
- **License policy is enforced in CI** (e.g., GPL incompatibility for proprietary code blocks the build).
- **Internal artifact registry** mirrors public registries. Direct fetches from npm/PyPI/Maven Central in production builds are blocked.

### Source integrity

- **Signed commits** required for `main` on regulated services.
- **Branch protection**: no direct pushes to `main`, required reviews, required status checks.
- **CODEOWNERS** for security-sensitive paths (auth, payments, data deletion, infra).
- **CI/CD pipelines** themselves are reviewed code, not Jenkins jobs configured by hand.

### Build & artifact integrity

- **SLSA Level 3 target** for production services: hermetic builds, provenance attestation, tamper-evident artifacts. See [SLSA framework](https://slsa.dev/).
- **Container images** are signed (Cosign or equivalent) and verified at deploy.
- **Base images** come from a curated internal registry, scanned on update.

---

## Secrets & credentials

- **No secrets in code, ever.** Pre-commit hooks + CI scans block them.
- **No secrets in environment files committed to repos.** Local dev uses an approved secrets manager (1Password CLI, Doppler, Vault, etc.).
- **Production secrets** live in a managed secrets store with audit logging.
- **Short-lived credentials by default.** Long-lived API keys are a finding.
- **Rotation** is automated and tested in non-prod.

---

## Application security

- **SAST** in CI on every PR. Findings above an agreed severity block merge.
- **DAST** in pre-production environments, scheduled.
- **Dependency scanning** continuous (SCA), not just on build.
- **Threat modeling** is a required section of any [ADR](../templates/architecture-decision-record.md) for a new service or significant change to an existing one. Use STRIDE or LINDDUN.
- **OWASP Top 10** + **OWASP API Security Top 10** are explicit in the security review checklist.
- **Bug bounty / responsible disclosure** path is public and staffed.

---

## AI-specific security

These are the threats that did not meaningfully exist five years ago and now must be designed for.

### AI-generated code

- Treated as untrusted input until reviewed — see [AI policy](ai-assisted-development-policy.md) and [critical thinking with AI](critical-thinking-with-ai.md).
- Goes through *the same* SAST/SCA/review gates as human code. No exceptions.
- Security-sensitive paths (auth, crypto, payments, data deletion) require dual control regardless of code origin.
- License/IP risk: generated code suspected of being a near-copy of training data is rejected. Use of license-aware tools is preferred.

### Prompt injection & jailbreaking

- Any LLM-backed feature that processes **untrusted text** (user input, documents, emails, web content) must assume **prompt injection will happen**.
- Mitigations layered (no single defense): input sanitization, instruction hierarchy, tool-call allowlists, output validation, capability scoping, sandboxing.
- Reference: [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/).

### Model supply chain

- **Approved models only** — vendor models on the allowlist; open-weights models from verified sources with checksums.
- **Pinned model versions** in production; changes go through change management.
- **Model evals run on every version change** (see [eval template](../templates/ai-feature-eval-template.md)).
- **No training on customer data** without Security + Legal + product approval.

### Agent security

Distinct treatment in [ai-agent-governance.md](ai-agent-governance.md). Summary: agents are privileged software actors and must be treated as such — capability scoping, audit logs, human-in-loop for production-affecting actions.

### Data egress to AI providers

- Customer data, secrets, PII, and unreleased material only sent to **approved** tools with a data-handling agreement.
- DLP controls on the egress path where feasible.
- Audit logging of which model received what (for incident triage).

---

## Identity & access

- **SSO mandatory** for all internal tools.
- **MFA mandatory** for all humans; phishing-resistant (WebAuthn/passkeys) for admin roles.
- **Just-in-time access** for production systems; standing access is a finding.
- **Service-to-service auth** via short-lived tokens or mTLS. No shared static credentials.
- **Quarterly access review** for every privileged role.

---

## Data security

- **Data classification scheme** with at least four tiers (public, internal, confidential, restricted/PII). Owned by Data Governance — see [data-and-privacy-governance.md](data-and-privacy-governance.md).
- **Encryption in transit (TLS 1.2+) and at rest** is default. Exceptions require an ADR.
- **Key management** through a managed KMS; key rotation automated.
- **Backups encrypted, periodically restored** (an unrestored backup is a hope, not a backup).

---

## Incident response — security flavor

Security incidents follow the [incident management](incident-management.md) playbook with additions:

- **Sev1-Sec** triggers immediate Security + Legal + Comms + on-call leadership.
- **Containment first, attribution later.** Pull credentials, rotate keys, isolate hosts before the postmortem.
- **Evidence preservation** is the IC's responsibility. Snapshots, logs, forensic copies before remediation.
- **Customer disclosure** decisions go through a pre-defined matrix (severity × jurisdiction × contract) — not an ad-hoc call at 2am.
- **Postmortem** is blameless and includes a "what would have prevented detection delay" section.

---

## Compliance & audit

This operating system targets the controls common to SOC 2, ISO 27001, PCI-DSS scope, and HIPAA where applicable. The standing posture:

- Controls are **codified** (policy-as-code) where possible.
- Evidence is **continuously collected**, not bulk-assembled at audit time.
- Auditors are met with **read-only access to the system of record**, not screenshots.

Specific regulated-industry obligations live in domain docs (handled per-org).

---

## Metrics

Tracked on the [scorecard](metrics-scorecard.md), reliability lens:

- **Mean time to patch critical CVEs** (target: <7 days for production paths)
- **% of production services with current SBOM**
- **% of secrets in approved store** (target: 100%)
- **% of services with passing SAST in last 7 days**
- **Phishing simulation click-through rate** (trending down)
- **AI feature eval pass rate** (per [eval template](../templates/ai-feature-eval-template.md))
- **Mean time to detect / mean time to contain** for security incidents

---

## Roles

- **Security engineering team** — owns the paved-road controls, the central scans, the response playbook. Stream-aligned to security as a flow, not a gate ([team topologies](team-topologies.md)).
- **Every engineer** — security is part of definition-of-done. There is no "throw it over the wall."
- **Staff+ engineers** — expected to lead threat modeling and security review on significant changes (in the [career ladder](career-ladders.md)).
- **Director / VP of Engineering** — accountable for security posture at the board.

---

## Further reading

- **OWASP** — [Top 10](https://owasp.org/www-project-top-ten/), [API Security Top 10](https://owasp.org/API-Security/), [Top 10 for LLM Apps](https://owasp.org/www-project-top-10-for-large-language-model-applications/).
- **SLSA** — [Supply-chain Levels for Software Artifacts](https://slsa.dev/).
- **NIST** — [Secure Software Development Framework (SSDF)](https://csrc.nist.gov/Projects/ssdf), [AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework).
- **CISA** — [Secure by Design](https://www.cisa.gov/securebydesign).
- **Google** — [BeyondProd](https://cloud.google.com/docs/security/beyondprod), [SRE Book: Security](https://sre.google/).
- **Microsoft** — [SDL](https://www.microsoft.com/en-us/securityengineering/sdl).
