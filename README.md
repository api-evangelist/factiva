# Factiva (factiva)

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

Factiva is a business information and research tool from Dow Jones that provides access to global news, company information, and market data from thousands of sources.

**URL:** [https://www.dowjones.com/professional/factiva/](https://www.dowjones.com/professional/factiva/)

## Tags

- Business Intelligence
- Content Aggregation
- Market Data
- Media Monitoring
- News
- Research

## Timestamps

- **Created:** 2024
- **Modified:** 2026-03-16

## APIs

### Factiva Snapshots API
Provides programmatic access to create, retrieve, and manage news snapshots based on search queries and filters. Supports analytics explain jobs and time series operations for volume estimation and trend analysis over Factiva content.

**Human URL:** [https://developer.dowjones.com/site/global/apis/factiva_snapshots/index.gsp](https://developer.dowjones.com/site/global/apis/factiva_snapshots/index.gsp)

**Base URL:** `https://api.dowjones.com/factiva/snapshots/v1`

#### Tags
- Analytics
- News
- Search
- Snapshots

### Factiva Streams API
Real-time streaming API that delivers continuous feeds of news content matching specified criteria and filters. Supports creating and managing stream subscriptions with listener methods for pushing content to downstream systems in high-availability setups.

**Human URL:** [https://developer.dowjones.com/site/global/apis/factiva_streams/index.gsp](https://developer.dowjones.com/site/global/apis/factiva_streams/index.gsp)

**Base URL:** `https://api.dowjones.com/factiva/streams/v1`

#### Tags
- News Feed
- Real-Time
- Streaming

### Factiva Extractions API
Enables large-scale extraction of historical news articles and content based on complex queries and date ranges. After job validation, a Snapshot ID is provided along with a list of files to download for offline analysis.

**Human URL:** [https://developer.dowjones.com/site/global/apis/factiva_extractions/index.gsp](https://developer.dowjones.com/site/global/apis/factiva_extractions/index.gsp)

**Base URL:** `https://api.dowjones.com/factiva/extractions/v1`

#### Tags
- Bulk Data
- Extractions
- Historical Data

### Factiva Analytics API
Provides access to aggregated analytics, trends, and insights derived from Factiva's news and content database. Supports volume estimation, explain jobs, and time series analysis for understanding news coverage patterns.

**Human URL:** [https://developer.dowjones.com/site/global/apis/factiva_analytics/index.gsp](https://developer.dowjones.com/site/global/apis/factiva_analytics/index.gsp)

**Base URL:** `https://api.dowjones.com/factiva/analytics/v1`

#### Tags
- Analytics
- Insights
- Trends

### Factiva DJID Taxonomy API
Explores the taxonomy of the Factiva databases using Dow Jones Intelligent Identifiers (DJID). Provides access to approximately 350,000 taxonomy codes covering industries, regions, news subjects, companies, and organizations used to classify Factiva content.

**Human URL:** [https://dowjones.developerprogram.org/site/docs/factiva_apis/factiva_djid_taxonomy_api/index.gsp](https://dowjones.developerprogram.org/site/docs/factiva_apis/factiva_djid_taxonomy_api/index.gsp)

#### Tags
- Classification
- Metadata
- Reference Data
- Taxonomy

### Factiva Code API
Enables retrieval of codes necessary to search for companies, currencies, exchanges, locations, industries, instruments, and news subjects within Factiva. Each data item is identified by a unique Factiva Code and supports lookups by Dow Jones Ticker, CUSIP, DUNS, and ISIN identifiers.

**Human URL:** [https://dowjones.developerprogram.org/site/docs/factiva_apis/factiva_code_api/index.gsp](https://dowjones.developerprogram.org/site/docs/factiva_apis/factiva_code_api/index.gsp)

#### Tags
- Codes
- Companies
- Identifiers
- Reference Data

### Factiva Retrieval API
Provides retrieval functionality that returns licensed news articles as part of trusted data sources in a retrieval-augmented generation (RAG) stack. Designed for enterprise customers building chatbots, research tools, and other AI applications using copyright-compliant Factiva content.

**Human URL:** [https://www.postman.com/dj-cse/factiva-developer/collection/7qbhcvz/factiva-retrieval-api](https://www.postman.com/dj-cse/factiva-developer/collection/7qbhcvz/factiva-retrieval-api)

#### Tags
- AI
- Content
- RAG
- Retrieval

### Factiva Market Data API
Retrieves real-time quotes, delayed quotes, and time series market data for US, Canadian, and global companies. Supports lookups by Dow Jones Ticker, Factiva Code, CUSIP, DUNS, or ISIN to retrieve market fundamentals such as revenue, earnings, assets, liabilities, and growth.

**Human URL:** [https://developer.dowjones.com](https://developer.dowjones.com)

#### Tags
- Financials
- Market Data
- Quotes
- Time Series

## Common Properties

- [Portal](https://developer.dowjones.com)
- [Sign Up](https://developer.dowjones.com/site/global/register/index.gsp)
- [Getting Started](https://www.postman.com/dj-cse/dow-jones-apis/collection/l9tpql6/factiva-apis)
- [Authentication](https://developer.dowjones.com/site/global/apis/authentication/index.gsp)
- [Documentation](https://www.postman.com/dj-cse/dow-jones-apis/documentation/l9tpql6/factiva-apis)
- [Postman Collection](https://www.postman.com/dj-cse/dow-jones-apis/documentation/l9tpql6/factiva-apis)
- [Terms of Service](https://www.dowjones.com/terms-of-use/)
- [Privacy Policy](https://www.dowjones.com/privacy-policy/)
- [Status](https://status.dowjones.com)
- [Support](https://developer.dowjones.com/support)
- [Website](https://www.dowjones.com/professional/factiva/)
- [Blog](https://medium.com/dowjones)
- [GitHub Organization](https://github.com/dowjones)
- [GitHub Repository](https://github.com/dowjones/developer-platform)
- [SDKs](https://github.com/dowjones/factiva-news-python)
- [LinkedIn](https://www.linkedin.com/company/dow-jones)
- [X](https://twitter.com/DowJones)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
