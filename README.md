# Kinetica

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

Kinetica is a GPU-accelerated, real-time analytical database that unifies relational (SQL), vector, graph, geospatial, time-series and OLAP workloads in a single query engine, aimed at applications needing millisecond-latency analytics over continuously streaming data. Grown out of a GPU-accelerated geospatial and temporal engine built for U.S. Army Intelligence (INSCOM) in 2009, it is deployed today as the retrieval and reasoning layer behind AI agents and LLM-powered systems. The database is consumed through a POST-only JSON REST API (/execute/sql, /show/table, /insert/records/json, /filter/*, /aggregate/*, /match/graph and friends) served from each deployment on port 9191, plus first-party client libraries for Python, Java, C++, C#, JavaScript/Node.js and Go, JDBC/ODBC drivers, and the KiSQL command-line client. For agents, Kinetica publishes an A2A agent card and an installable Agent Skills package on its documentation host, and ships Toolbelt — an OAuth-protected hosted MCP server exposing toolbelt_* tools for SQL, vector search, graph traversal, schema introspection and ingest-job inspection.

**Areas:** Database · Analytics · gpu-acceleration · Real-Time Analytics · Vector Search · Graph Analytics · Geospatial · Time Series · SQL · Streaming · Data Infrastructure · MCP

## Kinetica on APIs.io

Everything profiled for Kinetica is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/kinetica/](https://apis.io/providers/kinetica/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [Kinetica Database REST API](https://apis.io/apis/kinetica/kinetica-database-rest-api/) — POST-only JSON REST API exposed by every Kinetica deployment on port 9191. Endpoints cover SQL execution (/execute/sql), record ingest and egress…
- [Kinetica Toolbelt MCP Server](https://apis.io/apis/kinetica/kinetica-toolbelt-mcp-server/) — Hosted Model Context Protocol server that gives any MCP-speaking agent a single endpoint onto a Kinetica database. Exposes toolbelt_* tools for SQL…
- [Kinetica Docs MCP Server](https://apis.io/apis/kinetica/kinetica-docs-mcp-server/) — Read-only Model Context Protocol server over the published Kinetica documentation site, advertised from https://docs.kinetica.com/.well-known/mcp.json with…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (2)

Model Context Protocol servers that expose the API to agents.

- [Kinetica Docs](https://apis.io/servers/kinetica/kinetica-docs/)
- [toolbelt](https://apis.io/servers/kinetica/toolbelt/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Kinetica Authentication](https://apis.io/security/kinetica/kinetica-authentication/)
- [Kinetica Domain Security](https://apis.io/security/kinetica/kinetica-domain-security/)
- [Kinetica Vulnerability Disclosure](https://apis.io/security/kinetica/kinetica-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Kinetica Scopes](https://apis.io/scopes/kinetica/kinetica-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.kinetica.com/)
- [Documentation](https://docs.kinetica.com/7.2/)
- [Getting started](https://docs.kinetica.com/7.2/guides/quickstart-guide/)
- [API reference](https://docs.kinetica.com/7.2/api/)
- [Pricing](https://www.kinetica.com/pricing)
- [Sign up](https://cloud.kinetica.com/)
- [Support](https://www.kinetica.com/support)
- [Changelog](https://docs.kinetica.com/7.2/release/)
- [Blog](https://www.kinetica.com/blog)
- [Security](https://www.kinetica.com/.well-known/security.txt)
- [Terms of service](https://www.kinetica.com/terms-of-service)
- [Privacy policy](https://www.kinetica.com/privacy-policy)
- [GitHub](https://github.com/kineticadb)

## API Evangelist rating

**Kin Score 41.2** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 0.0 |
| Contract governance | 18.2 |
| Operational transparency | 28.9 |
| Developer ergonomics | 85.7 |
| Access clarity | 31.6 |

**Agent readiness 27.3** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | — |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | yes |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 40.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/kinetica/](https://apis.io/providers/kinetica/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Kinetica: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/kinetica/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
