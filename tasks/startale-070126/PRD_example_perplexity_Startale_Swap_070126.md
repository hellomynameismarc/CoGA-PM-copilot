# Startale Wallet Swap PRD

**Version:** 1.0  
**Status:** Draft  
**Owner:** Product Team  
**Date:** January 07, 2026

## 1. Executive Summary
This PRD outlines the V1 Swap feature for the Startale Wallet. Our goal is to leverage **Account Abstraction (AA)** to deliver the most seamless swap experience on **Astar (L1)** and **Soneium (L2)**. By abstracting gas fees and batching transactions, we solve the primary friction points of traditional wallets (MetaMask/Phantom) and position Startale as the "SuperApp" for the Sony/Astar ecosystem.

## 2. Product Goals & User Segments

### User Personas
| Persona | Description | Primary Goal | V1 Feature Focus |
| :--- | :--- | :--- | :--- |
| **The Astar Insider** | Existing ASTR staker & DeFi user | Diversify yield; swap ASTR ↔ Stablecoins | Deep liquidity via 1inch; Low fees |
| **The Soneium Gamer** | New crypto user via Sony games | Instant in-game currency swaps | **Gasless Swaps**; Zero friction |
| **The Cross-Chain Bridger** | Power user moving assets | Bridge Astar L1 ↔ Soneium L2 | Unified Bridge+Swap (LiFi) |

### Top 3 Product Goals (V1)
1.  **Ecosystem Stickiness:** Become the default "Service Layer" for Soneium. Target: **50% of new wallets complete 1+ swap in first 14 days.**
2.  **Retail-Friendly UX:** Eradicate "Insufficient Gas" errors. Target: **98% Swap Success Rate (SSR) via AA Paymasters.**
3.  **Revenue Generation:** Establish sustainable cash flow. Target: **$100k+ monthly revenue by Month 2.**

### Non-Goals (V1)
*   Building a proprietary AMM/DEX (we route, we don't pool).
*   Advanced trading tools (Charts, Order Books, Stop-Loss).
*   Fiat On-Ramp integration (handled in separate PRD).

## 3. Chains & Liquidity Strategy

### Chain Support Matrix
| Chain | Strategy | Primary Provider | Fallback |
| :--- | :--- | :--- | :--- |
| **Astar (L1)** | Aggregator-First | **1inch API** | Uniswap V3 SDK |
| **Soneium (L2)** | Direct Integration | **Uniswap V4** | Velodrome |
| **Cross-Chain** | Bridge Aggregation | **LiFi** (Phase 1.5) | Stargate Direct |

**Rationale:**
*   **Astar:** Mature ecosystem; 1inch provides best routing across Curve, Balancer, and Uniswap.
*   **Soneium:** New chain; Aggregators lag in indexing. Direct Uniswap V4 integration ensures Day 1 uptime and liquidity access.

### Handling Liquidity Edge Cases
*   **Low Liquidity (<$100k):** Display "High Price Impact" warning if slippage > 2%.
*   **Stable Pairs (USDC/USDT):** Auto-route via Curve (Astar) or Uniswap V3 0.01% pools (Soneium) for near-zero slippage.
*   **Token Safety:**
    *   **Tier 1:** Verified (CoinGecko Top 1k + Uniswap List) → Show Logo.
    *   **Tier 2:** Unverified (> $50k liq) → Show Warning.
    *   **Tier 3:** Blocked (Scams/Honeypots) → Hide.

## 4. Swap Features & UX

### V1 Feature Set (Launch)
*   **Market Swaps:** Instant execution at current price.
*   **Gasless Swaps (AA):** User pays swap fee; Startale Paymaster covers gas.
*   **One-Click Batching:** `Approve` + `Swap` combined into single UserOperation.
*   **Simulation:** Pre-flight check via Tenderly to prevent failed txs.

### Advanced Features (Phase 2)
*   **Limit Orders:** "Gasless" off-chain orders via 1inch Protocol.
*   **DCA (Dollar Cost Average):** Recurring swaps powered by AA Session Keys.
*   **Cross-Chain Swaps:** One-click Astar → Soneium bridging.

## 5. Fees & Economics

### Fee Model
*   **User Fee:** **0.50%** flat fee on all swaps.
*   **Gas Policy:** Startale subsidizes gas (cost ~ $0.05 on Soneium) from the 0.5% fee revenue.
*   **Revenue Share:** 1inch Partner Program (30-50% of positive slippage).

### Treasury Operations (The "Sweeper")
*   **Collection:** Fees accrue in `FeeCollector` contracts on each chain in the *input token* (e.g., DOGE, PEPE).
*   **Liquidation:** **Gelato Web3 Function** triggers weekly.
    *   Batches all tokens > $100 value.
    *   Swaps to USDC.
    *   Bridges to Mainnet Treasury Multisig.

## 6. Risk, Safety & Compliance

| Risk Category | Mitigation Strategy | Owner |
| :--- | :--- | :--- |
| **Smart Contract Risk** | Direct integration with audited protocols (1inch, Uniswap). Minimal custom code. | Engineering |
| **Scam Tokens** | **GoPlus Security API** integration to detect Honeypots/Tax tokens. | Product |
| **Failed Txs** | **Tenderly Simulation** blocks "doomed" txs before signing. | Engineering |
| **Regulatory** | Geo-fence feature for Japan/Singapore compliance (if required). Terms of Service disclaimer. | Legal |

## 7. Technical Architecture (High-Level)

### Components
1.  **Frontend (Mobile/Web):** React Native; calls Startale Backend for quotes.
2.  **Backend "Quote Engine":** Aggregates 1inch/Uniswap APIs; adds fee; returns `UserOperation` calldata.
3.  **Bundler Service:** Stackup or Alchemy; submits UserOps to Soneium/Astar mempool.
4.  **Paymaster Contract:** Verifies fee payment; sponsors gas.
5.  **Simulations:** Tenderly API for pre-flight checks.

### Data Flow
1.  User requests Quote (ASTR → USDC).
2.  Backend fetches best rate (1inch).
3.  Backend simulates tx (Tenderly).
4.  Backend constructs `UserOp` (Approve + Swap).
5.  User signs `UserOp`.
6.  Bundler submits to chain.

## 8. Roadmap & Phasing

| Phase | Timeline | Key Deliverables | Success Metrics |
| :--- | :--- | :--- | :--- |
| **Phase 0: Build** | Weeks 1-4 | Contracts (Paymaster), 1inch Integration, Tenderly Setup | Audit Pass |
| **Phase 1: Alpha** | Weeks 5-6 | Internal Launch, Whitelisted Users, Soneium Mainnet | 99% Swap Success |
| **Phase 1.5: Beta** | Weeks 7-8 | Public Launch, Token Safety Lists | $100k Vol/Day |
| **Phase 2: Scale** | Month 3+ | LiFi Cross-Chain, Limit Orders, DCA | $10M Vol/Month |

## 9. Appendix: Competitive Analysis
*   **Vs. MetaMask:** We offer **Gasless Swaps** (they don't). Lower fees (0.5% vs 0.875%).
*   **Vs. Phantom:** We support **Astar/Soneium native** (they focus on Solana).
*   **Vs. Uniswap Wallet:** We offer **Cross-Chain Bridge+Swap** (they are chain-siloed).
