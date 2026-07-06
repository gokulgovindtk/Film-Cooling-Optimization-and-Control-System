# Film-Cooled Turbine Blade — CFD → FEA → Digital Twin Controller

End-to-end engineering project that couples **ANSYS Fluent (CFD)** and **ANSYS Mechanical (FEA)** with **MATLAB** post-processing, closing the loop with a **Simulink** real-time PID controller for coolant flow.

> **Status:** Phases 1–3 complete (CFD → FEA → MATLAB analysis). Phase 4 (Simulink closed-loop controller) in progress.

---

## Project Pipeline

```
ANSYS Fluent (CFD)  →  ANSYS Mechanical (FEA)  →  MATLAB (Post-Processing)  →  Simulink (PID Control)
   wall heat flux         thermal stress            response surface fit         real-time controller
```

The project simulates a film-cooled turbine blade: Fluent computes the wall heat flux map, Mechanical maps that as a thermal load to get the stress field, MATLAB fits response surfaces across blowing-ratio sweeps, and Simulink will use the fitted model to run a real-time coolant-flow controller that keeps blade temperature under its safety limit.

---

## Repository Structure

```
├── ansys/
│   ├── fluent/              # Fluent case/geometry files, boundary conditions
│   └── mechanical/          # Static structural setup, material data (IN718)
├── data/
│   ├── fluent_wall_data.csv
│   ├── mechanical_stress.csv
│   ├── M05_wall.csv ... M20_wall.csv        # blowing ratio sweep (CFD)
│   └── M05_stress.csv ... M20_stress.csv    # blowing ratio sweep (FEA)
├── matlab/
│   ├── film_cooling_analysis.m   # Script 1: import + effectiveness plot
│   ├── parametric_sweep.m        # Script 2: response surface + optimal M*
│   ├── baldauf_correlation.m     # Script 3: literature validation
│   └── response_surface.mat      # saved fit, feeds into Simulink
├── simulink/                     # (in progress) plant model + PID controller
├── figures/                      # exported .png plots for the report
└── README.md
```

---

## Phase Summary

| Phase | Tool | Output | Status |
|---|---|---|---|
| 1 | ANSYS Fluent | Wall heat flux + adiabatic effectiveness map | ✅ Done |
| 2 | ANSYS Mechanical | Thermal-structural stress field (one-way FSI) | ✅ Done |
| 3 | MATLAB | Response-surface fit, optimal blowing ratio M*, validation vs Baldauf et al. (2002) | ✅ Done |
| 4 | Simulink | Real-time PID controller for coolant flow | 🔧 In progress |

### Key results so far
- Film cooling effectiveness (η) computed across a blowing-ratio sweep (M = 0.5–2.0)
- Polynomial response surfaces fit for η and max von Mises stress vs. M
- Optimal blowing ratio `M*` identified (max η subject to stress staying below yield)
- CFD results validated against the Baldauf et al. (2002) correlation (L2 relative error reported in console output)

---

## Requirements

- ANSYS Student (Fluent + Mechanical), 2024 release or later
- MATLAB R2024a (Curve Fitting Toolbox)
- Simulink (for Phase 4, once added)

---

## How to Reproduce

1. Open `ansys/fluent/` case, run the CFD solve, export wall data as `fluent_wall_data.csv`
2. Link Fluent solution into `ansys/mechanical/` Static Structural, solve, export `mechanical_stress.csv`
3. Run the MATLAB scripts in order:
   ```matlab
   film_cooling_analysis   % effectiveness plot from single-run data
   parametric_sweep        % sweep M = 0.5–2.0, fit response surfaces
   baldauf_correlation     % validate against published correlation
   ```
4. (Coming soon) Load `response_surface.mat` into the Simulink model in `simulink/` to run the closed-loop controller

---

## Notes

- Full two-way FSI (Fluent ↔ Mechanical) requires an HPC license; this project uses one-way thermal coupling (heat flux → thermal load), which is standard practice for this type of analysis.
- Mesh is kept under ANSYS Student's 512k cell cap (~280k–420k cells) with inflation layers near the blade wall.

## Roadmap

- [ ] Build Simulink plant model (MATLAB Function block + transfer function for thermal lag + transport delay)
- [ ] Tune PID controller for coolant mass flow rate
- [ ] Test disturbance rejection (hot-gas inlet temperature step changes)
- [ ] Finalize report figures and write-up.
