# Team Topologies

> Based on the *Team Topologies* model (Skelton & Pais). I treat it as the lingua franca of org design because it gives us a shared vocabulary for *why* a team exists, not just *what* it works on.

## The four team types

| Type | Purpose | Lifespan | Example |
|---|---|---|---|
| **Stream-aligned** | Owns a continuous flow of value for a specific customer segment or product area | Long-lived | Checkout team, Enterprise Admin team |
| **Platform** | Reduces cognitive load for stream-aligned teams by providing internal products (paved roads) | Long-lived | Developer Platform, Data Platform |
| **Enabling** | Helps stream-aligned teams acquire missing capability, then disbands or rotates | Short-lived (1–3 quarters) | AI Adoption Enabling Team, Observability Enabling Team |
| **Complicated-Subsystem** | Owns a system requiring deep specialist expertise that doesn't fit any single stream | Long-lived | Search Ranking, Payments Risk Engine |

## Interaction modes

Teams interact in exactly one of three ways at any given time. We are explicit about which one applies.

1. **Collaboration** — two teams work closely together for a bounded period (e.g. spinning up a new capability). High bandwidth, high coordination cost. Use sparingly.
2. **X-as-a-Service** — one team consumes another's product with minimal ongoing coordination. The default for stream-aligned teams consuming platform products.
3. **Facilitating** — an enabling team coaches a stream-aligned team. Time-boxed.

## My defaults

- **Stream-aligned teams own services end-to-end.** Code, infra, on-call, SLOs.
- **Platform teams treat their internal products as products.** Roadmaps, customer interviews (with engineers), adoption metrics. See [sample platform team charter](../examples/sample-platform-team-charter.md).
- **Enabling teams have an explicit sunset clause.** Every enabling team charter includes the date and criteria for disbanding.
- **A team owns a system, or no one does.** "Shared ownership" is a euphemism for "nobody is on call at 2am."

## Cognitive load is the constraint

The single most useful question in team design:

> *Is the cognitive load of what this team owns actually fitting in their heads?*

When the answer is no, the right response is almost never "hire more engineers into this team." It is usually one of:

1. Split the team along a clearer domain boundary.
2. Move a chunk of complexity behind a platform abstraction.
3. Reduce the surface area (deprecate, consolidate).

## Topology for the mock scenario

Starting state (40 engineers): mostly stream-aligned teams plus a small SRE group.

Target state (120 engineers):

| Type | Teams | Headcount |
|---|---|---|
| Stream-aligned | 7 product teams | ~60 |
| Platform | 4 (Dev Platform, Data Platform, Infra/SRE, Security) | ~33 |
| Enabling | 2 rotating (AI Adoption, Observability uplift) | ~6 |
| Complicated-subsystem | 1 (Applied AI / model serving) | ~7 |
| Leadership / Eng Ops | — | ~5 |
| Buffer / hiring | — | ~9 |

Notice: the platform-to-stream ratio is ~1:2. This is intentional. Under-investing in platform is the single most common scaling mistake I see, and it shows up as deployment friction, security drift, and reliability regressions.
