# Quantum Grid Optimization

A framework for optimizing power generation and distribution across electrical grids, comparing classical methods against Qiskit-based quantum optimization.

---

## Overview

Electrical grids face a constant optimization problem: which generators to turn on, how much power each should produce, and how to route electricity across transmission lines to meet demand at the lowest cost. This is known as Unit Commitment and Optimal Power Flow.

Classical methods handle this today, but the problem is growing harder. Renewable sources like solar and wind are intermittent and uncertain. Demand patterns are shifting. The grid is getting larger and more complex. Solvers run every 5 to 15 minutes, and even small improvements in solution quality translate to billions of dollars in savings annually.

This project explores whether quantum optimization via Qiskit can offer a different approach, benchmarked honestly against classical baselines.

---

## Problem Statement

Given:

* a network of generators with different costs, capacities, and ramp rates
* transmission lines with capacity limits
* demand at each node that varies over time
* uncertainty from renewable generation

Determine:

* which generators to turn on or off (unit commitment)
* how much power each produces (economic dispatch)
* how power flows across the network (optimal power flow)

Such that:

> total cost is minimized while meeting demand and respecting physical constraints.

---

## Goals

* Model a simplified power grid as a network optimization problem
* Implement classical baselines (greedy dispatch, LP, mixed-integer programming)
* Formulate the problem as a QUBO for quantum solvers
* Solve using Qiskit (QAOA, VQE)
* Compare classical and quantum methods on solution quality, runtime, and scaling

---

## Real-World Applications

**Grid dispatch** — Operators decide every few minutes which plants to run and at what output. Suboptimal decisions waste fuel and money.

**Renewable integration** — Solar and wind output is uncertain. The grid must handle variability without blackouts or over-generation.

**Demand response** — Shifting industrial load during peaks is another binary decision layer on top of generation scheduling.

**Microgrid management** — Small local grids (military bases, hospitals, remote communities) with batteries, solar, and backup generators.

**Grid resilience** — After a storm or failure, deciding which lines to restore first and how to reroute power.

---

## Why Quantum?

Unit commitment is a mixed-integer optimization problem. The on/off state of each generator is binary, and the search space grows exponentially:

| Generators | Time steps | Binary variables | Combinations |
|------------|-----------|-----------------|--------------|
| 10         | 1         | 10              | 1,024        |
| 20         | 1         | 20              | ~1 million   |
| 50         | 24        | 1,200           | ~10³⁶¹       |
| 100        | 24        | 2,400           | astronomical |

Classical solvers (branch-and-bound, Lagrangian relaxation) handle medium instances well. But with renewables adding uncertainty, tighter constraints, and faster re-optimization cycles, the problem keeps growing.

QAOA encodes generator on/off decisions as qubits. The cost function becomes the problem Hamiltonian. The algorithm explores combinations through superposition and uses interference to favor low-cost solutions.

The potential advantage: classical solvers like branch-and-bound still search through exponential space — they're just smart about pruning. QAOA and VQE can sample high-quality solutions in polynomial circuit depth by exploiting quantum interference, meaning they could find near-optimal schedules faster as grid size grows. For a 100-generator, 24-hour problem with 2,400 binary variables, classical MIP solvers already struggle to close the optimality gap within real-time dispatch windows. A quantum solver that consistently finds 98% optimal solutions in seconds instead of minutes would be operationally valuable even without perfect answers.

That said, current quantum hardware is too small and noisy to compete on real grids. No one has demonstrated quantum advantage here yet. The point is building the formulation now so it's ready when hardware catches up.

---

## Why Qiskit?

[Qiskit](https://qiskit.org/) is IBM's open-source quantum computing SDK.

* `qiskit-optimization` handles QUBO formulation and solver management
* Same problem definition works with classical exact solvers, QAOA, and VQE
* Develop on simulators locally, run on IBM quantum hardware when ready
* Widely used in research and industry

---

## Project Pipeline

```
1. GRID MODEL           Network of generators, lines, and demand nodes
        ↓
2. COST MODEL           Fuel costs, startup costs, ramping penalties
        ↓
3. CONSTRAINTS          Capacity limits, demand balance, line flow limits
        ↓
4. CLASSICAL SOLVERS    Greedy dispatch, LP relaxation, MIP
        ↓
5. QUBO FORMULATION     Binary generator states → quadratic cost + penalty terms
        ↓
6. QISKIT SOLVERS       QAOA, VQE
        ↓
7. BENCHMARK            Compare cost, feasibility, runtime, scaling
```

---

## References

Tracked in [references/research-papers/README.md](references/research-papers/README.md)

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---
