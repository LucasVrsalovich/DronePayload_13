# Drone Arm Payload Structure Design and Analysis

## Objective

This project evaluates drone arm designs to determine maximum payload capacity while ensuring structural integrity under operational loads. We analyze two primary arm geometries across six material choices (carbon fiber composite, aluminum alloy, fiberglass, PLA, ABS, and wood) for a total of 12 design combinations.

Using MATLAB, we perform:

- Thrust-to-Weight Analysis: Calculating maximum payload capacity for each combination.
- Finite Element Analysis (FEA): Modeling displacement, von Mises stress, and safety factors under load.

Based on these results, we will determine a final recommended design and material combination that satisfies both the minimum payload requirement (0.5 kg) and the structural safety margin (factor of safety of 1.5 to 2+).

## Project Files

- `DroneDesign_StudentProjectTemplate.mlx` – Main Live Script (handles the math, FEA pipeline, and final design pick).
- `DroneDesign_StudentProjectTemplate.pdf` – Exported PDF if you just want to view results without opening MATLAB.
- `droneArmMaterials.mat` – Material constants (density, Modulus, Poisson's ratio, yield strength, cost) for all 6 materials.
- `DRONE_ARM.STL` & `DRONE_ARM2_SLDPRT.STL` – CAD files for Arm Design 1 and Design 2.

## Requirements

**MATLAB (R2021a or newer)** and the **Partial Differential Equation Toolbox**. 

## Running the Script & Reproducing our Results

1. Copy or download this repository. Make sure all `.mlx`, `.mat`, and `.stl` files stay in the same folder. 
2. Open `DroneDesign_StudentProjectTemplate.mlx` in MATLAB.
3. Run the script sections sequentially:
   - **Task 1 (Setup):** will load material properties and set up the drone/arm parameters. (Must be run first to initialize variables like `materials`, `designs`, and `baseMass`.
   - **Task 3 (Thrust-to-Weight Analysis):** Calculates maximum payload capacities across all 12 design/material combinations, outputting the `resultsT3` summary table and comparison bar chart.
   - **Task 4 (Finite Element Analysis):** will import CAD geometry, apply boundary loads, and solve for structural performance. This will generate the `resultsT4` table along with stress and displacement figures.
 
*Note:* Task 4 opens individual figure windows for each combination, so expect a few dozen plot windows to open while it solves. Helper functions (`computeArmVolume`, `runFEA`, etc.) are located at the bottom of the Live Script.

## Setup Details

- **Boundary Conditions:** Base and tip faces are detected automatically using geometry algorithms (`identifyBaseTipFaces`) rather than hardcoded face IDs, keeping FEA boundary conditions consistent across different MATLAB sessions.
- **CAD Scale:** STL files are assumed to be exported in millimeters (`cadUnitScale = 1e-3`). If your CAD files use a different unit, adjust `cadUnitScale` in the Task 1 design struct.
