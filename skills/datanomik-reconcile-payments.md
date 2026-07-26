---
name: Reconcile payments and PIX transactions
description: List payments, payment slips and PIX transactions and download their receipts for reconciliation.
api: openapi/datanomik-openbanking-openapi.json
operations: [get_v1-payments, get_v1-payments-1, get_v1-payments-2, get_v1-pix-transactions, get_v1-pix-transactions-1]
---

# Reconcile payments and PIX transactions

Use the Datanomik OpenBanking API to pull payments, payment slips and PIX transactions for reconciliation.

## Auth
HTTP Basic with `secretId` / `secretPassword`. Payment endpoints require the `ROLE_PAYMENTS_READ` role. Base URL `https://api.datanomik.com`.

## Steps
1. Call `get_v1-payments` (`GET /v1/payments`) to list payments; filter by link, account, owner, institution, date range, type, status, amount, currency, country, beneficiary, reference or category.
2. Download a payment receipt PDF with `get_v1-payments-1` (`GET /v1/payments/{paymentId}/receipt`, `application/pdf`).
3. List payment slips with `get_v1-payments-2` (`GET /v1/payment-slips`).
4. List PIX transactions with `get_v1-pix-transactions` (`GET /v1/pix-transactions`).
5. Download a PIX receipt PDF with `get_v1-pix-transactions-1` (`GET /v1/pix-transactions/{pixTransactionId}/receipt`, `application/pdf`).

## Conventions & errors
- Paginate with `page` / `size`.
- Receipt endpoints return binary `application/pdf`; handle the content type accordingly.
- `401` = missing `ROLE_PAYMENTS_READ` or invalid keys. See `errors/datanomik-problem-types.yml`.
