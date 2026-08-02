# Immuta

Immuta is a data security and access-governance platform. Organizations register their
cloud data platforms — Snowflake, Databricks (Unity Catalog, Lakebase, Spark), Amazon
Redshift and Redshift Spectrum, Amazon S3, AWS Lake Formation, Google BigQuery, Azure
Synapse Analytics, Starburst (Trino) and Teradata — then author, enforce and audit
subscription, data and write policies against that data from one control plane. The
product is split into the Govern, Provision (Request) and Comply apps, and now includes
agentic data access controls for governing how AI agents and LLMs query sensitive data.

- Website: https://www.immuta.com/
- Documentation: https://documentation.immuta.com/saas
- API guides: https://documentation.immuta.com/saas/developer-guides/api-intro
- Status: https://status.immuta.com/
- Trust: https://www.immuta.com/trust/

## APIs

| API | Contract | Base URL |
|---|---|---|
| Immuta Data Marketplace (Request app) | OpenAPI 3.0, 83 operations | `https://{na\|eu\|ap}.api.immutacloud.com/marketplace` |
| Immuta Govern (V1, V2, integrations, connections) | documented reference, no spec | the customer's own Immuta tenant host |

## Artifacts in this repo

| Path | What it is |
|---|---|
| `openapi/` | The Immuta Data Marketplace OpenAPI 3.0, harvested verbatim from Immuta's GitBook spec host |
| `overlays/` | API Evangelist Overlay 1.0.0 over that spec (does not mutate the original) |
| `asyncapi/` | The webhook event surface — 73 Govern event types plus the Request app webhook API. No AsyncAPI is published |
| `authentication/`, `conventions/`, `errors/`, `data-model/` | Auth profile, cross-cutting semantics, error catalog, entity graph |
| `lifecycle/`, `changelog/` | Versioning, behavior-change process, deprecations, status page, SLA, recent release entries |
| `security/` | Domain security probe, Bugcrowd vulnerability disclosure program, trust center certifications |
| `conformance/` | Standards conformance and the published compliance program |
| `mcp/` | The live documentation MCP server (verified `tools/list`) and the MCP↔REST tool crosswalk |
| `packages/`, `cli/` | Client tooling — the Immuta CLI binaries, Terraform provider, Singer tap |
| `skills/` | Five packaged Agent Skills grounded in verified operationIds |
| `agentic-access/` | Recommended `x-agentic-access` execution contracts for all 83 operations |
| `well-known/`, `llms/` | `/.well-known/` probe record (none published) and the harvested `llms.txt` |

No A2A agent card is published on any Immuta host; `a2a/` is intentionally absent.
