# NOSTRUM 15 MW - 270 m RWT OpenFAST Model

OpenFAST input deck for the NOSTRUM 15 MW 270 m rotor wind turbine on UMaine VolturnUS-S semi-submersible platform.

In the context of the NOSTRUM project, this repository provides a floating offshore wind turbine (FOWT) model for aero-hydro-servo-elastic simulations using OpenFAST.

The model files in this repository are organized for OpenFAST v4.2.0 input format.

## Requirements

- OpenFAST v4.2.0 (or compatible recent v4.x build)
- ROSCO v2.9 controller library for ServoDyn Bladed interface (`libdiscon`/`DISCON.dll`)
- Wind inflow files included in `Wind/` and linked from `inflow_*.dat`
- Hydrodynamic potential-flow data in `HydroData-IEA15_repo/`

## Build / Installation

No compilation is required for this repository itself.

Install OpenFAST separately and ensure the `openfast` executable is available in your shell.

## Configuration

Test simulation cases are:

- `RUN_8mps.fst`
- `RUN_11mps.fst`
- `RUN_15mps.fst`

Each `.fst` case links to module files for:

- ElastoDyn: `NOSTRUM-15-270-RWT-UMaineSemi-Elastodyn.dat`
- AeroDyn: `NOSTRUM-15-270-RWT-UMaineSemi_AeroDyn15.dat`
- ServoDyn: `NOSTRUM-15-270-RWT-UMaineSemi_ServoDyn.dat`
- SeaState: `NOSTRUM-15-270-RWT-UMaineSemi_SeaState.dat`
- HydroDyn: `NOSTRUM-15-270-RWT-UMaineSemi_HydroDyn.dat`
- MoorDyn: `NOSTRUM-15-270-RWT-UMaineSemi_MoorDyn.dat`

Important:

- `NOSTRUM-15-270-RWT-UMaineSemi_ServoDyn.dat` points at a placeholder dylib file
- Update `DLL_File` to your local ROSCO/OpenFAST controller library path before running.

## Usage

Run a case directly with OpenFAST:

```bash
openfast RUN_8mps.fst
```

Other provided operating points:

## Code Structure

- `RUN_*.fst`  
  Main OpenFAST case files for different wind speeds.
- `NOSTRUM-15-270-RWT-UMaineSemi_*.dat`  
  Module-level input files (ElastoDyn, AeroDyn, ServoDyn, SeaState, HydroDyn, MoorDyn).
- `NOSTRUM-15-270-RWT_ElastoDyn_blade.dat`, `NOSTRUM-15-270-RWT-UMaineSemi_ElastoDyn_tower.dat`  
  Blade and tower structural properties.
- `NOSTRUM-15-270-Blade.dat`  
  AeroDyn blade geometry and sectional data.
- `Airfoils/`  
  Airfoil polars and coordinate files used by AeroDyn.
- `HydroData-IEA15_repo/`  
  WAMIT and related hydrodynamic data used by HydroDyn potential-flow model for the floating platform as used in the IEA 15-240-RWT (https://github.com/IEAWindSystems/IEA-15-240-RWT/tree/master).
- `Wind/` and `inflow_*.dat`  
  Wind input definitions and references.

## NOSTRUM Project summary

NOSTRUM is a 2-year research project aimed at optimizing floating offshore wind turbines (FOWTs) for the Mediterranean Sea. Through a combination of advanced numerical approaches, the project focuses on innovative design solutions for blades, towers and floating platforms, along with advanced control strategies tailored to Mediterranean conditions.

The aim is to provide the wind energy community with design guidelines and reference data, models and analyses to apply in the framework of modern floating wind turbines for offshore wind energy development and research in the Mediterranean Sea.

This collaborative effort between three research units from Sapienza University, Universita degli Studi di Firenze, and CNR-INM culminates in new reference wind turbine models, available as open-access resources for future research and feasibility studies.

Visit: https://nostrum-project.it

## References

[1] Cardamone, R., Broglia, R., Papi, F., Rispoli, F., Corsini, A., Bianchini, A., & Castorrini, A. (2025). Aerodynamic design of wind turbine blades using multi-fidelity analysis and surrogate models. International Journal of Turbomachinery, Propulsion and Power, 10(3), 16. https://doi.org/10.3390/ijtpp10030016

[2] Castorrini, A., Papi, F., Bianchini, A., Broglia, R., Rispoli, F., Ferrara, G., Lugni, C., & Cardamone, R. (2026). NOSTRUM - Optimizing Floating Offshore Wind Turbines For Use In The Mediterranean Sea - TECHNICAL REPORTS - Part 2. Zenodo. https://doi.org/10.5281/zenodo.18620593

## Acknowledgement

This research is supported by the Ministry of University and Research (MUR) as part of the European Union program NextGenerationEU, Missione 4 "Istruzione e Ricerca" del Piano Nazionale di Ripresa e Resilienza (PNRR), Componente C2 - Investimento 1.1, Fondo per il Programma Nazionale di Ricerca e Progetti di Rilevante Interesse Nazionale (PRIN).
