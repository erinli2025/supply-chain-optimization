# WFP Ethiopia Supply Chain Optimization

A linear programming model to minimize food distribution costs for the UN World Food Programme (WFP) in Ethiopia, ensuring nutritional requirements are met for 1.1M+ beneficiaries across 32 refugee camps.

## Problem

Food must travel through a 4-layer supply chain:
```
Supplier Countries → Ports → Warehouses → Beneficiary Camps
```
The model selects the cheapest combination of procurement and transportation routes while satisfying nutritional constraints for every camp.

## My Contribution

- Preprocessed raw multi-sheet Excel data into 11,834 enumerated routes with aggregated cost per ton
- Formulated the LP model: decision variables, objective function, and 4 constraint types
- Implemented and solved using `cvxpy`

The team subsequently extended this to an integer programming formulation.

## Model

**Decision variable:** $x_i$ = quantity (tons) shipped along route $i$

**Objective:** Minimize total cost $\sum_i c_i \cdot x_i$

**Constraints:**
1. Supplier procurement capacity
2. Port throughput capacity
3. Warehouse throughput capacity
4. Nutritional demand satisfaction (32 camps × 11 nutrients)

## Results

- **Optimal monthly cost: ~$31M** for 1.1M+ beneficiaries
- 128 active routes selected out of 11,834 possible
- Djibouti port handles ~80% of total volume
- Primary suppliers: India (Sorghum/Millet), Turkey (Corn Soya Blend, Wheat Flour)

## Note on Solver Status

The solver returns `optimal_inaccurate` rather than `optimal`. 
This is a numerical scaling issue: the nutrient constraints span 
several orders of magnitude (Energy ~1e10 vs. micronutrients ~1e3), 
making it difficult for the solver to satisfy its convergence tolerance.

However, the solution is **stable and practically reliable**:
- The result is consistent across multiple solvers (~$36M)
- All constraints are satisfied within acceptable tolerance
- The gap between primal and dual objective is < 0.01%

In a production setting, this would be addressed with a commercial 
solver (e.g. Gurobi) or more aggressive constraint scaling.

## 📓 View Notebook

👉 [Open in nbviewer](https://nbviewer.org/github/erinli2025/supply-chain-optimization/blob/main/supply_chain_lp_model.ipynb)

## Repository Structure

```
supply-chain-optimization/
├── supply_chain_lp_model.ipynb   # LP model (preprocessing + formulation + results)
├── optimized_results.csv         # Optimal routes and quantities
├── data/
│   ├── Data_OPT_for_DS.xlsx                          # Raw data (nodes, nutrients, costs)
│   └── Updated_Procurement_and_Transport_Costs_v2.csv # Preprocessed route cost table
└── docs/
    └── Assignment_OPT_for_DS.pptx                    # Original assignment brief
```

## Setup

```bash
pip install cvxpy pandas openpyxl
jupyter notebook supply_chain_lp_model.ipynb
```

## Tools

- Python, pandas, numpy
- cvxpy (LP solver: SCS)
