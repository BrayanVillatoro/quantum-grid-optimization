# Quantum Sensor Network Optimization

A simulation framework for placing sensors and planning search actions in noisy environments, comparing classical baselines against Qiskit-based quantum optimization.

---

## Overview

Many real-world systems rely on detecting weak signals in noisy, uncertain environments. Examples include:

* underwater sensing and sonar
* autonomous drone search and exploration
* environmental and climate monitoring
* distributed robotics systems

Despite differences in hardware, these problems share a common structure:

* limited sensing resources
* uncertain environments
* noisy measurements
* the need to make optimal decisions

This project explores how to **optimally place sensors and plan sensing strategies** to maximize detection or information gain, while comparing:

* classical optimization methods
* quantum optimization approaches using Qiskit

---

## Problem Statement

Given:

* a spatial environment (initially a 2D grid)
* a limited number of sensors
* noisy and uncertain measurements
* an unknown or probabilistic source

Determine:

* where to place sensors
* how to allocate sensing resources

Such that:

> detection probability or information gain is maximized under uncertainty.

---

## Goals

* Build a clean simulation framework for noisy sensing environments
* Implement classical baselines for sensor placement
* Formulate the problem as a binary optimization problem (QUBO/Ising-style)
* Explore Qiskit-based approaches for solving the optimization
* Compare classical and quantum methods in terms of:

  * solution quality
  * scalability
  * robustness to noise

---

## Why Quantum?

Sensor placement and coordination problems often reduce to combinatorial optimization, which becomes intractable at scale.

This project investigates whether quantum approaches particularly those available through Qiskit—can provide advantages in:

* solving structured optimization problems
* exploring large solution spaces
* improving solution quality under constraints

---

## References

External research papers used by this project are tracked in:

* [references/research-papers/README.md](references/research-papers/README.md)

---

## License

This project is released under the MIT License. See the `LICENSE` file for details.

---
