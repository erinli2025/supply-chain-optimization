# Supply Chain Optimization – CVXPY Model

This is a course project for the Optimization for Data Science course at Tilburg University (2025 Spring Semester). The task was to model a real-world supply chain problem based on a World Food Programme (WFP) case in Ethiopia, where food needs to be distributed from suppliers to ports, warehouses, and refugee camps at minimum cost.

## My Contribution

I was responsible for building the initial linear programming model using Python and CVXPY, including:

- Defining decision variables for multi-layer distribution (supplier-port-warehouse-camp)
- Creating the objective function (total transportation cost)
- Modeling constraints such as demand fulfillment, port/warehouse capacities, and flow balance
- Writing and testing the code on synthetic test cases for validation

## Tools Used

- Python  
- CVXPY  
- NumPy  


## Output

The model produces an optimal transportation plan that minimizes cost while satisfying real-world constraints. This part was handed over to teammates for further refinement (integer programming, sensitivity analysis, final reporting).
