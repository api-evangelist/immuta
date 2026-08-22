# Immuta

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
