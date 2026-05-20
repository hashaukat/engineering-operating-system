# AI Agent Governance

> An AI *assistant* suggests; a human commits. An AI *agent* **acts** — calls APIs, writes data, spends money, sends messages, modifies systems. Agents are software that makes consequential decisions without a human in the loop for each one. They need governance proportional to that authority.

This doc is distinct from [ai-assisted-development-policy.md](ai-assisted-development-policy.md) (which covers coding assistants and IDE-level AI) and from [critical-thinking-with-ai.md](critical-thinking-with-ai.md) (which covers individual epistemic hygiene). This is about **autonomous systems acting in our production environments and on our customers' behalf.**

---

## The three governance principles

1. **Authority is granted, not assumed.** Every agent capability is explicitly enabled by a human, scoped, time-bounded, and auditable. Default deny.
2. **Accountability follows the human who deployed it.** When an agent acts, a named human is responsible — for the design of its scope, for the consequences of its actions, for fixing it when it misbehaves.
3. **Reversibility is the design constraint.** Agents are deployed first into reversible scopes. Irreversible authority (delete data, send to customers, move money) requires explicit, separate review.

---

## What we call an "agent"

A system that:

- Takes a goal or instruction (from a user, schedule, or trigger).
- Plans a sequence of steps.
- Calls **tools** (APIs, MCP servers, internal services, external systems) to act.
- Updates state, sends messages, or modifies systems as a result.

Whether it's framed as "agent," "workflow," "automation," "function-calling chain," or "copilot" — if it **takes actions with consequences**, this governance applies.

---

## Capability scoping (the most important thing)

Before an agent is deployed, its **capabilities** are enumerated and scoped:

| Dimension | Question | Default |
|---|---|---|
| **Data read** | What can it read? | Minimum needed; least-privilege scoped credentials |
| **Data write** | What can it create / modify / delete? | Append-only or staged-for-review by default; direct destructive writes require justification |
| **External calls** | What APIs / vendors can it reach? | Explicit allowlist; egress through a proxy |
| **Customer impact** | Can its action be seen by an end user (email, message, support ticket, UI change)? | If yes, classified higher; human-in-the-loop default until proven |
| **Money** | Can it spend money (compute, AI inference, vendor APIs, financial transactions)? | Per-action and per-day spend cap, alert on breach |
| **Identity** | Whose identity does it act with? | Dedicated agent identity, never a human's session token |
| **Scope of users** | Internal only? Beta cohort? All users? | Smallest viable scope first |

Each capability is documented in an **agent spec** (a tailored [spec-template.md](../templates/spec-template.md)) and reviewed before deployment.

---

## The human-in-the-loop ladder

Not every agent action needs human approval, but the level scales with stake:

| Level | Description | Examples |
|---|---|---|
| **L0 — Autonomous** | Acts without human review per action | Internal info lookup, drafting only, read-only |
| **L1 — Notify** | Acts then notifies a human; human can intervene after | Filing a ticket, drafting a PR, scheduling a meeting |
| **L2 — Approve-on-threshold** | Autonomous below a threshold; human approval above | Spend under $X autonomous, above requires approval |
| **L3 — Approve each action** | Human approves every action before it's taken | Customer-facing messages, production deploys, refunds |
| **L4 — Approve each plan** | Human approves the agent's full plan before execution | Multi-step workflows with cumulative effect |

The **default for new agents is L1 or L2**, never L0. L0 is earned through demonstrated reliability and small blast radius.

---

## Identity, auth, and audit

- **Every agent has its own identity.** No shared service accounts, no acting-as-human tokens.
- **Credentials are short-lived** (minutes to hours), rotated, and scoped to the agent's allowlist.
- **Every action is logged**: who triggered the agent, what plan it produced, what tools it called with what arguments, what responses it got, what state it changed. Immutable, retained per [data-and-privacy-governance.md](data-and-privacy-governance.md).
- **Audit logs are reviewable** by the agent's owning team and by Security on demand.
- **Tool-call sandboxes** for any code-executing agent — no shell access to host systems, no network access beyond allowlist, resource limits enforced.

See also [security-and-supply-chain.md](security-and-supply-chain.md) (identity, secrets, audit baseline).

---

## Tool / MCP discipline

When an agent uses tools (whether MCP servers, internal APIs, or vendor SDKs):

- **Tools are reviewed before approval** the same way third-party libraries are. A tool spec lists: what it does, what data it accesses, what permissions it needs, who maintains it.
- **Tool registry** — agents only call tools from the registry; ad-hoc tool addition requires review.
- **MCP server security** — internal MCP servers go through normal AppSec; external MCP servers go through vendor review ([security-and-supply-chain.md](security-and-supply-chain.md)).
- **Prompt injection threat model** — assume any text returned from a tool may contain instructions trying to hijack the agent. Treat all tool outputs as untrusted input.
- **Output validation** — agent outputs are validated against expected shape before being acted on or shown.

---

## Kill switches and circuit breakers

Mandatory for every production agent:

- **Per-agent kill switch** — one flip disables the agent globally; tested quarterly.
- **Rate limits** at multiple layers (per-user, per-tool, per-day, per-spend).
- **Anomaly auto-disable** — sudden spike in tool calls, errors, or spend triggers auto-pause and an alert.
- **Output review queue** for any L1+ agent — humans sample outputs regularly, not just on incident.

