# 📈 HFT Strategy Optimization: Exact vs. Metaheuristic Approaches

## 1. Project Overview

This project focuses on solving a real-world Finance/Tech optimization
problem:\
**Maximizing the risk-adjusted returns of a High-Frequency Trading (HFT)
strategy.**

We model an **Order Book Imbalance trading strategy** and compare two
optimization approaches:

-   ✅ **Exact Optimization** --- Integer Linear Programming (ILP) using
    PuLP\
-   ✅ **Metaheuristic Optimization** --- Genetic Algorithm (GA) using
    PyGAD

### 🎯 Objective

Maximize the **Sharpe Ratio** of the trading strategy:

Z = (E\[Rₚ − R_f\]) / σₚ

Where: - Rₚ = Portfolio returns - R_f = Risk-free rate - σₚ = Standard
deviation of portfolio returns

------------------------------------------------------------------------

## 2. Dataset Description

-   **Source:** Kaggle -- Cryptocurrency Real-Time Market Data\
-   **Frequency:** 1-second interval tick data\
-   **Format:** CSV

### 📊 Features Used

-   Timestamp\
-   Bid Price\
-   Ask Price\
-   Bid Volume\
-   Ask Volume

### 🔎 Feature Engineering

-   Mid Price = (Bid + Ask) / 2\
-   Order Book Imbalance = (Bid Volume − Ask Volume) / (Bid Volume + Ask
    Volume)\
-   Strategy Returns\
-   Transaction Costs\
-   Maximum Drawdown

------------------------------------------------------------------------

## 3. Mathematical Formulation

### 🔢 Decision Variables

-   **T** → Threshold for Order Book Imbalance\
-   **L** → Stop-loss percentage\
-   **P** → Take-profit percentage

### 🎯 Objective Function

Maximize:

Z = Sharpe Ratio

### 📌 Constraints

-   Maximum Drawdown ≤ 5%\
-   Total Transaction Costs ≤ 10% of Gross Profit\
-   Logical parameter bounds:
    -   0 \< T ≤ 1
    -   0 \< L ≤ 10%
    -   0 \< P ≤ 20%

------------------------------------------------------------------------

## 4. Optimization Approaches

### 🔵 Exact Method -- Integer Linear Programming (PuLP)

-   Discretized search space
-   Guarantees global optimum within discretized bounds
-   Slower for large search spaces
-   Deterministic results

### 🟢 Metaheuristic -- Genetic Algorithm (PyGAD)

-   Population-based search
-   Evolves candidate solutions over 50--100 generations
-   Faster exploration of large search spaces
-   May converge to near-optimal solution

------------------------------------------------------------------------

## 5. Experimental Evaluation

We compare:

-   Runtime
-   Final Sharpe Ratio
-   Convergence Speed
-   Stability of Results

### 📈 Expected Insights

-   ILP provides higher precision for small search spaces.
-   GA scales better for continuous and large parameter domains.
-   Trade-off between computational efficiency and optimality guarantee.

------------------------------------------------------------------------

## 6. Setup and Installation

### 🔧 Prerequisites

-   Python 3.10+
-   Jupyter Notebook

### 📦 Install Dependencies

``` bash
pip install pandas numpy matplotlib pulp pygad jupyter
```

### 📂 Dataset Setup

1.  Download dataset from Kaggle.
2.  Place the CSV file inside:

```{=html}
<!-- -->
```
    /data

### ▶️ Run the Notebook

``` bash
jupyter notebook Optimization_Main.ipynb
```

------------------------------------------------------------------------

## 7. Execution Workflow

1.  **Data Preprocessing**
    -   Clean tick data
    -   Compute imbalance feature
    -   Calculate returns and drawdown
2.  **Exact Method Section**
    -   Run PuLP optimization
    -   Retrieve optimal parameters
3.  **Genetic Algorithm Section**
    -   Initialize population
    -   Evolve over generations
    -   Track convergence
4.  **Visualization & Comparison**
    -   Plot convergence curves
    -   Compare runtime
    -   Compare Sharpe ratios

------------------------------------------------------------------------

## 8. Project Structure

    hft-optimization/
    │
    ├── data/
    │   └── crypto_data.csv
    │
    ├── Optimization_Main.ipynb
    ├── Report.pdf
    ├── members.txt
    ├── submission.txt
    └── README.md

------------------------------------------------------------------------

## 9. Performance Considerations

-   Vectorized computations using NumPy for speed
-   Avoided look-ahead bias in return calculation
-   Transaction cost modeling included
-   Reproducibility ensured via random seed control in GA

------------------------------------------------------------------------

## 10. Limitations

-   Backtesting assumes perfect liquidity
-   No slippage modeling
-   Sharpe Ratio assumes normal return distribution
-   ILP discretization limits continuous precision

------------------------------------------------------------------------

## 11. Future Improvements

-   Add Bayesian Optimization
-   Include slippage modeling
-   Multi-objective optimization (Sharpe + Drawdown)
-   Walk-forward validation
-   Parallel GA execution

------------------------------------------------------------------------

## 12. Individual Contributions

-   **Member 1 (Didula):**
    -   Problem modeling
    -   Mathematical formulation
    -   Exact method implementation (PuLP)
    -   Constraint modeling
-   **Member 2:**
    -   Data preprocessing
    -   Genetic Algorithm implementation
    -   Visualization
    -   Video presentation

------------------------------------------------------------------------

## 📜 License

This project is developed for academic purposes.

------------------------------------------------------------------------

## 📬 Contact

For academic inquiries or collaboration, please contact the project
contributors.
