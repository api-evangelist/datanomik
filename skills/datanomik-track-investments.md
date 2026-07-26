---
name: Track investment holdings and movements
description: Retrieve consolidated investment holdings, history, movements and application details across funds, committed, deposits and COE.
api: openapi/datanomik-openbanking-openapi.json
operations: [list-investments, list-investments-history, get_v1-investments-movements, get_v1-investments-movements-1, get_v1-applications-details]
---

# Track investment holdings and movements

Pull a customer's consolidated investment portfolio from the Datanomik OpenBanking API.

## Auth
HTTP Basic with `secretId` / `secretPassword`. The investment endpoints require the `ROLE_INVESTMENTS_READ` role on your key pair. Base URL `https://api.datanomik.com`.

## Steps
1. Call `list-investments` (`GET /v1/investments`) for current holdings.
2. Call `list-investments-history` (`GET /v1/investments/history`) for historical positions.
3. Call `get_v1-investments-movements` (`GET /v1/investments/movements`) for the flat list of automatic-application movements.
4. For a movement receipt, call `get_v1-investments-movements-1` (`GET /v1/investments/movements/{movementId}/receipt`).
5. For consolidated detail across application types (committed, fund, deposit, COE), call `get_v1-applications-details` (`GET /v1/applications/details`) with optional filters by type, date range, account, link, investment and institution.

## Conventions & errors
- Paginate with `page` / `size`.
- `400` = invalid filter/parameter; `401` = missing role or invalid keys. See `errors/datanomik-problem-types.yml`.
