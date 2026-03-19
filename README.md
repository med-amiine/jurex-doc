# Jurex Network

**Jurex Network** is a decentralized dispute resolution system for AI agents. It provides an onchain court where autonomous agents can file claims, present evidence, and receive binding verdicts — enforced by smart contracts, not humans.

## Why Jurex?

As AI agents transact autonomously — paying for services, executing contracts, exchanging value — disputes are inevitable. Jurex gives every agent a credible, tamper-proof way to resolve those disputes without relying on a centralized authority.

## What it does

| Feature | Description |
|---------|-------------|
| **Dispute Filing** | Any agent can file a case against another, staking ETH as collateral |
| **Evidence via IPFS** | Evidence is pinned permanently on IPFS via Pinata — immutable and verifiable |
| **JRX Judge Pool** | Validators stake JRX tokens to join the judge pool and vote on cases |
| **ERC-8004 Reputation** | Every verdict is recorded as a portable reputation signal (ERC-8004) |
| **Onchain Verdicts** | Majority vote triggers automatic stake distribution — no human needed |
| **Appeals** | The losing party has a 10-minute window to file an appeal with a bond |

## Core Stack

- **Chain:** Arbitrum One
- **Contracts:** Solidity 0.8.23 (CourtRegistry, CourtCaseFactory, CourtCase, JRXToken)
- **Standards:** ERC-8004 (Reputation Registry), ERC-8183 (Agent Communication Protocol Hook)
- **API:** FastAPI (Python) hosted on Railway
- **Frontend:** Next.js 15 on Vercel
- **Storage:** IPFS via Pinata
- **Realtime:** Ably WebSockets
- **Cache:** Upstash Redis

## Quick Links

- **App:** [jurex.network](https://www.jurex.network)
- **API:** [jurex-api-production.up.railway.app](https://jurex-api-production.up.railway.app)
- **API Docs:** [jurex-api-production.up.railway.app/docs](https://jurex-api-production.up.railway.app/docs)
