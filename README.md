    
Film-Cooled Turbine Blade — CFD to FEA to Digital Twin Controller

End-to-end engineering project that couples ANSYS Fluent (CFD)[span_0](start_span)[span_0](end_span) and ANSYS Mechanical (FEA)[span_1](start_span)[span_1](end_span) with MATLAB post-processing[span_2](start_span)[span_2](end_span), closing the loop with a Simulink real-time PID controller for coolant flow[span_3](start_span)[span_3](end_span).

Status: Phases 1 and 2 are complete (CFD and FEA solved)[span_4](start_span)[span_4](end_span)[span_5](start_span)[span_5](end_span). Phase 3 (MATLAB response surfaces) and Phase 4 (Simulink closed-loop controller) are currently in active development[span_6](start_span)[span_6](end_span).

Project Pipeline
ANSYS Fluent (CFD)  ->  ANSYS Mechanical (FEA)  ->  MATLAB (Post-Processing)  ->  Simulink (PID Control)
   wall heat flux         thermal stress            response surface fit         real-time controller

The project simulates a film-cooled turbine blade[span_7](start_span)[span_7](end_span). Fluent computes the wall heat flux map[span_8](start_span)[span_8](end_span), Mechanical maps that data as a thermal load to evaluate the stress field[span_9](start_span)[span_9](end_span), MATLAB fits response surfaces across parametric blowing-ratio sweeps[span_10](start_span)[span_10](end_span), and Simulink utilizes the fitted model to execute a real-time coolant-flow controller that maintains localized temperatures below safety thresholds[span_11](start_span)[span_11](end_span).

Repository Structure
├── ansys/
│   ├── fluent/              # Fluent case, geometry files, and boundary conditions[span_12](start_span)[span_12](end_span)
│   └── mechanical/          # Static structural setup and material data (IN718)[span_13](start_span)[span_13](end_span)
├── data/                    # Data generation pipeline in progress
│   ├── fluent_wall_data.csv
│   └── mechanical_stress.csv
├── matlab/                  # Scripts to post-process FEA datasets (in development)
│   ├── film_cooling_analysis.m   # Script 1: data import and effectiveness plotting[span_14](start_span)[span_14](end_span)
│   ├── parametric_sweep.m        # Script 2: response surface and optimal M* determination[span_15](start_span)[span_15](end_span)
│   └── baldauf_correlation.m     # Script 3: literature validation[span_16](start_span)[span_16](end_span)
├── simulink/                # Plant model and PID architecture (in development)[span_17](start_span)[span_17](end_span)
├── figures/                 # Exported contour plots and solver convergence history[span_18](start_span)[span_18](end_span)[span_19](start_span)[span_19](end_span)
└── README.md

Phase Summary
Phase 1: ANSYS Fluent
* Output: Wall heat flux and adiabatic effectiveness maps[span_20](start_span)[span_20](end_span)
* Status: Complete[span_21](start_span)[span_21](end_span)

Phase 2: ANSYS Mechanical
* Output: Thermal-structural stress field via one-way fluid-structure interaction (FSI)[span_22](start_span)[span_22](end_span)
* Status: Complete[span_23](start_span)[span_23](end_span)

Phase 3: MATLAB
* Output: Response-surface fit, optimal blowing ratio M*, and validation against Baldauf et al. (2002)[span_24](start_span)[span_24](end_span)
* Status: In progress (Scripts developed)

Phase 4: Simulink
* Output: Real-time PID controller for coolant flow[span_25](start_span)[span_25](end_span)
* Status: In progress (Active testing)

Key Results So Far
* Structured a 2D Fluent mesh honoring cell constraints (~280k to 420k cells) utilizing local inflation layers near the blade wall[span_26](start_span)[span_26](end_span)[span_27](start_span)[span_27](end_span).
* Linked the Fluent fluid domain solution directly into the ANSYS Mechanical Static Structural environment[span_28](start_span)[span_28](end_span).
* Resolved coupled thermal-structural matrix equations to map von Mises stress distributions and structural safety factors[span_29](start_span)[span_29](end_span).
* Developed core MATLAB mathematical scripts to process text data, calculate spanwise-averaged adiabatic effectiveness, and model polynomial response surfaces[span_30](start_span)[span_30](end_span).

Requirements
* ANSYS Student (Fluent + Mechanical), 2024 release or later[span_31](start_span)[span_31](end_span)[span_32](start_span)[span_32](end_span)
* MATLAB R2024a (Control System Toolbox, Curve Fitting Toolbox)[span_33](start_span)[span_33](end_span)
* Simulink[span_34](start_span)[span_34](end_span)

How to Reproduce
1. Open the case file in ansys/fluent/, run the steady-state CFD solver, and export the resulting wall data[span_35](start_span)[span_35](end_span)[span_36](start_span)[span_36](end_span).
2. Open the Workbench project schematic to link the Fluent solution cell directly into the ansys/mechanical/ Static Structural setup, then solve for thermal stresses[span_37](start_span)[span_37](end_span).
3. Execute the MATLAB mathematical pipeline to import and structure the exported structural CSV data[span_38](start_span)[span_38](end_span).
4. Load the compiled response surfaces into the active Simulink workspace to interface with the control blocks[span_39](start_span)[span_39](end_span).

Technical Notes
* Full two-way FSI (Fluent to Mechanical and back) requires an HPC license. This repository implements a one-way thermal coupling framework (heat flux map applied as a thermal load)[span_40](start_span)[span_40](end_span), which represents standard industry practice for turbine component tracking.
* Mesh counts strictly adhere to the ANSYS Student 512k cell limit constraint[span_41](start_span)[span_41](end_span).

Roadmap
1. Complete structural data generation across the full parametric blowing ratio sweep (M = 0.5 to 2.0)[span_42](start_span)[span_42](end_span).
2. Validate and test MATLAB script execution directly against the generated structural datasets[span_43](start_span)[span_43](end_span).
3. Finalize Simulink closed-loop plant integration, incorporating transfer function modeling for material thermal lag and transport delays[span_44](start_span)[span_44](end_span).
4. Run disturbance step changes (hot-gas temperature fluctuations) to benchmark PID tracking and stability performance[span_45](start_span)[span_45](end_span).
