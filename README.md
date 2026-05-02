# Multivariate-Portfolio-Analysis-Optimization
This project focuses on modeling daily log-returns for 30 Dow Jones stocks (1990–2000) using a **multivariate t-distribution**. It covers the statistical estimation of heavy-tailed distributions and the application of those models to portfolio risk management and constrained optimization.
# Homework 5: Multivariate Portfolio Analysis & Optimization

## Overview
This project focuses on modeling daily log-returns for 30 Dow Jones stocks (1990–2000) using a **multivariate t-distribution**. It covers the statistical estimation of heavy-tailed distributions and the application of those models to portfolio risk management and constrained optimization.

---

## Problem Summaries

### Problem 1: Likelihood & Risk
*   **Model Fitting:** Estimate the shape matrix $\Lambda$ and use **profile likelihood** to determine the optimal degrees of freedom ($\nu$).
*   **Inference:** Construct an asymptotic **95% confidence interval** for $\nu$.
*   **Risk Metrics:** Calculate the daily **Value-at-Risk (VaR)** at the $\alpha = 0.95$ level for an equally-weighted portfolio.

### Problem 2: Mean-VaR Optimization
*   **VaR Minimization:** Find the optimal portfolio weights $w$ that minimize $VaR_{0.95}$ for a specific target return.
*   **Efficient Frontier:** Plot the risk-reward tradeoff across various return targets.
*   **Sharpe Ratio:** Identify the "Tangency Portfolio" using a daily risk-free rate derived from a 3% annual rate.
*   **Constraint Analysis:** Compare the performance of portfolios with and without short-selling ($w_i \geq 0$).

---

## Key R Skills Used

### 1. Financial Data Engineering
*   **Data Transformation:** Converting raw price data into daily log-returns using vectorized operations.
*   **Matrix Algebra:** Managing 30-dimension data structures for joint distribution modeling.

### 2. Statistical Modeling
*   **Maximum Likelihood Estimation (MLE):** Implementing profile likelihood loops to find the best-fit parameters for heavy-tailed data.
*   **Quantile Functions:** Utilizing `qt()` to derive the probabilistic components of Value-at-Risk.

### 3. Quantitative Optimization & Finance
*   **Quadratic Programming:** Using the `quadprog` library (`solve.QP`) to solve the objective function: $\min w^T \Lambda w$.
*   **Linear Constraint Mapping:** Constructing constraint matrices (`Amat`) and vector offsets (`bvec`) to enforce "sum of weights = 1" and "target return = v".
*   **Performance Metrics:** Calculating the Sharpe Ratio and adjusting annual rates (3%) to daily log-scale units.

### 4. Data Visualization
*   **Efficient Frontier Plotting:** Using base R or `ggplot2` to visualize the relationship between portfolio risk (SD) and expected reward.

### 5. Reproducible Research
*   **Literate Programming:** Using `Rnw` (Sweave/knitr) and $\LaTeX$ to generate professional, code-integrated PDF reports.

---

## Technical Requirements
*   **Environment:** R, RStudio, and `pdflatex`.
*   **Packages:** `knitr`, `mnormt`, `quadprog`.
*   **Data:** `DowJones30.csv`.
