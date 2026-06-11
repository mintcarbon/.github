# mintcarbon

> A platform for tokenizing verified carbon credits onto Stellar/Soroban and enabling peer-to-peer trading of those tokens.

## Organization Overview

mintcarbon allows carbon credit project developers to mint on-chain tokens backed by real-world verified carbon offsets, and enables buyers, brokers, and institutional traders to discover, purchase, transfer, and retire credits transparently. A full audit trail ensures regulatory compliance and prevents double-counting.

## Repositories

| Repository | Description | Tech Stack |
|------------|-------------|------------|
| [contracts](./repos/mintcarbon-contracts/README.md) | Soroban smart contracts — token, marketplace, escrow, governance, verification records, audit log | Rust, Soroban SDK |
| [backend](./repos/mintcarbonbackend/README.md) | Off-chain backend services — REST API, KYC module, registry integrations, notification service, price oracle adapter, compliance reporting | Rust/Go, PostgreSQL, Redis |
| [web](./repos/mintcarbon-web/README.md) | Frontend web dashboard — Issuer, Trader, Compliance Officer, and Admin interfaces | React/Next.js, TypeScript, Tailwind |

## Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│                       web                                │
│           (React/Next.js Dashboard)                      │
└────────────────────┬────────────────────────────────────┘
                     │ HTTPS/TLS 1.3
┌────────────────────▼────────────────────────────────────┐
│                    backend                                │
│   ┌──────┬──────┬────────┬────────┬──────────────────┐   │
│   │ API  │ KYC  │Registry│ Notif. │ Price Oracle     │   │
│   │      │Module│Adapter │ Service│ Adapter          │   │
│   └──────┴──────┴────────┴────────┴──────────────────┘   │
└────────────────────┬────────────────────────────────────┘
                     │ Soroban RPC
┌────────────────────▼────────────────────────────────────┐
│                   contracts                              │
│  ┌───────┬──────────┬─────────┬──────────┬──────────┐   │
│  │Token  │Marketplace│ Escrow  │Governance│Verific.  │   │
│  │Contract│ Contract │Contract │ Contract │Records   │   │
│  └───────┴──────────┴─────────┴──────────┴──────────┘   │
│                     Stellar/Soroban                       │
└─────────────────────────────────────────────────────────┘
```

## Key Features

- **Multi-token standard** — ERC-1155-like contract supporting multiple carbon credit projects
- **Registry verification** — Integrations with Verra VCS, Gold Standard, and American Carbon Registry
- **Atomic settlement** — Locking escrow + token transfer + payment in a single operation
- **On-chain audit trail** — Append-only log with Merkle-tree integrity proofs
- **Governed upgrades** — Time-locked proxy with multi-sig administration
- **Role-based access** — Issuer, Trader, Compliance Officer, Administrator roles with MFA
- **Compliance ready** — KYC/AML, sanctioned-country checks, 7+ year document retention

## Getting Started

Each repository contains its own setup instructions, but the general flow is:

1. Start the [Soroban contracts](./repos/contracts/README.md) — deploy to testnet
2. Start the [backend services](./repos/backend/README.md) — configure environment, run migrations
3. Start the [frontend](./repos/web/README.md) — connect to backend API

## License

This project is licensed under the terms specified in each repository.
