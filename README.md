# Film-Cooled Turbine Blade: CFD to FEA to Digital Twin Controller

An end-to-end engineering pipeline that couples fluid dynamics and structural mechanics with post-processing routines, closing the loop with a real-time control system for optimized thermal management. This repository implements a physics-informed reduced-order model by mapping localized heat fluxes into structural stresses, providing the plant framework for an automated coolant-flow governor.

## Project Status

* **Phase 1 (Aerodynamic Simulation):** Complete. 2D fluid domain resolved using steady-state solvers.
* **Phase 2 (Structural Mapping):** Complete. One-way fluid-structure interaction matrix resolved for thermal stress.
* **Phase 3 (Mathematical Post-Processing):** In Progress. Core scripts developed for parametric response surfaces.
* **Phase 4 (Control Systems Integration):** In Progress. Active testing of closed-loop tracking architectures.

## Execution Pipeline

