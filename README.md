# Drone Arm Payload Structure Design and Analysis

## Objective

This project optimizes quadcopter drone arm design, evaluating geometry and material selection to maximize payload capacity while ensuring structural integrity under motor-induced loads. Two structurally distinct arm designs are evaluated across six candidate materials (carbon fiber composite, aluminum alloy, fiberglass composite, PLA plastic, ABS plastic, and wood), using MATLAB to perform:

- A thrust-to-weight analysis to estimate maximum payload capacity for each design/material combination
- Finite element analysis (FEA) to evaluate structural safety (displacement, stress, and factor of safety) under applied thrust and motor weight loads

Based on these results, a final recommended design and material combination is selected that satisfies both the minimum payload requirement (0.5 kg) and the structural safety margin (factor of safety of 1.5-2+).

## Project Files

- `DroneDesign_StudentProjectTemplate.mlx` - Main MATLAB Live Script containing the full project: problem breakdown, design proposals, thrust-to-weight analysis (Task 3), finite element analysis (Task 4), and final design recommendation
- `DroneDesign_StudentProjectTemplate.pdf` - PDF export of the completed Live Script, for reviewers who do not have MATLAB installed
- `droneArmMaterials.mat` - Material property data (density, Young's modulus, Poisson's ratio, yield strength, cost per meter) for the six candidate materials
- `DRONE_ARM.STL` - CAD geometry for Design 1
- `DRONE_ARM2_SLDPRT.STL` - CAD geometry for Design 2

## Required Toolboxes and Dependencies

- MATLAB (R2021a or later recommended)
- **Partial Differential Equation Toolbox** - required for all Task 4 finite element analysis functions (`createpde`, `importGeometry`, `structuralBC`, `structuralBoundaryLoad`, `generateMesh`, `solve`, `pdeplot3D`, etc.)
- No additional third-party packages are required; all analysis uses built-in MATLAB and toolbox functions

To check whether the required toolbox is installed, run the following in MATLAB:

```matlab
ver
```

and confirm that "Partial Differential Equation Toolbox" appears in the list. If it is missing, install it via **Home > Add-Ons > Get Add-Ons** and search for "Partial Differential Equation Toolbox."

## How to Run the Code

1. Clone or download this repository, and make sure all files (the `.mlx` script, the `.mat` material file, and both `.stl` CAD files) are in the same folder, or update the file paths inside the script to point to their actual location.
2. Open `DroneDesign_StudentProjectTemplate.mlx` in MATLAB.
3. Run the sections in order from top to bottom:
   - **Task 1 (Setup):** loads material properties and defines drone/arm design parameters
   - **Task 3 (Thrust-to-Weight Analysis):** computes maximum payload capacity for all 12 design/material combinations and generates a summary table and bar chart
   - **Task 4 (Finite Element Analysis):** imports the CAD geometry for each design, applies boundary conditions and loads, runs the structural solver, and generates results tables and displacement/stress plots for all 12 combinations
4. Local helper functions (`computeArmVolume`, `thrustToWeightAnalysis`, `runFEA`, `identifyBaseTipFaces`) are defined at the end of the Live Script, after the last code section, as required by MATLAB for local functions inside a Live Script.

Each section can be re-run independently after Task 1 has been run once, since later sections depend on variables defined in Task 1 (`materials`, `designs`, `baseMass`, etc.).

## How to Reproduce the Results

1. Run Task 1 to load the exact material properties and geometry parameters used in this analysis (arm dimensions are hardcoded in Task 1 based on the actual CAD files provided).
2. Run Task 3. This will regenerate `resultsT3`, a 12-row table of arm mass, drone mass, and maximum payload capacity for every design/material combination, along with a grouped bar chart comparing payload capacity across materials and designs.
3. Run Task 4. This will regenerate `resultsT4`, a 12-row table of maximum displacement, maximum von Mises stress, and factor of safety for every combination, along with geometry and stress/displacement visualization figures for each combination.
4. Compare the printed/table output to the results discussed in the Interpretation of Results section of the Live Script. Note that FEA figures are generated fresh each run and may open as a large number of separate MATLAB figure windows (one geometry plot plus one 4-panel results plot per design/material combination).

### Notes on Reproducibility

- The base and tip mounting faces for the FEA boundary conditions are identified automatically (see `identifyBaseTipFaces`), based on geometry rather than hardcoded face IDs, so results should reproduce consistently across MATLAB sessions and versions without manual adjustment.
- CAD geometry is assumed to be exported in millimeters (standard SolidWorks STL export); the code automatically converts to meters via a `cadUnitScale` factor. If a different CAD export unit is used, update `cadUnitScale` in the relevant design struct in Task 1.
