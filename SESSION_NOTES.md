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

| # | Title | Description |
|---|-------|-------------|
| 06 | Liquidity and AMMs | Constant product formula (x*y=k). Uniswap-style pool implementation. Guild commodity trading with automated pricing. Impermanent loss analysis. |
| 07 | MEV and Front-Running | Miner/Maximum Extractable Value. Simulate front-running and sandwich attacks on guild trades. Detection strategies. Flashbots-style ordering. |
| 08 | Capstone: The Guild Economy | Complete token economy simulation: guild membership tokens (ERC-20), staked reputation with slashing, AMM for commodity trading, 1000-round simulation, system health metrics (Gini, collusion risk, participation). |

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

### Continuation Prompt

```
I'm continuing Course 05 (Tokens and Incentive Design) in the blockchain series. This is session 2 of 2.

Read SESSION_NOTES.md in courses/blockchain-series/05-tokens-and-incentives/ for full context.

Session 1 built tutorials 01-05 (~179 KB). This session builds tutorials 06-08.

Notebooks to build:
| # | Title | Description |
|---|-------|-------------|
| 06 | Liquidity and AMMs | Constant product formula (x*y=k), Uniswap-style pool, guild commodity trading, impermanent loss |
| 07 | MEV and Front-Running | MEV types, front-running/sandwich attacks, detection strategies, Flashbots ordering |
| 08 | Capstone: The Guild Economy | Complete token economy: ERC-20 membership, staked reputation, AMM trading, 1000-round simulation, system health |

Datasets already generated (use from GitHub BASE_URL):
- amm_liquidity_pools.csv (200 rows) — for Tutorial 06
- mev_extraction_log.csv (150 rows) — for Tutorial 07
- All 5 datasets — for Tutorial 08 capstone

After building, update README.md (fill in tutorials 06-08 Colab badges), git commit + push to buildLittleWorlds/blockchain-tokens-and-incentives.
```
