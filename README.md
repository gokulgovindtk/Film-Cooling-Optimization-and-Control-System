# Turbine Blade Thermal Management & Control

This project presents a multi-disciplinary engineering workflow that couples Computational Fluid Dynamics (CFD), Finite Element Analysis (FEA), and System Controls to optimize turbine blade film cooling[cite: 1].

## Pipeline Architecture
The project follows a "Physics-to-Controls" methodology[cite: 1]:
* **CFD (ANSYS Fluent)**: Captures steady-state wall heat flux and temperature maps[cite: 1].
* **FEA (ANSYS Mechanical)**: Maps thermal loads to compute stress fields and safety factors[cite: 1].
* **Analysis (MATLAB)**: Processes simulation data, fits polynomial response surfaces, and validates results against established literature (e.g., Baldauf et al.)[cite: 1].
* **Control (Simulink)**: Implements a PID controller that regulates coolant mass flow in real-time to maintain blade integrity during thermal disturbances[cite: 1].

## Repository Contents
* `/CFD`: Fluent project files, mesh statistics, and boundary condition setup[cite: 1].
* `/FEA`: Mechanical structural analysis files and material property definitions[cite: 1].
* `/MATLAB`: Scripts for importing data, calculating adiabatic effectiveness ($\eta$), and generating response surfaces[cite: 1].
* `/Simulink`: Models for the thermal plant and the PID controller logic[cite: 1].

## Technical Highlights
* **Turbulence Modeling**: Utilized the $k-\omega$ SST model, as it is superior for predicting flow separation at coolant hole locations compared to standard $k-\epsilon$ models[cite: 1].
* **System Controls**: Designed a PID controller featuring anti-windup logic to account for physical constraints in coolant flow saturation[cite: 1].
* **Mesh Integrity**: Performed a rigorous Mesh Independence Study using Richardson Extrapolation to achieve a Grid Convergence Index (GCI) of less than 3%[cite: 1].

## Project Status Checklist
- [ ] Fluent CFD convergence (residuals $< 10^{-4}$)[cite: 1]

---
*This project was developed to demonstrate end-to-end integration of ANSYS, MATLAB, and Simulink workflows[cite: 1].*
