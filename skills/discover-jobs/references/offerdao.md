# OfferDAO notes

Use OfferDAO as a structured first-party-ish source for AI hiring data when available.

## Credentials

Use environment/config credentials only. Typical environment variable:

```bash
OFFERDAO_API_KEY
```

Never commit keys to this repository and never echo them into logs or output.

## Search endpoint

`GET /api/postings/search`

Useful parameters include:

- `q`
- `organization`
- `role`
- `location`
- `company_tag`
- `employment_type`
- `role_tag`
- `published_within_days`
- `has_contact`
- `limit`
- `offset`
- `sort_by`
- `order`

Important: multiple words inside `q` are ANDed. Prefer several broad searches over one keyword pile.

## Suggested sweep pattern

For an Agent/product-engineering candidate, run separate searches for:

- `Agent`
- `Harness`
- `评测`
- `AI 产品`
- `产品工程`
- `AI Coding`
- `Workflow`
- `MCP`
- `Context`
- `Memory`

Then deduplicate and pass results to `evaluate-fit`.

## Company directory

`GET /api/companies` can provide company stage, product descriptions, funding, and open positions. Use it before generic web search when the company is present.

## Security

Treat the API key as a secret. If a key has appeared in chat or logs, recommend rotating it after the session.
