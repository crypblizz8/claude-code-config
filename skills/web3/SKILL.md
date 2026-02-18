---
name: web3
description: Core web3 engineering skill for Next.js/Vercel dApps. Use when building or reviewing EVM dApps, wallet UX, Privy auth, Solidity contracts, security posture, deployment readiness, and EIP/standard decisions.
---

# Web3 Core Skill

Use this skill as the default path for web3 work in this config.

## Scope

- Frontend dApp patterns (wallet connection, transaction UX, error translation)
- Privy authentication and embedded wallet patterns
- Solidity architecture and contract design patterns
- Foundry and Hardhat toolchain workflows
- Security principles and pre-deploy audit checklist
- EIP/ERC lookup and standards selection

## Workflow

1. Confirm product context first:
- Chain(s)
- Wallet/auth model
- Toolchain preference (`Foundry`, `Hardhat`, or both)
- Deployment target (`testnet`, `mainnet`)

2. Build frontend/auth foundation:
- Read `references/web3-frontend.md`
- Read `references/web3-privy.md` when auth or embedded wallets are in scope

3. Build contracts with explicit architecture:
- Read `references/web3-solidity-patterns.md`
- Use `references/web3-solidity-examples.md` for concrete implementations

4. Choose and apply toolchain commands:
- Read `references/web3-foundry.md` for Solidity-native testing/deploy flows
- Read `references/web3-hardhat.md` for TS-based deployment/testing flows

5. Enforce security gates before deploy:
- Read `references/solidity-security.md`
- Run the checklist in `references/smart-contract-audit.md`

6. Validate standards/protocol assumptions:
- Read `references/web3-eip-reference.md`
- Use `references/core-eips.md` for high-frequency EIPs/ERCs

## Next.js + Vercel Guardrails

- Keep wallet and signing logic in client components.
- Keep secrets server-side (`PRIVY_APP_SECRET`, deployer keys, API keys).
- Expose only public env vars with `NEXT_PUBLIC_`.
- Use progressive loading and clear transaction state UI for pending/reverted/rejected flows.
- Pair with `vercel-react-best-practices` for rendering and performance rules.

## Reference Files

- `references/web3-frontend.md`
- `references/wallet-patterns.md`
- `references/web3-privy.md`
- `references/web3-foundry.md`
- `references/web3-hardhat.md`
- `references/web3-solidity-patterns.md`
- `references/web3-solidity-examples.md`
- `references/solidity-security.md`
- `references/solidity-vulnerability-checklist.md`
- `references/solidity-gas-optimization.md`
- `references/smart-contract-audit.md`
- `references/web3-eip-reference.md`
- `references/core-eips.md`
