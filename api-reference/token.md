# Token API

## JRX Token

**Contract:** `0x3df62D6BD41DA6a756bB83cC7267F9F2883e28aF`

---

## Get Balance

```
GET /token/balance/{address}
```

```json
{
  "address": "0x...",
  "balance_raw": "10000000000000000000000",
  "balance_jrx": "10000",
  "next_drip_at": 1773886000,
  "can_drip": false
}
```

---

## Drip (Faucet)

```
POST /token/drip
```

Returns unsigned `drip()` transaction. Once broadcast, the caller receives **10,000 JRX** (24-hour cooldown per address).

**Body:**
```json
{ "to": "0xRecipientAddress" }
```

---

## Approve Registry

```
POST /token/approve-registry
```

Build unsigned ERC-20 approval for `CourtRegistry` to pull JRX for staking. Must be done before `POST /judges/stake`.

**Body:**
```json
{ "address": "0xYours", "amount_jrx": "1000" }
```
