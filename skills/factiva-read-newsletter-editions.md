---
name: Read Factiva newsletters and their editions
description: List the newsletters an account can see, walk a newsletter's editions, and pull the content items inside a specific edition using the JSON:API relationship links.
api: openapi/factiva-newsletters-api-openapi.json
operations:
  - NewslettersRead
  - NewsletterReadById
  - EditionsRead
  - EditionReadById
generated: '2026-08-13'
method: generated
source: openapi/factiva-newsletters-api-openapi.json
---

# Read Factiva newsletters and their editions

The Newsletters API is the best-formed Factiva surface: a real OpenAPI 3.0.2 document, unique
operationIds, error schemas, and `application/vnd.api+json` responses in JSON:API shape. Follow
the relationship links instead of constructing URLs.

## Before you start

- Base host `https://api.dowjones.com`.
- Auth: `Authorization: Bearer {token}` (`bearerAuth`, JWT). Token from
  `POST https://accounts.dowjones.com/oauth2/v1/token`. Note that the spec declares no 401 —
  an unauthenticated call fails at the gateway with `403` and code `1011001`.
- Which newsletters you can see is an entitlement on the account, not a scope on the token.

## Steps

1. **List newsletters.** `NewslettersRead` — `GET /newsletters`. Each item carries
   `attributes` (`name`, `token`, `shared_status`, `access_scope`, `is_owner`, `total_editions`,
   `user_type`) and a `relationships` object with `editions`, `deliveries` and `content`.
   - `shared_status` is one of `User`, `Account`, `Factiva` — `Factiva` means a Dow Jones-curated
     newsletter rather than one the account built.
   - `access_scope` is `Personal` or `Account`.
   - Read `total_editions` before you page: it tells you whether the next call is worth making.
2. **Read one newsletter.** `NewsletterReadById` — `GET /newsletters/{id}`. Returns the full
   `newsletter_details` and `current_update_status`.
3. **List its editions.** `EditionsRead` — `GET /newsletters/{id}/editions`. Prefer the
   `relationships.editions.links` value from step 1 or 2 over building this path yourself.
4. **Read one edition.** `EditionReadById` — `GET /newsletters/{id}/editions/{editionId}`.
   The edition's `relationships.content` names the content items; each is a `content_item` with
   `attributes` (headline, body, images) and `meta` (code sets, print edition placement,
   emphasis flags such as `hot` / `dominant` / `analysis`, geo relevance).
5. **Fetch full article text if you need it.** The edition returns content items, not always the
   complete licensed article. Take the accession number and use the Content API
   (`GET /refs/{ref}`) — see `skills/factiva-search-and-fetch-article.md`.

## Paging

Standard Factiva pagination: `offset` and `limit` query parameters, a `meta` object with
pagination state, and a `links` object with `self` / `prev` / `next` / `first` / `last`.
Follow `links.next`.

## Errors

`application/vnd.api+json` with an `errors[]` root.

- `400` — Bad Request, incorrect parameters.
- `404` — no newsletter or edition with that id.
- `500` — internal error.
- `503` — service unavailable; retry with backoff.

Note the partial-success shape: a list response can return an item whose `attributes` is an
`error_response` rather than newsletter attributes (with `id` set to something like
`id_number_not_exists`). Check each item's shape before reading `attributes.name` — a 200 does
not guarantee every element resolved.

Conventions: `conventions/factiva-conventions.yml`. Errors: `errors/factiva-problem-types.yml`.
