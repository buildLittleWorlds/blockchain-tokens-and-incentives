# Dataset Reference Card: Course 05 — Tokens and Incentive Design

> *"Do not ask whether the guild member will cheat. Ask what it will cost them."*
> — Brenn Auster, *Self-Enforcing Agreements* (Year 867)

---

## Overview

| Type | Dataset | Rows | Description |
|------|---------|------|-------------|
| New | `guild_trade_ledger.csv` | 600 | Traders Guild transaction records with prices, disputes, fraud |
| New | `game_theory_outcomes.csv` | 300 | Prisoner's dilemma tournament: 30 matches x 10 rounds |
| New | `staking_rewards.csv` | 387 | Staking/slashing simulation across 20 epochs, 20 stakers |
| New | `amm_liquidity_pools.csv` | 200 | Automated market maker: 4 pools x 50 state transitions |
| New | `mev_extraction_log.csv` | 150 | MEV extraction events: sandwich attacks, front-running, arbitrage |
| Reused | `scholars.csv` | 40 | Densworld scholars — guild members drawn from this registry |

---

## New Datasets

### guild_trade_ledger.csv

| Rows | Key Columns | Encyclopedia Entities |
|------|-------------|----------------------|
| 600 | trade_id, seller, buyer, commodity, outcome, fraud_detected | Brenn Auster, Traders Guild, Western Reaches, Threshold |

**What it contains:**
- 600 trade transactions across Years 860-880
- 16 commodities traded on 12 routes
- 30 guild members as buyers/sellers
- Outcome categories: completed (70%), disputed (8%), defaulted (7%)
- Dispute types: quality, quantity, timing, substitution, non_delivery
- Inspector involvement and rulings (including bribery)
- Dens proximity scores per route (Threshold: 0.9, Capital: 0.1)

| outcome | meaning |
|---------|---------|
| completed | Trade fulfilled (with or without minor dispute) |
| disputed | Formal dispute filed, resolution pending |
| defaulted | One party failed to deliver |

| inspector_ruling | meaning |
|-------------------|---------|
| seller_liable | Seller at fault |
| buyer_liable | Buyer at fault |
| split_liability | Shared fault |
| insufficient_evidence | Inconclusive |
| inspector_bribed | Inspector compromised |

**Teaching use:**
- Tutorial 01: Motivate mechanism design — show enforcement failures
- Tutorial 03: Auction data for mechanism design exercises
- Tutorial 08 (capstone): Full economy simulation substrate

**Critical rows:** Trades on Threshold routes show highest fraud rates and inspector bribery — this is where Auster's mechanism design is most needed.

---

### game_theory_outcomes.csv

| Rows | Key Columns | Encyclopedia Entities |
|------|-------------|----------------------|
| 300 | match_id, strategy_a, strategy_b, action_a, action_b, payoff_a, payoff_b | Guild members as game players |

**What it contains:**
- 30 matches of iterated Prisoner's Dilemma (10 rounds each)
- 8 strategies: always_cooperate, always_defect, tit_for_tat, generous_tit_for_tat, random, grim_trigger, pavlov, suspicious_tit_for_tat
- Payoff matrix: T=5, R=3, P=1, S=0
- Cumulative payoffs tracked per round
- Cooperation rate per player over time
- Dens interference flag (5% chance of action flip)

| strategy | description |
|----------|-------------|
| always_cooperate | Always cooperate regardless |
| always_defect | Always defect regardless |
| tit_for_tat | Start cooperate, copy opponent's last move |
| generous_tit_for_tat | Tit-for-tat but forgive 10% of defections |
| random | 50/50 cooperate/defect |
| grim_trigger | Cooperate until first defection, then always defect |
| pavlov | Repeat last action if it paid well; switch otherwise |
| suspicious_tit_for_tat | Start defect, then copy opponent |

**Teaching use:**
- Tutorial 01: Introduce the Prisoner's Dilemma with guild trade data
- Tutorial 02: Full game theory analysis — Nash equilibrium, strategy performance
- Tutorial 02: Tit-for-tat dominance in repeated games

---

### staking_rewards.csv

| Rows | Key Columns | Encyclopedia Entities |
|------|-------------|----------------------|
| 387 | epoch, staker, lockup_years, stake_balance, behavior, slash_amount, status | 20 guild members as validators |

**What it contains:**
- 20 stakers across 20 epochs (some ejected early → 387 not 400)
- Lockup durations: 1, 2, 4, or 8 years (ICP model)
- Lockup multiplier: 1x, 1.5x, 2.5x, 4x (longer lockup = higher rewards)
- Validator behaviors: honest, late_attestation, missed_block, double_signing, equivocation
- Penalties for minor infractions, slashing for major violations
- Ejection after 3 cumulative violations

| behavior | severity | consequence |
|----------|----------|-------------|
| honest | none | Full reward |
| late_attestation | minor | 10% reward reduction |
| missed_block | moderate | 30% reward reduction |
| double_signing | major | 10% stake slashed |
| equivocation | severe | 33% stake slashed |

| status | meaning |
|--------|---------|
| active | Normal operation |
| penalized | Minor penalty applied |
| slashed | Major slash event |
| ejected | Removed from validator set (3+ violations) |

**Teaching use:**
- Tutorial 05: Staking mechanics — lockup, rewards, slashing
- Tutorial 05: ICP's 8-year lockup and reward scaling analysis
- Tutorial 08 (capstone): Staking as part of the full guild economy

**Critical rows:** Stakers with 8-year lockup who get ejected show the tension between long commitment and catastrophic failure.

---

### amm_liquidity_pools.csv

| Rows | Key Columns | Encyclopedia Entities |
|------|-------------|----------------------|
| 200 | pool, action, reserve_a, reserve_b, constant_product_k, slippage_pct | 4 commodity pools |

