Film-Cooled Turbine Blade — CFD → FEA → Digital Twin Controller
End-to-end engineering project that couples ANSYS Fluent (CFD)[span_0](start_span)[span_0](end_span) and ANSYS Mechanical (FEA)[span_1](start_span)[span_1](end_span) with MATLAB post-processing[span_2](start_span)[span_2](end_span), closing the loop with a Simulink real-time PID controller for coolant flow[span_3](start_span)[span_3](end_span).

Status: Phases 1–2 complete (CFD → FEA solved)[span_4](start_span)[span_4](end_span)[span_5](start_span)[span_5](end_span). Phase 3 (MATLAB response surfaces) and Phase 4 (Simulink closed-loop controller) are currently in active development[span_6](start_span)[span_6](end_span).

Project Pipeline
ANSYS Fluent (CFD)  →  ANSYS Mechanical (FEA)  →  MATLAB (Post-Processing)  →  Simulink (PID Control)
   wall heat flux         thermal stress            response surface fit         real-time controller
The project simulates a film-cooled turbine blade[span_7](start_span)[span_7](end_span): Fluent computes the wall heat flux map[span_8](start_span)[span_8](end_span), Mechanical maps that as a thermal load to get the stress field[span_9](start_span)[span_9](end_span), MATLAB fits response surfaces across blowing-ratio sweeps[span_10](start_span)[span_10](end_span), and Simulink uses the fitted model to run a real-time coolant-flow controller that keeps blade temperature under its safety limit[span_11](start_span)[span_11](end_span).

Repository Structure
├── ansys/
│   ├── fluent/              # Fluent case/geometry files, boundary conditions[span_12](start_span)[span_12](end_span)
│   └── mechanical/          # Static structural setup, material data (IN718)[span_13](start_span)[span_13](end_span)
├── data/                    # (Data generation pipeline in progress)
│   ├── fluent_wall_data.csv
│   └── mechanical_stress.csv
├── matlab/                  # (In development) Scripts to post-process FEA datasets
│   ├── film_cooling_analysis.m   # Script 1: import + effectiveness plot[span_14](start_span)[span_14](end_span)
│   ├── parametric_sweep.m        # Script 2: response surface + optimal M*[span_15](start_span)[span_15](end_span)
│   └── baldauf_correlation.m     # Script 3: literature validation[span_16](start_span)[span_16](end_span)
├── simulink/                # (In development) Plant model + PID architecture[span_17](start_span)[span_17](end_span)
├── figures/                 # Exported contour plots and solver convergence history[span_18](start_span)[span_18](end_span)[span_19](start_span)[span_19](end_span)
└── README.md

Phase Summary
Phase	Tool	Output	Status
1	ANSYS Fluent	Wall heat flux + adiabatic effectiveness map[span_20](start_span)[span_20](end_span)	✅ Done[span_21](start_span)[span_21](end_span)
2	ANSYS Mechanical	Thermal-structural stress field (one-way FSI)[span_22](start_span)[span_22](end_span)	✅ Done[span_23](start_span)[span_23](end_span)
3	MATLAB	Response-surface fit, optimal blowing ratio M*, validation vs Baldauf et al. (2002)[span_24](start_span)[span_24](end_span)	🔧 In progress (Scripts written)
4	Simulink	Real-time PID controller for coolant flow[span_25](start_span)[span_25](end_span)	🔧 In progress (Active testing)

Key results so far
* Completed 2D Fluent meshing and solution matching physical limits (~280k–420k cells with local inflation layers)[span_26](start_span)[span_26](end_span)[span_27](start_span)[span_27](end_span).
* Successfully linked the Fluent fluid domain solution directly into the ANSYS Mechanical Static Structural setup[span_28](start_span)[span_28](end_span).
* Resolved the coupled thermal-structural matrix equations to produce von Mises stress fields and safety factors[span_29](start_span)[span_29](end_span).
* Written core MATLAB mathematical scripts to compute spanwise-averaged adiabatic effectiveness and structure polynomial response fits[span_30](start_span)[span_30](end_span).

Requirements
* ANSYS Student (Fluent + Mechanical), 2024 release or later[span_31](start_span)[span_31](end_span)[span_32](start_span)[span_32](end_span)
* MATLAB R2024a (Control System Toolbox, Curve Fitting Toolbox)[span_33](start_span)[span_33](end_span)
* Simulink[span_34](start_span)[span_34](end_span)

How to Reproduce
1. Open `ansys/fluent/` case, run the steady-state CFD solve, and export wall data[span_35](start_span)[span_35](end_span)[span_36](start_span)[span_36](end_span).
2. Open the Workbench system to link the Fluent solution cell directly into `ansys/mechanical/` Static Structural[span_37](start_span)[span_37](end_span). Solve for thermal stresses[span_38](start_span)[span_38](end_span).
3. Run the developed MATLAB mathematical pipeline to import the structural data[span_39](start_span)[span_39](end_span).
4. Load the structured response surfaces into the active Simulink workspace to interface with the control blocks[span_40](start_span)[span_40](end_span).

Notes
* Full two-way FSI (Fluent ↔ Mechanical) requires an HPC license; this project maps a one-way thermal coupling framework (heat flux → thermal load)[span_41](start_span)[span_41](end_span), which is the industry standard for turbine component tracking.
* Mesh counts strictly adhere to the ANSYS Student 512k cell cap constraint[span_42](start_span)[span_42](end_span).

Roadmap
 Complete data generation across the full blowing ratio sweep (M = 0.5–2.0)[span_43](start_span)[span_43](end_span).
 Validate MATLAB code execution directly against generated structural CSV datasets[span_44](start_span)[span_44](end_span).
 Finalize Simulink closed-loop plant integration (Transfer function modeling for thermal lag + delay)[span_45](start_span)[span_45](end_span).
 Run disturbance step changes (hot-gas profile variations) to benchmark PID tracking performance[span_46](start_span)[span_46](end_span).
