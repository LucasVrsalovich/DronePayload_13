# Drone Arm Payload Structure Design and Analysis

## Objective

This project evaluates drone arm designs to determine maximum payload capacity while ensuring structural integrity under operational loads. We analyze two primary arm geometries across six material choices (carbon fiber composite, aluminum alloy, fiberglass, PLA, ABS, and wood) for a total of 12 design combinations.

Using MATLAB, we perform:

- Thrust-to-Weight Analysis: Calculating maximum payload capacity for each combination.
- Finite Element Analysis (FEA): Modeling displacement, von Mises stress, and safety factors under load.

Based on these results, we will determine a final recommended design and material combination that satisfies both the minimum payload requirement (0.5 kg) and the structural safety margin (factor of safety of 1.5-2+).

## Project Files

- `DroneDesign_StudentProjectTemplate.mlx` – Main Live Script (handles the math, FEA pipeline, and final design pick).
- `DroneDesign_StudentProjectTemplate.pdf` – Exported PDF if you just want to view results without opening MATLAB.
- `droneArmMaterials.mat` – Material constants (density, Modulus, Poisson's ratio, yield strength, cost) for all 6 materials.
- `DRONE_ARM.STL` & `DRONE_ARM2_SLDPRT.STL` – CAD files for Arm Design 1 and Design 2.

## Requirements

You'll need **MATLAB (R2021a or newer)** and the **Partial Differential Equation Toolbox**. 

## How to Run It

1. Download/clone everything into a single folder so file paths don't break.
2. Open `DroneDesign_StudentProjectTemplate.mlx`.
3. Run the script sections top-to-bottom:
   - **Task 1 (Setup):** Loads material properties and geometry defaults. Run this first or the variables won't be in your workspace.
   - **Task 3 (Thrust-to-Weight):** Calculates payload capacity across the 12 combinations and builds the comparison bar chart + `resultsT3` table.
   - **Task 4 (FEA):** Pulls in the CAD geometries, sets up boundary conditions, and solves for stress/displacement. Generates the `resultsT4` table along with stress plots.

*Note:* Task 4 generates individual plots for every scenario, so don't be surprised when a ton of figure windows pop open. Local helper functions are tucked at the bottom of the script.

## Setup Notes

- **Boundary Conditions:** The script uses `identifyBaseTipFaces` to auto-detect base and tip faces from geometry rather than hardcoded IDs, so FEA loads apply cleanly across different MATLAB versions.
- **CAD Scale:** STL files assume millimeter exports (`cadUnitScale = 1e-3`). If your CAD geometry was saved in meters or inches, change `cadUnitScale` in Task 1.
