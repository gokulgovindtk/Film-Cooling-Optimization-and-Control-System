## Phase 1: ANSYS Fluent CFD Analysis
This phase focuses on modeling the film cooling effectiveness of a 2D turbine blade cross-section. The objective is to produce a physically meaningful wall heat flux map while adhering to the 512,000-cell limitation of the ANSYS Student version.

### Problem Statement
* **Geometry**: 2D NACA 4412 profile with a single coolant hole (injection angle: 30°, diameter: 0.5D).
* **Turbulence Modeling**: $k-\omega$ SST model employed to accurately capture boundary layer separation and jet-in-crossflow interactions at the coolant hole trailing edge.
* **Constraint**: Maintain mesh count between 280k–420k cells to ensure quality without exceeding student license limits.

### Boundary Conditions
| Boundary | Type | Value / Condition | Rationale |
| :--- | :--- | :--- | :--- |
| **Main Inlet** | Velocity Inlet | 150 m/s, 1600 K | Simulated turbine gas conditions |
| **Coolant Inlet** | Velocity Inlet | 2 m/s, 700 K | Sets blowing ratio ($M$) to 0.2 |
| **Outlet** | Pressure Outlet | 0 Pa (gauge) | Exit to atmosphere |
| **Blade Wall** | Wall | No-slip, 1100 K | Fixed temperature thermal load |

### Key Metrics
* **Adiabatic Effectiveness ($\eta$)**: $\eta = \frac{T_\infty - T_{aw}}{T_\infty - T_c}$.
* **Convergence Criteria**: Continuity residuals $< 10^{-4}$ and Energy residuals $< 10^{-7}$.
