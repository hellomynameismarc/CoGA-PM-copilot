# Startale Wallet Swap PRD

**Status**: Draft
**Date**: 2026-01-07
**Owner**: Product Team

# Problem Alignment

## Problem & Opportunity
Startale ecosystem users currently face high friction when trying to swap assets between Astar (L1) and Soneium (L2). They are forced to manage multiple addresses (EVM vs Native), bridge manualy, and constantly worry about "insufficient gas."
By leveraging **Account Abstraction (AA)**, we can abstract gas fees and batch transactions to deliver a seamless "SuperApp" experience.

**Why Now?**
- **Astar & Soneium Growth**: As Sony's chain launches, new users are entering via games/apps and expect a zero-friction experience.
- **Lost Revenue**: Users are leaving the wallet to swap on external DEXs or centralized exchanges.
- **Tech Readiness**: Soneium AA infrastructure allows us to finally solve the "gas problem" via Paymasters.

## High Level Approach
We will build a native **Swap Module** within the Startale Wallet that aggregates liquidity from **1inch (Astar)** and **Uniswap (Soneium)**.

**Key Differeniators:**
- **Gasless Swaps**: Use AA Paymasters to allow users to pay swap fees in the token being swapped (e.g. pay fee in USDC, not ETH/ASTR).
- **Unified Account**: Automatically route between EVM and WASM/Native addresses without user manual bridging.

### Narrative
*Hero Moment*: A new user playing a Sony game on Soneium wants to buy an in-game item priced in USDC, but only has ETH. instead of leaving the game, finding a DEX, approving, and swapping, they click "Swap" in the wallet. One click, no gas check, instant USDC. "It just works."

## Goals
1. **Ecosystem Stickiness**: 50% of new wallets complete 1+ swap in first 14 days.
2. **Retail-Friendly UX**: 98% Swap Success Rate (SSR) via AA Paymasters (no "out of gas" errors).
3. **Revenue**: $100k+ monthly revenue by Month 2 via 0.5% swap fees.

## Non-goals
1. Building our own AMM/DEX (we route, we don't pool).
2. Fiat On-Ramp integration (separate PRD).
3. Advanced trading tools (Limit orders, Charts) for V1.

# Solution Alignment

## Key Features
1. **Market Swaps**: Instant execution at current price via Aggregators.
2. **Gasless Swaps (AA)**: Paymaster covers gas; fee taken from trade.
3. **One-Click Batching**: Combine `Approve` + `Swap` into one UserOp.
4. **Token Safety**: Warning system for unverified/scam tokens (Tiered safety list).

### Key Flows
**User Swap Flow**:
1. User selects ASTR -> USDC.
2. "Quote Engine" fetches best rate from 1inch.
3. Backend simulates transaction via Tenderly (Fail if likelihood of failure > 0).
4. User signs ONE UserOp (Approve + Swap).
5. Bundler submits to chain; Paymaster pays gas.
6. User receives USDC.

### Key Logic
- **Slippage**: Auto-set to 0.5% for majors, 3% for low liquidity.
- **Liquidity Routing**:
    - **Astar**: Route via 1inch API.
    - **Soneium**: Direct Uniswap V4 integration (fallback to Velodrome).
- **Cross-Chain**: If swapping Astar <-> Soneium, use LiFi bridge aggregation (Phase 1.5).
- **Fees**: 0.5% flat fee. Collected in input token. Swept weekly to Treasury via Gelato.

# Development and Launch Planning

| Milestone | Use Case | Description |
|-----------|-------------|-------------|
| **Phase 0** | Infrastructure | Paymaster contracts, 1inch API setup, Tenderly integration. |
| **Phase 1** | Internal Alpha | Whitelisted users, Mainnet test. 99% Success Rate target. |
| **Phase 1.5** | Public Beta | Public launch, Token Safety list active. Target $100k vol/day. |
| **Phase 2** | Scale | LiFi Cross-chain integration. |

## Operational Checklist
- [ ] Paymaster funding strategy defined (Treasury Ops)
- [ ] Legal/Compliance review (Geo-fencing if needed)
- [ ] Analytics event tracking (Swap Start vs Swap Success)
- [ ] Support FAQs for "Why did my swap fail?" (Slippage explanation)

## Risks
- **Smart Contract Risk**: Mitigated by using audited external protocols (1inch, Uniswap).
- **Frontend/API Downtime**: Fallback to direct provider SDKs.
- **Scam Tokens**: Integration with GoPlus Security API to filter honeypots.
