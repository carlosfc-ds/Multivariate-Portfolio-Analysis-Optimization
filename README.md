# Multivariate Portfolio Analysis & Optimization in R

## Overview
This project focuses on modeling daily log-returns for 30 Dow Jones stocks (1990–2000) using a **multivariate t-distribution**. It covers the statistical estimation of heavy-tailed distributions and the application of those models to portfolio risk management and constrained optimization.

---

## Problem Summaries

### Problem 1: Likelihood & Risk
*   **Model Fitting:** Estimate the shape matrix $\Lambda$ and use **profile likelihood** to determine the optimal degrees of freedom ($\nu$).
*   **Goal:** Model daily log-returns of 30 Dow Jones stocks using a multivariate $t$-distribution.
*   **Tasks:** Estimate the degrees of freedom ($\nu$) using profile likelihood, determine a 95% confidence interval for $\nu$, and calculate the daily **Value-at-Risk (VaR)** for an equal-weighted portfolio.
*   **Inference:** Construct an asymptotic **95% confidence interval** for $\nu$.
*   **Risk Metrics:** Calculate the daily **Value-at-Risk (VaR)** at the $\alpha = 0.95$ level for an equally-weighted portfolio.

### Problem 2: Portfolio Optimization & Efficient Frontier
*   **Goal:** Find optimal portfolio weights that minimize VaR for a target return.
*   **Tasks:** Write an R function for quadratic optimization, graph the **Efficient Frontier** (Risk-Reward diagram), and identify the "tangency" portfolio (maximizing the **Sharpe Ratio**) under both short-selling and no-short-selling conditions.
*   **VaR Minimization:** Find the optimal portfolio weights $w$ that minimize $VaR_{0.95}$ for a specific target return.
*   **Efficient Frontier:** Plot the risk-reward tradeoff across various return targets.
*   **Sharpe Ratio:** Identify the "Tangency Portfolio" using a daily risk-free rate derived from a 3% annual rate.
*   **Constraint Analysis:** Compare the performance of portfolios with and without short-selling ($w_i \geq 0$).

### Problem 3: CAPM & Stock Beta
*   **Goal:** Analyze a specific stock's relationship to the market.
*   **Tasks:** Calculate the stock's **Beta ($\beta$)**, determine the expected return using the Capital Asset Pricing Model, and partition the variance to find the percentage of market risk.

### Problem 4: Portfolio Beta and Variance
*   **Goal:** Evaluate a three-stock portfolio.
*   **Tasks:** Calculate the portfolio's aggregate Beta and determine its total variance, including both market-related and idiosyncratic (error) risk.

### Problem 5: Time Series Model Selection (AR Models)
*   **Goal:** Compare different Autoregressive models for financial data.
*   **Tasks:** Use `arima()` to fit AR(1) and AR(2) models and select the best fit based on **AIC** and **BIC** criteria.
---

## 🛠️ R Functions & Skills Highlight

### 1. Multivariate Data Manipulation
*   **Data Transformation:** Converting raw price data into daily log-returns using vectorized operations.
*   **Matrix Algebra:** Managing 30-dimension data structures for joint distribution modeling.
*   **`apply(dat, 2, mean)`**: Used to calculate the mean of each column (stock) simultaneously.
*   **`cov(ret)`**: Computes the covariance matrix for the stock returns.
*   **`%*%`**: Performs formal matrix multiplication (essential for calculating portfolio variance: $w^\top \Sigma w$).
*   **`t()`**: Transposes a matrix or vector.
*   **`unlist()` / `matrix()`**: Used to reshape raw data into a structured numerical format for analysis.

### 2. Statistical Modeling
*   **Maximum Likelihood Estimation (MLE):** Implementing profile likelihood loops to find the best-fit parameters for heavy-tailed data.
*   **Quantile Functions:** Utilizing `qt()` to derive the probabilistic components of Value-at-Risk.
*   **`library("mnormt")`**: Used for the multivariate $t$-distribution functions.
    *   **`dmt()`**: Calculates the density of the multivariate $t$-distribution to find the log-likelihood.
*   **`arima(data, order=c(p,d,q))`**: Fits Autoregressive Integrated Moving Average models to time-series data.
*   **`which.max()`**: Identifies the index of the maximum value in a vector (used to find the MLE for $\nu$).
*   **`seq()`**: Generates a sequence of numbers (e.g., `nu.range` or `v.range`) to iterate through possible parameter values.
*   **`qt()`**: The Student $t$ distribution quantile function, used to calculate **Value-at-Risk (VaR)**.
*   **`qchisq()`**: The Chi-squared quantile function, used to find critical values for **Likelihood Ratio Tests** and confidence intervals.

### 3. Optimization
*   **Quadratic Programming:** Using the `quadprog` library (`solve.QP`) to solve the objective function: $\min w^T \Lambda w$.
*   **Linear Constraint Mapping:** Constructing constraint matrices (`Amat`) and vector offsets (`bvec`) to enforce "sum of weights = 1" and "target return = v".
*   **Performance Metrics:** Calculating the Sharpe Ratio and adjusting annual rates (3%) to daily log-scale units.
*   **Short-Selling Logic**: Toggling constraints in the `Amat` (Constraint Matrix) to allow or forbid negative weights.
*   **`library("quadprog")`**: The core library for solving quadratic programming problems.
    *   **`solve.QP()`**: Solves for weights that minimize variance subject to constraints (target return and sum of weights = 1).

### 4. Data Visualization
*   **Efficient Frontier Plotting:** Using base R or `ggplot2` to visualize the relationship between portfolio risk (SD) and expected reward.
*   **`plot(..., type='l')`**: Generates line graphs for the **Efficient Frontier** and Risk-Reward diagrams.
*   **`library("knitr")`**:
    *   **`kable()`**: Formats R data frames and matrices into clean, readable Markdown/PDF tables.
*   **`cat()`**: Outputs specific results (like the estimated $\nu$) directly into the report text.

### 5. Reproducible Research
*   **Literate Programming:** Using `Rnw` (Sweave/knitr) and $\LaTeX$ to generate professional, code-integrated PDF reports.
*   **`plot(..., type='l')`**: Generates line graphs for the **Efficient Frontier** and Risk-Reward diagrams.
*   **`library("knitr")`**:
    *   **`kable()`**: Formats R data frames and matrices into clean, readable Markdown/PDF tables.
*   **`cat()`**: Outputs specific results (like the estimated $\nu$) directly into the report text.



---

## Technical Requirements
*   **Environment:** R, RStudio, and `pdflatex`.
*   **Packages:** `knitr`, `mnormt`, `quadprog`.
*   **Data:** `DowJones30.csv`.
