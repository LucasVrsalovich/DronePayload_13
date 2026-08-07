# Drone Arm Payload Structure Design and Analysis

## Objective

This project evaluates drone arm designs to determine maximum payload capacity while ensuring structural integrity under operational loads. We analyze two primary arm geometries across six material choices (carbon fiber composite, aluminum alloy, fiberglass, PLA, ABS, and wood) for a total of 12 design combinations.

Using MATLAB, we perform:

- Thrust-to-Weight Analysis: Calculating maximum payload capacity for each combination.
- Finite Element Analysis (FEA): Modeling displacement, von Mises stress, and safety factors under load.

Based on these results, we will determine a final recommended design and material combination that satisfies both the minimum payload requirement (0.5 kg) and the structural safety margin (factor of safety of 1.5-2+).

## Project Files

- `DroneDesign_StudentProjectTemplate.mlx` - Main MATLAB Live Script containing the analysis, FEA pipeline, and final recommendations.
- `DroneDesign_StudentProjectTemplate.pdf` - PDF export of the completed Live Script for quick viewing without MATLAB.
- `droneArmMaterials.mat` - Material properties (density, Young's modulus, Poisson's ratio, yield strength, cost/m) for all six candidate materials.
- `DRONE_ARM.STL` - CAD geometry for Design 1.
- `DRONE_ARM2_SLDPRT.STL` - CAD geometry for Design 2.

## Requirements

- MATLAB (R2021a or newer recommended)
- **Partial Differential Equation Toolbox** (required for Task 4 FEA functions)

To verify the toolbox is installed, run `ver` in the Command Window and check for *Partial Differential Equation Toolbox*. If it's missing, install it via **Home > Add-Ons > Get Add-Ons**.

## Running the Script & Reproducing Results

1. Clone or download this repository. Ensure all `.mlx`, `.mat`, and `.stl` files stay in the same working directory (or update file paths inside the script).
2. Open `DroneDesign_StudentProjectTemplate.mlx` in MATLAB.
3. Run the script sections sequentially:
   - **Task 1 (Setup):** Loads material properties and sets up the drone/arm parameters. (Must be run first to initialize workspace variables like `materials`, `designs`, and `baseMass`).
   - **Task 3 (Thrust-to-Weight Analysis):** Calculates maximum payload capacities across all 12 design/material combinations, outputting the `resultsT3` summary table and comparison bar chart.
   - **Task 4 (Finite Element Analysis):** Imports CAD geometry, applies boundary loads, and solves for structural performance. Generates the `resultsT4` table along with stress and displacement figures.

*Note:* Task 4 opens individual figure windows for each combination, so expect a few dozen plot windows to open while it solves. Helper functions (`computeArmVolume`, `runFEA`, etc.) are located at the bottom of the Live Script.

## Setup Details

- **Boundary Conditions:** Base and tip faces are detected automatically using geometry algorithms (`identifyBaseTipFaces`) rather than hardcoded face IDs, keeping FEA boundary conditions consistent across different MATLAB sessions.
- **CAD Scale:** STL files are assumed to be exported in millimeters (`cadUnitScale = 1e-3`). If your CAD files use a different unit, adjust `cadUnitScale` in the Task 1 design struct.
