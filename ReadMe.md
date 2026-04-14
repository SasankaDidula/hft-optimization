# HFT Strategy Optimization: Exact vs. Metaheuristic Approaches

## 1. Project Overview

This project solves a real-world **Finance/Tech optimization problem**:
**Maximizing the risk-adjusted returns of a High-Frequency Trading (HFT) strategy.**

We model an **Order Book Imbalance trading strategy** on real Binance BTC/USDT tick data and compare two optimization approaches:

- **Exact Optimization** — Branch & Bound with Recursive Zoom
- **Metaheuristic Optimization** — Genetic Algorithm (GA) using PyGAD

### Objective

Maximize the **annualized Sharpe Ratio**:

```
S = (E[Rp - Rf]) / sigma_p  *  sqrt(bars_per_day * 365)
```

Where Rp = portfolio returns, Rf = risk-free rate, sigma_p = return volatility.

---

## 2. Dataset Description

- **Source:** Binance Public Data API (`https://data.binance.vision`)
- **Asset:** BTC/USDT Aggregated Trades
- **Frequency:** 1-second interval tick data (resampled from raw trade data)
- **Date:** 2024-01-01
- **Type:** Real-world data, downloaded programmatically in the notebook

### Features Used

| Feature | Description |
|---|---|
| Mid Price | (Last trade price per 1-second bar) |
| Buy Volume | Aggregated taker-buy volume per bar |
| Sell Volume | Aggregated taker-sell (maker) volume per bar |
| Order Book Imbalance | (Buy Vol - Sell Vol) / (Buy Vol + Sell Vol) |
| Mid Price Returns | Percentage change of mid price |

---

## 3. Mathematical Formulation

### Decision Variables

| Variable | Description | Domain |
|:---:|---|---|
| T | Order Book Imbalance Threshold | (0.01, 1.0] |
| L | Stop-Loss percentage | (0.1, 10.0] % |
| P | Take-Profit percentage | (0.1, 20.0] % |

### Objective Function

Maximize: `S(T, L, P) = annualized Sharpe Ratio`

### Constraints

| Constraint | Condition | Rationale |
|---|---|---|
| Risk Control | Max Drawdown <= 10% | Prevents catastrophic capital erosion |
| Cost Efficiency | Transaction Costs <= 20% of Gross Profit | Ensures profitability net of fees |
| Statistical Significance | Trade Count >= 50 | Guards against overfitting |

---

## 4. Optimization Approaches

### Exact Method — Branch & Bound with Recursive Zoom

- Discretizes the 3D parameter space into a grid (branching)
- Evaluates all grid points via backtesting (bounding)
- Prunes all regions except the best neighborhood (pruning)
- Recursively refines the grid around the incumbent solution (zoom)
- Guarantees global optimum within grid resolution
- Deterministic results

### Metaheuristic — Genetic Algorithm (PyGAD)

- Population-based search with 20 individuals
- Tournament selection, single-point crossover, random mutation
- Evolves over 50 generations with early stopping
- Constraints enforced via penalty-based fitness function
- Explores continuous space between grid points
- May converge to near-optimal solution

---

## 5. Experimental Evaluation

We compare across multiple dimensions:

- **Solution Quality**: Sharpe Ratio, Net Profit, Win Rate
- **Risk Metrics**: Max Drawdown, Transaction Costs
- **Runtime**: Wall-clock seconds for each method
- **Scalability**: Runtime and solution quality vs. dataset size (10% to 100%)
- **Convergence**: How quickly each method finds good solutions
- **Constraint Satisfaction**: Feasibility of final solutions

---

## 6. Setup and Installation

### Prerequisites

- Python 3.10+
- Jupyter Notebook

### Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn scipy pulp pygad requests jupyter
```

### Run the Notebook

```bash
jupyter notebook Optimization_Main.ipynb
```

The notebook automatically downloads the Binance dataset on first run.

---

## 7. Project Structure

```
hft-optimization/
│
├── data/                        # Auto-downloaded Binance tick data
│   └── BTCUSDT-aggTrades-*.csv
│
├── Optimization_Main.ipynb      # Main notebook (all code + analysis)
├── ReadMe.md                    # This file
├── members.txt                  # Group member details
├── submission.txt               # Submission metadata
└── .gitignore
```

---

## 8. Notebook Sections

1. **Import Libraries** — Dependencies and reproducibility setup
2. **Load & Explore Dataset** — Download Binance data, preprocess
3. **Exploratory Data Analysis** — Statistical properties, distributions, autocorrelation
4. **Mathematical Formulation** — Formal optimization problem definition
5. **Backtesting Engine** — Vectorized strategy simulator
6. **Branch & Bound (Exact)** — Recursive zoom optimization
7. **Genetic Algorithm (GA)** — PyGAD metaheuristic optimization
8. **Results Comparison** — Tables, charts, radar plots, equity curves
9. **Scalability Analysis** — Runtime and quality vs. data size
10. **Complexity & NP-Hardness** — Theoretical discussion
11. **Summary & Key Findings** — Trade-offs and future work
12. **Individual Contributions** — Per-member task breakdown

---

## 9. Key Results

| Metric | Branch & Bound (Exact) | Genetic Algorithm |
|---|---|---|
| Search Type | Discrete, deterministic | Continuous, stochastic |
| Optimality | Global within grid resolution | Near-optimal (no formal guarantee) |
| Scalability | Exponential in dimensions | Linear in dimensions |
| Constraint Handling | Post-hoc penalty | Embedded in fitness |

---

## 10. Individual Contributions

- **Member 1 (NANAYAKKARA N.G.S.D M  - MS25948592):**
  - Problem selection & scoping
  - Mathematical formulation & constraints
  - Branch & Bound implementation
  - Back testing engine development
  - Scalability analysis 

- **Member 2 (KALUARACHCHI N.A. - MS25951608):**
  - Binance API integration & Dataset sourcing
  - Data preprocessing & feature engineering
  - Genetic Algorithm (PyGAD) implementation
  - EDA & visualization 
---

## 11. Limitations

- Backtesting assumes perfect liquidity (no slippage)
- Sharpe Ratio assumes approximately normal return distribution
- B&B discretization limits continuous precision
- GA results may vary slightly between runs (mitigated by seed control)

## 12. Future Improvements

- Walk-Forward Analysis for out-of-sample validation
- Bayesian Optimization (e.g., Optuna) for sample efficiency
- Monte Carlo stress testing for robustness evaluation
- Multi-Objective Optimization (NSGA-II) for Pareto frontiers
- Position sizing as a 4th decision variable

---
