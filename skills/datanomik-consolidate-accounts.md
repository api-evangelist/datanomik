---
name: Consolidate bank accounts and balances
description: Retrieve a customer's connected accounts, their positions, balance history and owners across connected Brazilian institutions.
api: openapi/datanomik-openbanking-openapi.json
operations: [list-accounts, account-position, list-balances-copy, list-general-owners, detail-account, detail-general-owner]
---

# Consolidate bank accounts and balances

Use the Datanomik OpenBanking API to pull a consolidated view of a customer's accounts after they have connected an institution via the Connect Widget (which produces a `linkId`).

## Auth
Send your API keys as HTTP Basic auth: username = `secretId`, password = `secretPassword`. Use the key pair matching your target environment (sandbox vs production). Base URL: `https://api.datanomik.com`.

## Steps
1. Call `list-accounts` (`GET /v1/accounts`, optional `linkId`, `country`) to enumerate the accounts behind a link.
2. Call `account-position` (`GET /v1/accounts/position`) for the current consolidated position.
3. For a specific account, call `detail-account` (`GET /v1/accounts/{id}`).
4. Call `list-balances-copy` (`GET /v1/balances/history`) for balance history.
5. Call `list-general-owners` (`GET /v1/general-owners`) and `detail-general-owner` (`GET /v1/general-owners/{id}`) to resolve account ownership.

## Conventions & errors
- Paginate with `page` (zero-based) and `size` query params, e.g. `?page=0&size=100`.
- `401` = missing/invalid API keys or the key lacks the required role. `404` = the account/link does not exist in this environment. See `errors/datanomik-problem-types.yml`.
- There is no idempotency-key contract; these are safe idempotent reads.