**What it contains:**
- 4 liquidity pools (commodity pairs), 50 state transitions each
- Actions: swap (60%), add_liquidity (25%), remove_liquidity (15%)
- Constant product invariant: k = reserve_a * reserve_b
- 0.3% swap fee
- Slippage percentage per swap
- LP token tracking (minting on add, burning on remove)
- Pool TVL (total value locked)

| pool | commodities |
|------|-------------|
| iron_ore/salt_crystal | Base metals / minerals |
| manuscript_vellum/amber_resin | Scholarly materials |
| copper_ingot/timber_cedar | Construction materials |
| dye_indigo/grain_winter | Luxury / staple goods |

**Teaching use:**
- Tutorial 06 (session 2): AMM mechanics — constant product formula, slippage, impermanent loss
- Tutorial 08 (capstone): AMM as the exchange layer of the guild economy

---

### mev_extraction_log.csv

| Rows | Key Columns | Encyclopedia Entities |
|------|-------------|----------------------|
| 150 | mev_type, extractor, victim, extractor_profit, victim_loss, net_profit | Guild validators as extractors |

**What it contains:**
- 150 MEV extraction events across 4 pools
- 6 MEV types: sandwich_attack, front_run, back_run, liquidation, arbitrage, just_in_time_liquidity
- Profit/loss for extractor and victim
- Gas costs (extraction isn't free)
- Net profit (some extractions are unprofitable after gas)
- Detection difficulty ratings

| mev_type | description | victim_harm |
|----------|-------------|-------------|
| sandwich_attack | Front-run + back-run victim's swap | Direct |
| front_run | Trade before victim to move price | Direct |
| back_run | Trade after victim to capture residual | None |
| liquidation | Liquidate undercollateralized positions | Indirect |
| arbitrage | Correct cross-pool price differences | None |
| just_in_time_liquidity | Add/remove liquidity around large swaps | None |

**Teaching use:**
- Tutorial 07 (session 2): MEV analysis — the "observer effect" of transparent mempools
- Tutorial 08 (capstone): MEV as a system health metric

---

## Reused Datasets

| Dataset | Rows | Source | Used For |
|---------|------|--------|----------|
| `scholars.csv` | 40 | Core Densworld | Guild member identities, affiliations, specialties |

---

## Cross-Dataset Connections

### The Incentive Design Pipeline

```
guild_trade_ledger.csv         game_theory_outcomes.csv
  (enforcement failures)    →    (why defection dominates)
         ↓                              ↓
         └──────────┬───────────────────┘
                    ↓
            Mechanism Design
            (Tutorial 03: design games with good equilibria)
                    ↓
         ┌──────────┴──────────┐
         ↓                     ↓
  staking_rewards.csv    Token Standards
  (stake to participate,  (ERC-20/721 as
   lose for misbehavior)  guild currency)
         ↓                     ↓
         └──────────┬──────────┘
                    ↓
        amm_liquidity_pools.csv    mev_extraction_log.csv
        (automated exchange)    →  (when validators extract value)
                    ↓
              Guild Economy
              (Capstone: Tutorial 08)
```

### The Auster Arc

1. **The Problem** — `guild_trade_ledger.csv` shows 30% of trades have disputes, inspectors can be bribed
2. **The Theory** — `game_theory_outcomes.csv` shows defection dominates in one-shot games, but tit-for-tat wins in repeated play
3. **The Design** — Mechanism design turns insights into rules: make cooperation the dominant strategy
4. **The Implementation** — `staking_rewards.csv` shows stake-based enforcement: 8-year lockups align incentives
5. **The Exchange** — `amm_liquidity_pools.csv` provides automated, trustless commodity trading
6. **The Risk** — `mev_extraction_log.csv` shows that even well-designed systems can be exploited by those who see transactions first

### Connection to Previous Courses

- **Course 01** (Immutable Record): Trade records need tamper-proof storage
- **Course 02** (Consensus): Guild validators must agree on trade outcomes
- **Course 03** (Smart Contracts): Token standards ARE smart contracts; staking IS contract logic
- **Course 04** (Cryptography): Digital signatures authenticate trade participants

---

## Quick Start

```python
import pandas as pd

BASE_URL = "https://raw.githubusercontent.com/buildLittleWorlds/densworld-datasets/main/data/"

# Load all Course 05 datasets
guild_trades = pd.read_csv(BASE_URL + "guild_trade_ledger.csv")
game_theory = pd.read_csv(BASE_URL + "game_theory_outcomes.csv")
staking = pd.read_csv(BASE_URL + "staking_rewards.csv")
amm_pools = pd.read_csv(BASE_URL + "amm_liquidity_pools.csv")
mev_log = pd.read_csv(BASE_URL + "mev_extraction_log.csv")

# Reused
scholars = pd.read_csv(BASE_URL + "scholars.csv")

# Example queries
# 1. Fraud rate by trade route
guild_trades.groupby('trade_route')['fraud_detected'].mean().sort_values(ascending=False)

# 2. Best strategy in the Prisoner's Dilemma tournament
final_rounds = game_theory[game_theory['round'] == 10]
final_rounds.groupby('strategy_a')['cumulative_payoff_a'].mean().sort_values(ascending=False)

# 3. Average yield by lockup duration
staking.groupby('lockup_years')['annual_yield_pct'].first()

# 4. Total MEV extracted by type
mev_log.groupby('mev_type')['net_profit'].sum().sort_values(ascending=False)
```

---

> *"The Capital tried rules. The Guild tried honor. Both failed. I tried mathematics — and discovered that honesty is just the cheapest strategy."*
> — Brenn Auster, *On the Alignment of Interest and Obligation* (Year 875)
