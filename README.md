# Course 5: Tokens and Incentive Design

[![Course Series](https://img.shields.io/badge/Series-Blockchain-orange)](../README.md)
[![Tutorials](https://img.shields.io/badge/Tutorials-8-blue)]()
[![Datasets](https://img.shields.io/badge/Datasets-5-green)]()

> *"The Capital tried rules. The Guild tried honor. Both failed. I tried mathematics — and discovered that honesty is just the cheapest strategy."*
>
> — Brenn Auster, *Self-Enforcing Agreements* (Year 867)

---

## Overview

This course teaches **mechanism design, game theory, and token economics** through the story of Brenn Auster — a guild economist who watched the Traders Guild tear itself apart through fraud, bribery, and broken contracts. The Capital imposed rules. The Guild tried honor codes. Both failed. Auster proposed something different: design the incentive structure so that honest behavior is the rational choice. If cheating costs more than it gains — always, automatically, without needing a judge — then the system self-enforces.

**Technical Concepts Covered:**
- Prisoner's Dilemma and dominant strategy analysis
- Nash equilibrium, iterated games, and Axelrod's tournament strategies
- Mechanism design: Vickrey auctions, incentive compatibility, VCG mechanisms
- EIP-1559 gas auction model (base fee + priority tip, fee burning)
- ERC-20 (fungible) and ERC-721 (non-fungible) token standards
- Proof of Stake: staking contracts, lockup multipliers, slashing conditions
- ICP's 8-year lockup model with reward scaling

**Key Character:** Brenn Auster, a cynical but effective economist who replaced guild honor with mathematical self-enforcement. His incentive reform transformed the Traders Guild from a trust-based system to a stake-based one.

---

## Prerequisites

- **Technical:** Python, familiarity with `pandas`, `matplotlib`, basic statistics
- **Conceptual:** Course 03 (smart contracts) recommended; no game theory knowledge required

---

## The Tutorials

**Session 1 (Tutorials 01-05):** Complete — game theory through staking and slashing.

| # | Tutorial | Notebook | Description |
|---|----------|----------|-------------|
| 1 | The Guild's Problem | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/buildLittleWorlds/blockchain-tokens-and-incentives/blob/main/notebooks/tutorial_01_the_guilds_problem.ipynb) | Traders Guild enforcement failures, Prisoner's Dilemma, Dens proximity effects |
| 2 | Game Theory Foundations | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/buildLittleWorlds/blockchain-tokens-and-incentives/blob/main/notebooks/tutorial_02_game_theory_foundations.ipynb) | Nash equilibrium, 8 strategies, Axelrod's tournament, Folk Theorem |
| 3 | Mechanism Design | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/buildLittleWorlds/blockchain-tokens-and-incentives/blob/main/notebooks/tutorial_03_mechanism_design.ipynb) | Vickrey auctions, incentive compatibility, EIP-1559, guild staking mechanism |
| 4 | Token Standards (ERC-20, ERC-721) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/buildLittleWorlds/blockchain-tokens-and-incentives/blob/main/notebooks/tutorial_04_token_standards.ipynb) | Fungible and non-fungible tokens, guild economy, Gini coefficient |
| 5 | Staking and Slashing | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/buildLittleWorlds/blockchain-tokens-and-incentives/blob/main/notebooks/tutorial_05_staking_and_slashing.ipynb) | Staking contracts, ICP lockup model, slashing analysis, delegation |

**Session 2 (Tutorials 06-08):** Coming soon — Liquidity and AMMs, MEV, and the Guild Economy capstone.

| # | Tutorial | Notebook | Description |
|---|----------|----------|-------------|
| 6 | Liquidity and AMMs | *Coming soon* | Constant product formula (x*y=k), Uniswap-style pools, guild commodity trading |
| 7 | MEV and Front-Running | *Coming soon* | Miner Extractable Value, front-running attacks, sandwich attacks on guild trades |
| 8 | Capstone: The Guild Economy | *Coming soon* | Complete token economy: membership tokens, staked reputation, AMM, 1000-round simulation |

---

## Datasets

**New datasets (generated for this course):**

| Dataset | Rows | Description |
|---------|------|-------------|
| `guild_trade_ledger.csv` | 600 | Trade records with prices, parties, outcomes, fraud detection, inspector rulings |
| `game_theory_outcomes.csv` | 300 | Prisoner's dilemma rounds with 8 strategies and payoffs |
| `staking_rewards.csv` | 387 | Staking/slashing simulation with epochs, rewards, penalties, ejections |
| `amm_liquidity_pools.csv` | 200 | Pool states: reserves, prices, constant product, LP tokens |
| `mev_extraction_log.csv` | 150 | Front-running events with profit/loss, extraction types |

**Reused datasets:**

| Dataset | Rows | Description |
|---------|------|-------------|
| `scholars.csv` | 40 | Scholar identities (Brenn Auster's entry) |

---

## Key Concepts

### The Incentive Arc

| Tutorial | Concept | What It Solves |
|----------|---------|---------------|
| 01 | Prisoner's Dilemma | Why rational agents defect even when cooperation is better |
| 02 | Repeated games | Why reputation enables cooperation (Folk Theorem) |
| 03 | Mechanism design | How to engineer games where honesty is dominant |
| 04 | Token standards | How to represent value as programmable state |
| 05 | Staking/slashing | How to make dishonesty expensive |

### Connection to Blockchain

| Auster's Concept | Blockchain Concept |
|-------------------|-------------------|
| Self-enforcing agreements | Smart contract enforcement |
| Guild token (GuildCoin) | ERC-20 fungible tokens |
| Manuscript certificates | ERC-721 non-fungible tokens |
| Staked reputation | Proof of Stake |
| Lockup multipliers | ICP's 8-year neuron model |
| Inspector slashing | Validator slashing (Ethereum 2.0) |

---

## Getting Started

1. Click the Colab badge for Tutorial 1 above
2. Run cells in order
3. Complete the exercises at the end of each tutorial
4. Follow the arc from the Guild's coordination failure through to staked self-enforcement

**Recommended pace:** One tutorial per session.

---

## Related Courses

| Course | Focus |
|--------|-------|
| [01 - The Immutable Record](../01-immutable-record/) | Hash functions, Merkle trees, blockchain data structure |
| [02 - Agreement Without Authority](../02-consensus/) | Byzantine fault tolerance, consensus algorithms |
| [03 - Programmable Trust](../03-smart-contracts/) | Smart contracts, EVM, Solidity, vulnerability analysis |
| [04 - The Mathematics of Trust](../04-cryptographic-foundations/) | Public-key cryptography, ECC, digital signatures |
| **05 - Tokens and Incentive Design** | **Mechanism design, game theory, token economics** |

---

*"A rule says 'don't steal.' An incentive makes stealing cost more than it gains. The first requires a judge. The second requires only arithmetic."*

— Brenn Auster
