---
name: Search Factiva and fetch a licensed article
description: Search the Factiva archive with the Factiva query language, page through the results, and retrieve the full text or a binary rendition of a specific article by its accession number.
api: openapi/factiva-content-api-swagger.json
operations:
  - Search_Get
  - Search_Post
  - GET /search/refs
  - GET /refs/{ref}
  - GET /refs
  - GET /refs/{ref}/binary
  - GET /refs/{ref}/redirect
generated: '2026-08-13'
method: generated
source: openapi/factiva-content-api-swagger.json + https://developer.dowjones.com/documents/factiva_integration-essentials-authentication
---

# Search Factiva and fetch a licensed article

Factiva content is **licensed**. Retrieving an article is a metered, contractual act, not a free
read. Do not cache, redistribute, or pass article text to a model unless the account's licence
covers it — see the Factiva for GenAI usage guidelines.

## Before you start

- You need a Dow Jones-issued credential. There is no self-service signup; credentials arrive
  after a Request Trial form and a sales conversation.
- Base host: `https://api.dowjones.com`, base path `/content`.
- Authenticate with **either** `user-key: {key}` **or** `Authorization: Bearer {token}`.
  For the Content API use the bearer token — get it from
  `POST https://accounts.dowjones.com/oauth2/v1/token` with `grant_type=password`,
  `connection=service-account`, `scope=openid service_account_id`.
- Send `X-API-VERSION` when you need a specific endpoint version. If you omit it you get that
  endpoint's default version, which is documented per product, not platform-wide.

## Steps

1. **Search.** `GET /search` (`Search_Get`) with your query, or `POST /search` (`Search_Post`)
   when the query is structured or too long for a query string. Build the query with the Factiva
   query language against DJID codes — company, industry, region and news subject codes rather
   than free text — which is what makes results reproducible.
2. **Page.** Use `offset` (zero-based index of results to skip) and `limit` (results per page).
   Read the `meta` object for pagination state and the `links` object for fully-formed
   `self` / `prev` / `next` / `first` / `last` URLs. Follow `links.next` rather than incrementing
   `offset` yourself when the object is present. If neither object is returned, page with
   `offset` and the `records` count.
3. **Narrow to references if that is all you need.** `GET /search/refs` returns accession numbers
   only. Cheaper to page over, and it lets you decide which articles are worth retrieving before
   you retrieve any.
4. **Fetch the article.** `GET /refs/{ref}` where `{ref}` is the accession number
   (for example `NFINCE0020251008ela8005aj`). Use `GET /refs` to fetch several by reference in
   one call.
5. **Fetch a rendition if you need one.** `GET /refs/{ref}/binary` returns the PDF or image
   rendition. `GET /refs/{ref}/redirect` resolves to the publisher's own URL — use this when the
   licence permits linking but not reproducing.

## Entity-scoped shortcuts

- `GET /search/organization/{code}` — content for one company, by Factiva company code.
- `GET /search/people/{code}` — content for one person, by Factiva person code.
- `POST /search/portfolio` — content across a portfolio of companies in one call.
- `GET /search/realtime` — the realtime index rather than the archive.
- `POST /search/emerging` — the most relevant emerging topics in the set.

Resolve names to codes first with the Taxonomy/Code endpoints. Searching Factiva by company name
instead of company code is the single most common cause of wrong results.

## Errors

Factiva returns a JSON:API-style envelope, **not** RFC 9457 problem+json:

```json
{"errors":[{"code":"950012","title":"Gen-ai Malformed Request ","status":"400","detail":"..."}]}
```

- `403` with code `1011001` — no credential presented. The gateway answers 403 here, not 401,
  even though some operations declare 401.
- `400` — bad parameters. Check the query syntax and the filter scope values.
- `404` — no article for that reference. Not retryable.
- `500` / `503` — retry with exponential backoff and jitter.

There is **no idempotency key** and **no published rate limit**. Nothing signals throttling in a
response header, so back off on 5xx rather than waiting for a `Retry-After` that will not come.

Full code registry: `errors/factiva-error-codes.yml`. Conventions: `conventions/factiva-conventions.yml`.
