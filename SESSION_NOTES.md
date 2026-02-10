# Session Notes: Course 05 — Tokens and Incentive Design

## Session 1 (2026-02-10)

### What Was Built

| # | Notebook | Size | Status |
|---|----------|------|--------|
| 01 | tutorial_01_the_guilds_problem.ipynb | ~35 KB | Complete |
| 02 | tutorial_02_game_theory_foundations.ipynb | ~38 KB | Complete |
| 03 | tutorial_03_mechanism_design.ipynb | ~37 KB | Complete |
| 04 | tutorial_04_token_standards.ipynb | ~32 KB | Complete |
| 05 | tutorial_05_staking_and_slashing.ipynb | ~37 KB | Complete |

**Total:** ~179 KB across 5 notebooks

### Also Created
- `data/DATASET_REFERENCE_CARD.md` — Full reference card for all 5 datasets
- `README.md` — Partial (tutorials 06-08 noted as "Coming soon")
- 5 new datasets: guild_trade_ledger.csv (600 rows), game_theory_outcomes.csv (300 rows), staking_rewards.csv (387 rows), amm_liquidity_pools.csv (200 rows), mev_extraction_log.csv (150 rows)
- Generation script: `_scripts/generate_blockchain_tokens_datasets.py` (seed=42)

### What Remains (Session 2)

*Completed — see Session 2 below.*

### Design Decisions Made

1. **Kept tutorials 02 and 03 separate** (as suggested in COURSE_DETAILS.md). Game theory foundations needed full space for Nash equilibrium, 8 strategies, tournament simulation, and the Folk Theorem. Mechanism design added Vickrey auctions, VCG, EIP-1559, and IC verification.
2. **Tutorial 04 implements full ERC-20 and ERC-721 in Python** — not Solidity. Follows the series pattern of Python implementations with blockchain parallels. Includes allowance pattern, Gini coefficient analysis, and Lorenz curves.
3. **Tutorial 05 models ICP's lockup multipliers** (1x/1.5x/2.5x/4x for 1/2/4/8 year lockups) — connects to the Williams transcript from CONNECTION_MAP.md. Monte Carlo IC verification proves honest staking is dominant.
4. **staking_rewards.csv has 387 rows** (not target 400) because some stakers are ejected before epoch 20 after accumulating 3+ violations. This is realistic behavior, not a bug.
5. **Notebooks run slightly larger than 25 KB target** (~32-38 KB each). The material is dense — game theory, mechanism design, and token economics each need substantial implementation space. The full session stays within ~179 KB.

### Key Classes and Functions Built

| Notebook | Key Implementations |
|----------|-------------------|
| 01 | `prisoners_dilemma()`, trade-to-PD mapping, enforcement failure analysis |
| 02 | `find_nash_equilibria()`, `check_dominance()`, 8 strategy functions, `play_match()`, `play_match_with_noise()`, Folk Theorem δ threshold |
| 03 | `first_price_auction()`, `vickrey_auction()`, `vcg_mechanism()`, `check_incentive_compatibility()`, `eip1559_auction()`, `guild_staking_mechanism()` |
| 04 | `ERC20` class (full standard), `ERC721` class (full standard), `ERC1155` sketch, Gini coefficient, Lorenz curves |
| 05 | `StakingContract` class (stake/process_epoch/slashing), ICP lockup model, `DelegatedStaking` class, Monte Carlo IC verification |

---

## Session 2 (2026-02-10)

### What Was Built

| # | Notebook | Status |
|---|----------|--------|
| 06 | tutorial_06_liquidity_and_amms.ipynb | Complete |
| 07 | tutorial_07_mev_and_front_running.ipynb | Complete |
| 08 | tutorial_08_capstone_the_guild_economy.ipynb | Complete |

### Also Updated
- `README.md` — Updated with Colab badges for tutorials 06-08, added AMM/MEV/capstone concepts

### Design Decisions Made

1. **Tutorial 06 builds a full `ConstantProductAMM` class** with swap_a_for_b/swap_b_for_a, add_liquidity/remove_liquidity, LP token tracking, and fee collection. Impermanent loss formula (2√r/(1+r) - 1) is derived and validated against the dataset. Arbitrage function demonstrates price discovery.
2. **Tutorial 07 implements `SimpleAMM` for MEV demonstrations** — front-running and sandwich attack simulations with detailed profit/victim-loss accounting. `FairOrderingSimulator` compares FIFO, attacker-optimal, and random ordering. Detection heuristics for sandwich and front-run patterns.
3. **Tutorial 08 capstone runs 30 agents for 1,000 rounds** with three strategies (60% honest, 25% opportunistic, 15% predatory). Four economy layers: GuildToken (ERC-20), ReputationSystem (staking/slashing), CommodityPool (AMM), and MEV extraction. System health dashboard tracks Gini, participation, collusion risk, TVL, and composite health score.
4. **Cross-dataset validation** in Tutorial 08 compares simulation patterns to all 5 pre-generated datasets, validating that staking-based detection outperforms historical enforcement and that honest strategies dominate.
5. **Parameter sensitivity exercises** test slash rate variations and adversarial scenarios (50% predatory population) to show system resilience.

### Key Classes and Functions Built

| Notebook | Key Implementations |
|----------|-------------------|
| 06 | `ConstantProductAMM` class (full Uniswap V2 model), `impermanent_loss()`, `compute_arbitrage()`, slippage analysis |
| 07 | `SimpleAMM` class (MEV demo), `simulate_sandwich()`, `detect_sandwich()`, `detect_front_runs()`, `FairOrderingSimulator` class |
| 08 | `GuildToken` class, `ReputationSystem` class, `CommodityPool` class, `GuildAgent` class, `GuildEconomy` class (full simulation engine), `compute_health_score()` |

### Course Status

**COMPLETE.** All 8 tutorials built across 2 sessions. Course covers the full arc from Prisoner's Dilemma through agent-based economic simulation.
