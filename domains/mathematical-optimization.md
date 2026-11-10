# Mathematical Optimization (Planning, Scheduling and Logistics)

**Problem:** go from a real-world decision (*"schedule 40 nurses across 3 shifts"*, *"plan delivery routes for 12 trucks"*, *"how much of each product should the factory make?"*) to the best possible plan.

← Back to the [main README](../README.md)

These problems are hard to solve by hand, but **solvers** have been very good at them for decades. The difficult part has always been writing the model. That is exactly the part an LLM can now do.

---

## Recommended tool

| | |
|---|---|
| **DSL** | [**Pyomo**](https://www.pyomo.org/) (Python) for linear / mixed-integer models · [**Google OR-Tools**](https://developers.google.com/optimization) (Python) for scheduling and routing |
| **Engine** | Solvers: [HiGHS](https://highs.dev/), CBC, SCIP, OR-Tools CP-SAT (open source) or Gurobi / CPLEX (commercial) |
| **Output** | An optimal (or near-optimal) plan with its objective value |
| **Leaderboard** | [LLM4OR](https://llm4or.github.io/LLM4OR/) |

**Why:**

- Both are **Python**, so LLMs write them easily, and both connect to many solvers.
- The result is **verifiable**: the solver reports whether the plan is feasible and how good it is, and every constraint can be checked.
- Pyomo is a general modeling language; **OR-Tools CP-SAT** is one of the best open-source solvers for scheduling and routing.

---

## Alternatives

| Tool | When to use it |
|---|---|
| [MiniZinc](https://www.minizinc.org/) | A dedicated constraint-modeling language, independent of the solver. |
| Prolog ([SWI-Prolog](https://www.swi-prolog.org/) with [CLP(FD)](https://www.swi-prolog.org/man/clpfd.html)) | Problems that are naturally logic rules: timetables, assignments, valid product configurations. The solver also explains *why* a solution is valid or impossible. |
| [PuLP](https://coin-or.github.io/pulp/) | Very simple linear models in Python. |
| [CVXPY](https://www.cvxpy.org/) | Convex optimization (finance, control, machine learning). |
| [JuMP](https://jump.dev/) | Julia, high performance. |
| [gurobipy](https://www.gurobi.com/) | When you already have a Gurobi licence. |

---

## Benchmarks

**Best model right now:** [LLM4OR leaderboard](https://llm4or.github.io/LLM4OR/). It comes from a survey that cleaned the main optimization-modeling datasets (which had many errors) and re-evaluated models on them. It is published as an image and may not include the newest models.

| Benchmark | What it measures | Results |
|---|---|---|
| **LLM4OR** | Cleaned versions of the existing optimization-modeling benchmarks, with a fair comparison across models. | [**Leaderboard**](https://llm4or.github.io/LLM4OR/) · [Survey](https://arxiv.org/abs/2508.10047) |
| IndustryOR | 100 real-world operations-research problems from 13 industries. | No public leaderboard · [Paper](https://arxiv.org/abs/2405.17743) |
| MIPLIB-NL | Industrial-scale problems built from MIPLIB instances. Systems that do well on older benchmarks drop sharply here. | No public leaderboard · [Paper](https://arxiv.org/abs/2602.10450) |