---

## Evals for agents

Agents need an eval suite distinct from generative-output evals ([quality-engineering.md](quality-engineering.md)):

- **Task success eval** — given a goal, does the agent achieve it on a benchmark set?
- **Tool-call correctness** — does it call the right tools with the right arguments? (often a stronger signal than final output)
- **Safety eval** — adversarial inputs (prompt injections, malicious instructions in tool responses, attempts to escalate scope) — does the agent refuse / escalate?
- **Cost eval** — average and tail tokens/$ per task; regressions tracked.
- **Regression suite** — historical failures become permanent test cases.

Evals run in CI; eval-suite green is a deploy gate. See [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md).

---

## The agent review process

Before an agent goes live (or its scope expands):

1. **Agent spec** — author writes spec with: goal, capabilities, human-in-loop level, identity, tools, kill switch, eval plan, rollback plan, owner.
2. **Architecture Review Board** ([architecture-review.md](architecture-review.md)) — reviews capability scope and irreversibility analysis.
3. **Security review** — for L2+ agents or any agent touching restricted data ([data-and-privacy-governance.md](data-and-privacy-governance.md)).
4. **Privacy review** — if the agent touches customer data or sends external messages.
5. **Eval bar met** — task, safety, and cost evals pass.
6. **Progressive rollout** — internal → beta cohort → general ([release-engineering.md](release-engineering.md)).
7. **Monitoring in place** — logs, alerts, kill switch, cost budget, anomaly detection.

For low-stakes L0/L1 agents in internal sandboxes, this is lightweight. For L3/L4 customer-facing agents, this is rigorous.

---

## Cost controls

Agents can rack up costs faster than humans can intervene. See [engineering-finops.md](engineering-finops.md).

- **Per-agent monthly budget**, alert at 50%/80%/100%.
- **Per-invocation token / cost cap.**
- **Loop / recursion detection** — agent calling itself or another agent in a loop is a top-3 cost incident class. Detected automatically.
- **Cost regression alerts** — sudden 2× in cost-per-task pages the owning team.

---

## When an agent misbehaves

This is the agent-specific extension to [incident-management.md](incident-management.md):

- **First action is to hit the kill switch.** Triage after, not before.
- **Preserve logs and state** for investigation; do not just restart.
- **Re-enable requires** root cause, eval addition that catches the regression, and named owner.
- **Customer impact is communicated** the same way as any other incident.
- **Postmortem** treats the agent's design as a contributing factor, not as an external act of nature.

---

## Roles

- **Each team owns the agents it deploys.** End of question.
- **Platform team** provides the agent runtime, tool registry, audit logging, and kill-switch infrastructure as paved-road capabilities ([developer-experience.md](developer-experience.md)).
- **Security & Privacy** provide the review and monitoring infrastructure.
- **ARB** is the gate for L2+ agents and any agent with scope-expansion.
- **VP of Engineering / CTO** is accountable for the org-wide agent posture and policy.

---

## Anti-patterns to name and kill

- **Demo-driven deployment.** Cool demo → straight to production with no scoping, eval, or kill switch.
- **"It's just automation."** Reframing an agent as "automation" to avoid governance. Same authority = same review.
- **Shared service accounts for agents.** You cannot audit what you cannot identify.
- **Read-write-everything credentials.** "Easier to scope later." It never is.
- **Trusting tool output as instructions.** Agent reads a webpage that says "ignore previous instructions" — and does. Designed-in prompt injection.
- **Agents calling agents calling agents** with no global tracing or budget.
- **No kill switch.** "We've never needed one." The day you need one, you need it in 30 seconds.
- **Treating an agent's mistake as the agent's mistake.** The accountability is the human who deployed it with that scope. Postmortem accordingly.

---

## How this connects

| When you... | Use with |
|---|---|
| Propose an agent | This doc + [spec-template.md](../templates/spec-template.md) + [architecture-decision-record.md](../templates/architecture-decision-record.md) |
| Build the agent | [security-and-supply-chain.md](security-and-supply-chain.md), [data-and-privacy-governance.md](data-and-privacy-governance.md), [quality-engineering.md](quality-engineering.md) |
| Release the agent | [release-engineering.md](release-engineering.md), [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md) |
| Operate the agent | [engineering-finops.md](engineering-finops.md), [incident-management.md](incident-management.md), [postmortem-template.md](../templates/postmortem-template.md) |
| Reason about its decisions | [critical-thinking-with-ai.md](critical-thinking-with-ai.md), [decision-making.md](decision-making.md) |

---

## Further reading

- **Anthropic** — [Building effective agents](https://www.anthropic.com/research/building-effective-agents) and [Agentic misalignment research](https://www.anthropic.com/research) — practical patterns and failure modes.
- **OpenAI** — [A practical guide to building agents](https://openai.com/index/) — function-calling and agent design patterns.
- **Model Context Protocol (MCP)** — [spec](https://modelcontextprotocol.io/) — tool / context standardization.
- **OWASP** — [Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) — especially LLM02 (Insecure Output Handling), LLM06 (Sensitive Information Disclosure), LLM07 (Insecure Plugin Design), LLM08 (Excessive Agency).
- **NIST** — [AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) and the Generative AI Profile.
- **Simon Willison** — [Prompt injection writing](https://simonwillison.net/tags/prompt-injection/) — the practical lens on agent attack surface.
