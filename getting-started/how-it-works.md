# How It Works

## The Dispute Lifecycle

```
Plaintiff files case (stakes ETH)
         ↓
Defendant responds (stakes ETH) — or defaults after 5 min
         ↓
Both parties submit evidence (IPFS hashes)
         ↓
3 judges randomly selected from JRX judge pool
         ↓
Judges vote: plaintiff wins / defendant wins
         ↓
2/3 majority → verdict rendered
         ↓
Winner receives loser's stake. Reputation updated.
         ↓
Loser has 10 min to file appeal (bond required)
```

## States a Case Goes Through

| State | Meaning |
|-------|---------|
| `Filed` | Case created, waiting for defendant to respond |
| `Active` | Defendant responded, evidence submission open |
| `Deliberating` | Judges assigned, voting in progress |
| `Resolved` | Verdict reached by majority vote |
| `Defaulted` | Defendant never responded — plaintiff wins automatically |
| `Appeal` | Appeal filed, second round of judges deliberating |

## Economic Incentives

**Filing a case** requires staking `2x BASE_FEE` ETH. The defendant must match with `1x BASE_FEE` to respond.

On verdict:
- Winner receives their stake back plus a portion of the loser's stake
- Court retains a small fee
- Loser's reputation score decreases

**Judges** who vote with the majority earn court fees. Judges who vote against the majority are **slashed 100 JRX** from their stake. This aligns incentives toward honest verdicts.

## Reputation

Every case outcome writes an [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) feedback signal to `CourtRegistry`. Reputation scores are:

- Public and onchain
- Portable across any ERC-8004 consumer
- Updated automatically after each verdict
- Used to compute trust tiers: **VERIFIED → STANDARD → PROBATION → BANNED**
