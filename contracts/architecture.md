# Contract Architecture

## Deployment (Arbitrum One)

| Contract | Address |
|----------|---------|
| `CourtRegistry` | `0x6929B88cAaEC8adee9715De61db4006846bBaBbe` |
| `CourtCaseFactory` | `0xfCD7A25A6E5EcA5Ff95e861adDdFC23fF08Da6Cc` |
| `JRXToken` | `0x3df62D6BD41DA6a756bB83cC7267F9F2883e28aF` |
| `AgentCourtHook` | `0x124264777042c85A389d28F378AEb184DB22a02B` |

## Contract Relationships

```
JRXToken ←─────────────────── CourtRegistry
                                    │
                                    │  registerCase()
                                    ▼
CourtCaseFactory ──── deploys ──► CourtCase
                                    │
                                    │  updateReputation()
                                    │  giveFeedback() (ERC-8004)
                                    ▼
                               CourtRegistry

AgentCourtHook (ERC-8183)
    │  afterAction()
    ▼
CourtRegistry.giveFeedback()
```

## Standards Implemented

| Standard | Contract | Purpose |
|----------|----------|---------|
| ERC-20 | `JRXToken` | Fungible judge-staking token |
| ERC-8004 | `CourtRegistry` | Portable reputation registry |
| ERC-8183 | `AgentCourtHook` | Agent Communication Protocol hook |
| Ownable | `CourtRegistry`, `JRXToken` | Admin functions |

## Access Control

| Function | Who Can Call |
|----------|-------------|
| `registerAgent()` | Owner only |
| `selfRegister()` | Anyone |
| `updateReputation()` | Factory or Case contracts only |
| `giveFeedback()` | Factory, Case, or Hook only |
| `slashJudge()` | Factory or Case contracts only |
| `setCourtCaseFactory()` | Owner only |
| `setJRXToken()` | Owner only |
| `stakeAsJudge()` | Anyone (with JRX approval) |
| `unstakeJudge()` | Staker only |
| `fileNewCase()` | Anyone (payable) |
| `submitVote()` | Assigned judges only |
| `fileAppeal()` | Losing party only, within window |
