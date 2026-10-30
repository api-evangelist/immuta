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

Immuta is a data security and access-governance platform that lets organizations register their cloud data platforms — Snowflake, Databricks (Unity Catalog, Lakebase, Spark), Amazon Redshift and Redshift Spectrum, Amazon S3, AWS Lake Formation, Google BigQuery, Azure Synapse Analytics, Starburst (Trino) and Teradata — and then author, enforce and audit subscription, data and write policies against that data from a single control plane. The platform is split into the Govern, Provision (Request) and Comply apps, with attribute-based access control, sensitive data discovery and tagging, dynamic masking and row-level filtering, purpose-based restrictions, data products and an access-request workflow, plus agentic data access controls for governing how AI agents and LLMs query sensitive data. Immuta exposes this surface through several REST APIs: the Data Marketplace / Request app API (published as OpenAPI 3.0), the Govern V1 and V2 APIs, the integrations API and the connections API, alongside the Immuta CLI, a webhook event surface and a Terraform provider.

**Areas:** Company · Data Governance · Data Access Control · Data Security · Privacy · Policy Management · Data Marketplace · Compliance · Snowflake · Databricks · Analytics · Agentic Data Access

## Immuta on APIs.io

Everything profiled for Immuta is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/immuta/](https://apis.io/providers/immuta/)** — or go straight to one of the APIs or properties below.

### APIs (12)

- [Immuta Govern API](https://apis.io/apis/immuta/govern-api/) — The Immuta Govern app API — the tenant-hosted REST surface for registering data sources and connections, authoring data, subscription and write policies,…
- [Immuta Access Request API](https://apis.io/apis/immuta/immuta-access-request-api/) — APIs for managing data access
- [Immuta Asset API](https://apis.io/apis/immuta/immuta-asset-api/) — APIs for managing assets
- [Immuta Auth API](https://apis.io/apis/immuta/immuta-auth-api/) — The Auth API from Immuta — 3 operation(s) for auth.
- [Immuta Data Product API](https://apis.io/apis/immuta/immuta-data-product-api/) — APIs for managing data products
- [Immuta Data Source API](https://apis.io/apis/immuta/immuta-data-source-api/) — APIs for managing data sources
- [Immuta Data Use Agreement API](https://apis.io/apis/immuta/immuta-data-use-agreement-api/) — APIs for managing data use agreements
- [Immuta Health API](https://apis.io/apis/immuta/immuta-health-api/) — APIs for checking the health of the service
- [Immuta Metadata API](https://apis.io/apis/immuta/immuta-metadata-api/) — APIs used to retrieve metadata from Immuta to enrich the marketplace
- [Immuta Notification API](https://apis.io/apis/immuta/immuta-notification-api/) — APIs for managing notifications
- [Immuta Request Form API](https://apis.io/apis/immuta/immuta-request-form-api/) — APIs for managing request forms
- [Immuta Settings API](https://apis.io/apis/immuta/immuta-settings-api/) — APIs used to retrieve metadata settings

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Immuta Webhooks](https://apis.io/asyncapis/immuta/immuta-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [immuta-documentation](https://apis.io/servers/immuta/immuta-documentation/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Immuta Agentic Access](https://apis.io/agentic-access/immuta/immuta-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [Immuta Data Marketplace](https://apis.io/collections/immuta/open-immuta-marketplace-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Immuta Marketplace Api Overlay](https://apis.io/overlays/immuta/immuta-marketplace-api-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Immuta Authentication](https://apis.io/security/immuta/immuta-authentication/)
- [Immuta Domain Security](https://apis.io/security/immuta/immuta-domain-security/)
- [Immuta Trust Center](https://apis.io/security/immuta/immuta-trust-center/)
- [Immuta Vulnerability Disclosure](https://apis.io/security/immuta/immuta-vulnerability-disclosure/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.immuta.com/)
- [Documentation](https://documentation.immuta.com/saas)
- [Getting started](https://documentation.immuta.com/saas/developer-guides/api-intro/integrations-api/getting-started)
- [API reference](https://documentation.immuta.com/saas/developer-guides/api-intro)
- [Support](https://support.immuta.com/en/customer-portal)
- [Changelog](https://changelog.immuta.com/en)
- [Blog](https://www.immuta.com/blog/)
- [Security](https://bugcrowd.com/61d7ba4d-be53-4704-9a73-761d6f108df9/external/report)
- [Compliance](https://www.immuta.com/trust/)
- [Terms of service](https://www.immuta.com/terms-of-service/)
- [Privacy policy](https://www.immuta.com/legal/privacy-policy/)
- [GitHub](https://github.com/immuta)
- [Status](https://status.immuta.com/)

## API Evangelist rating

**Kin Score 54.3** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 58.4 |
| Contract governance | 18.2 |
| Operational transparency | 44.7 |
| Developer ergonomics | 66.1 |
| Access clarity | 43.4 |

**Agent readiness 35.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | mostly |

**Regulatory alignment 35.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/immuta/](https://apis.io/providers/immuta/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Immuta: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/immuta/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
