# Global Manufacturing Network Design: A Stochastic Optimization Approach

## Project Background

Traditional supply chain designs frequently suffer from a fatal flaw: they rely on static, single-point demand forecasts. In highly volatile global markets, a network optimized for a single "average" forecast can become inefficient or fail completely when real-world demand shifts.

This project bridges that critical operational gap for a global consumer goods manufacturer managing potential production facilities across five key regions: **the USA, Germany, Japan, Brazil, and India**. 

By pairing **Mixed-Integer Linear Programming (MILP)** with a **Monte Carlo stress-test pipeline**, this model evaluates facility allocation decisions across 50 distinct randomized demand scenarios. The goal is to move past fragile local optima and identify the **Dominant Design**,the single most resilient network footprint capable of minimizing total global costs while absorbing demand volatility.

## 🚀 Executive Recommendation Summary

Based on the mathematical consensus across 50 simulated demand runs, the optimal global strategy to minimize total network outlays is a **centralized, low-cost export model**. The data proves that it is significantly more profitable to absorb international ocean freight than to bear high domestic Western manufacturing costs and steep fixed facility overhead.

#### 🏭 The Optimal Physical Footprint
* **Expand in India (Primary Export Engine):** Open **both** Low and High-capacity plants to aggressively exploit ultra-low variable manufacturing outlays ($5/unit).
* **Build Regional Hubs (Japan & Brazil):** Activate **High-capacity** plants in Japan and Brazil to absorb regional consumer volumes efficiently and shield against cross-ocean logistics spikes.
* **Bypass Western Production (USA & Germany):** Do **not** open any facilities in the USA or Germany. Despite the USA being the largest consumer market, local fixed overhead makes domestic manufacturing highly inefficient.
---
 #### 🧠 Core Strategic Pillars for Decision-Makers
To execute this layout successfully and maintain long-term supply chain resilience, these three mathematical paradigms proven by this model, must be adopted:

1. **Don't optimize for a single demand forecast:** Real-world market demand is stochastic; your network configuration must be built to survive a wide distribution of volatility.
2. **Prioritize Network Stability:** A configuration that works beautifully in one specific forecast but fails in five others is an operational liability.
3. **Treat Key Plants as Strategic Anchors:** View specialized facilities (such as India and Japan) as vital strategic assets for the entire global grid.
---

## 🗺️ Project Framework

**Problem Statement:** Design an optimal global manufacturing and distribution footprint that minimizes total system costs (fixed operational + variable processing + container logistics) while guaranteeing high demand coverage under significant demand uncertainty.

| Optimization Stage | Core Objective |
| :--- | :--- |
| **Cost Matrix Consolidation** | Compute comprehensive unit delivery costs by synthesizing local variable manufacturing outlays with destination-specific container freight rates. |
| **MILP Baseline Modeling** | Formulate the initial objective function and linear constraints to minimize total network expenses under fixed baseline demand. |
| **Stochastic Simulation** | Run a 50-iteration Monte Carlo simulation tracking independent Gaussian demand deviations for each global market. |
| **Multi-Scenario Evaluation** | Batch-solve the MILP optimization engine over all 50 demand variations to isolate structural patterns in active locations and shipment logistics. |
| **Footprint Analysis** | Profile system-wide risks, build complete layout visualization grids, and measure marginal vs. average cost efficiencies against volume scaling. |

---

## 🔬 Methodology & Mathematical Formulation

### 1. The Optimization Model
The optimization core utilizes a Capacitated Facility Location-Allocation formulation to simultaneously dictate structural assets (where to build) and tactical flows (where to ship).

#### Decision Variables
* $y_{i,s} \in \{0, 1\}$ : Binary indicator; equals $1$ if plant origin $i$ is opened with capacity tier $s$ ($\in \{\text{LOW}, \text{HIGH}\}$), $0$ otherwise.
* $x_{i,j} \geq 0$ : Continuous variable representing the quantity of physical units shipped from plant origin $i$ to market destination $j$.

#### Objective Function
Minimize the combined total network cost ($Z$):
Z = ∑ᵢ∑ₛ FixedCostᵢₛ · yᵢₛ + ∑ᵢ∑ⱼ VariableCostᵢⱼ · xᵢⱼ

#### Constraints
* **Supply Capacity Bounds:** Shipments leaving origin $i$ cannot breach the activated capacity threshold of that facility:
   ∑ⱼ xᵢⱼ ≤ ∑ₛ Capacityᵢₛ · yᵢₛ ∀i
* **Demand Satisfaction:** Market consumption requirements must be fully met by total inbound logistics:<br>
   ∑ᵢ xᵢⱼ = Demandⱼ ∀j

* **Solver Engine:** Formulated via `PuLP` using the open-source high-performance linear solver.

---

### 2. Robustness Testing: Monte Carlo Simulation
To prevent the engineering of a fragile network layout, demand is subjected to a severe coefficient of variation ($CV = 0.5$). 
* For each market, independent scenarios are drawn from a truncated normal distribution:
$$\text{Demand}_j \sim \max\left(0, \, \mathcal{N}(\mu_j, \, 0.5 \times \mu_j)\right)$$
* The model loops through all 50 iterations, dynamically adjusting the demand parameters and re-solving the matrix to extract structural frequencies and cost variance profiles.

---

### 3. Sensitivity & Elasticity Analytics
Post-optimization logs are evaluated using linear regression and elasticity models to map system cost scalability behaviors:
* **Marginal Cost ($\beta_1$):** Explores the baseline incremental variable cost per unit added.
* **Cost Elasticity:** Evaluates the percentage change in total expenditure driven by a $1\%$ change in global market demand.

---

## 📈 Key Insights & Optimization Metrics

### 1. Risk-Averse Consensus Footprints
When subjected to severe demand stress tests, static layouts fail. However, tracking facility activation frequencies over the 50 runs isolates the **"Dominant Footprint"**. This consensus matrix represents a balanced layout that protects margins during recessions while providing scalable volume during economic expansions.

### 2. Demand-Cost Elasticity Profile

| Optimization Metric | Evaluated System Value | Operational Interpretation |
| :--- | :--- | :--- |
| **Demand-Cost Correlation ($r$)** | `0.995` | Network costs are almost completely bound to market volumes; structural overhead is minimized. |
| **Marginal Cost** | `$16.35` / unit | The true systemic expense incurred for every extra unit added across the global distribution grid. |
| **Cost Elasticity** | `1.18` | A value $>1$ marks an **elastic** supply chain: a $1\%$ spike in global demand triggers a $1.18\%$ rise in overall network spend. |
| **Average Cost per Unit** | `$13.88` / unit | System-wide mean benchmark cost across all operational variations. |
| **Min-Max Range Matrix** | `$12.31` to `$15.65` | The full bounded operational financial risk under extreme scenario fluctuations. |

---

## ⚠️ Assumptions & Caveats

* **Linear Scaling:** Unit processing and freight costs are assumed constant (no bulk discounts or spot-market spikes).
* **Static Cost Parameters:** Fixed costs, variable costs, and freight rates remain constant; only demand fluctuates.
* **Instant Logistics:** Assumes zero transit lead times, zero customs delays, and infinite raw material availability.
* **100% Demand Met:** The model strictly forbids stockouts, unserved markets, or order backlogs.
* **Macro Risk Ignored:** Does not factor in currency exchange fluctuations, import tariffs, or localized inflation.
