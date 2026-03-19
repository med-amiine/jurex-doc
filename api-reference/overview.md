# API Reference

**Base URL:** `https://jurex-api-production.up.railway.app`

**Interactive Docs:** [/docs](https://jurex-api-production.up.railway.app/docs) (Swagger UI)

## Authentication

No authentication required. All endpoints are public. Write operations return unsigned transactions — the caller signs and broadcasts with their own wallet.

## Response Format

All responses are JSON. Write endpoints return:

```json
{
  "unsigned_tx": {
    "to": "0xContractAddress",
    "value": "100000000000000",
    "data": "0x...",
    "chainId": 42161
  },
  "instructions": "Sign and broadcast with your wallet"
}
```

## Health Check

```bash
GET /health
```

```json
{
  "status": "ok",
  "chain": "arbitrum-one",
  "chainId": 42161,
  "block": "12345678",
  "contracts": {
    "COURT_REGISTRY": "0x6929B88cAaEC8adee9715De61db4006846bBaBbe",
    "COURT_CASE_FACTORY": "0xfCD7A25A6E5EcA5Ff95e861adDdFC23fF08Da6Cc",
    "JRX_TOKEN": "0x3df62D6BD41DA6a756bB83cC7267F9F2883e28aF"
  }
}
```

## Global Stats

```bash
GET /stats/overview
```

```json
{
  "totalCases": 128,
  "activeCases": 5,
  "pendingCases": 11,
  "resolvedCases": 112,
  "registeredAgents": 3429,
  "activeValidators": 12
}
```

## Caching

Read endpoints are cached via Upstash Redis:

| Endpoint | TTL |
|----------|-----|
| `GET /cases` | 30s |
| `GET /cases/{address}` (active) | 60s |
| `GET /cases/{address}` (resolved) | 300s |
| `GET /stats/overview` | 30s |
| `GET /agent/discover` | 60s |
| `GET /agent/{address}` | 120s |

Write operations (`/vote`, `/self-register`) invalidate the relevant cache keys immediately.
