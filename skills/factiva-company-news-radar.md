---
name: Run a Factiva company news radar screen
description: Perform a realtime search against the Factiva realtime index to get a company screening list and news radar, the REST replacement for the legacy PerformContentSearch SOAP operation.
api: openapi/factiva-company-news-radar-api-openapi.json
operations:
  - POST /content/realtime/search
  - POST /factiva-organizations/company-screening-list
generated: '2026-08-13'
method: generated
source: openapi/factiva-company-news-radar-api-openapi.json + https://developer.dowjones.com/documents/site-docs-factiva_apis-factiva_workflow_apis_rest-factiva_news_search-news_radar_api-news_radar
---

# Run a Factiva company news radar screen

Company News Radar screens a set of companies against the Factiva realtime index and returns the
company screening list plus the news radar. This is the REST surface that replaced the
`PerformContentSearch` operation on the legacy Search SOAP service — which is deprecated and
largely sunset, so build here rather than there.

## Before you start

- Base host `https://api.dowjones.com`, base path `/search-realtime`.
- Auth: `Authorization: Bearer {token}` (`bearerAuth`, JWT).
- **Neither operation in the published spec declares an operationId.** Bind steps by method and
  path, not by id, and expect code generators to invent names.
- Resolve company names to Factiva company codes first. The screening list is keyed on codes;
  a name string will not match.

## Steps

1. **Screen.** `POST /content/realtime/search` with the search body. This performs the full
   realtime search and returns the matched content.
2. **Get the screening list.** `POST /factiva-organizations/company-screening-list` returns the
   company screening list and the company news radar for an entitled user. This is the operation
   the documentation names; it is not present in the published specification, so treat the
   request shape as documentation-only and confirm it against the Postman collection before
   depending on it.
3. **Page the results.** Standard Factiva pagination — `offset` and `limit`, with `meta` and
   `links` objects on the response.
4. **Retrieve articles.** The screen returns references. Fetch full text through the Content API
   (`GET /refs/{ref}`) — see `skills/factiva-search-and-fetch-article.md`.

## Errors

- `400` — Bad Request, incorrect parameters.
- `401` — Unauthorized. In practice an unauthenticated call is rejected by the gateway with
  `403` and code `1011001` before reaching this service.
- `404` — Not Found, no resource for the request.
- `500` / `503` / `5XX` — server-side; retry with exponential backoff and jitter.

## A trap worth knowing

The specification declares `GET /swagger` on this service. It returns **404** in production
(probed 2026-08-13) — the served copy of this specification lives on the developer portal at
`https://developer.dowjones.com/wp-json/swagger/v1/api/2672`, not on the API host. Do not build a
runtime spec-refresh step on the `/swagger` path.

Conventions: `conventions/factiva-conventions.yml`. Errors: `errors/factiva-problem-types.yml`.
