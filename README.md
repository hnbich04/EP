# EnergyPATHWAYS Scenario Execution, Diagnostics, and Probabilistic Demand Analysis

## Overview

This notebook is currently under development to provide an integrated workflow for running **EnergyPATHWAYS (EP)**
electricity demand scenarios, inspecting deterministic outputs, and applying
probabilistic demand analysis.

It supports:

- Scenario execution
- Output validation and diagnostics
- Probabilistic demand shape generation
- AEMO-consistent POE maximum demand estimation
- Exploratory demand-structure analysis


---

## Directory Assumptions

The notebook assumes a standard EP layout:


EnergyPATHWAYS/
├─ ep_runs/my_scenario/reference/demand_outputs/
│ ├─ d_energy.csv.gz
│ └─ subsector_electricity_profiles.csv.gz
├─ ep_db/ShapeData/
│ ├─ *.csv
│ ├─ poe_shapes/
│ └─ poe_maxima/

Paths are currently hard-coded for a local EP development environment.

---

## Cell-by-Cell Summary

### Cell 1 — Scenario Execution
Runs multiple EP scenarios from Python, replicating `start_runs.sh`.
Scenarios share a single shape engine run for efficiency and reproducibility.

### Cell 2 — Annual Electricity Demand
Aggregates final-energy outputs to total annual electricity demand and plots time
series.

### Cell 3 — Hourly Subsector Profiles
Plots full-year hourly electricity profiles for selected subsectors, years, and
regions.

### Cell 4 — Single-Day Hourly Diagnostics
Plots a single weather-day hourly profile for a modeled year.
Flags a suspected discrepancy between EP input and output shapes.

### Cell 5 — Subsector Demand Breakdown
Aggregates electricity demand by subsector and year to show structural composition.

### Cell 6 — Average Hourly Shapes by Subsector
Computes and plots mean intraday electricity profiles for each subsector.

### Cell 7 — Residential Shapes by GAU and Year
Overlays residential hourly shapes across years for each region.
Used for trend inspection; known data gaps are noted.

### Cell 8 — Input Shape Visual Audit
Automatically plots all EP input shape files, adapting to hourly, EV, or monthly
formats.

### Cell 9 — Annual Demand by Region
Aggregates and plots annual regional electricity demand (converted to GWh).
Forms the basis for comparison with AEMO projections.

### Cell 10 — Hourly POE Shape Generation
Generates probabilistic hourly demand envelopes (P10/P50/P90) via stochastic
weather simulation.
Percentiles are computed hour-by-hour, not over annual maxima.

### Cell 11 — Deterministic vs POE Shape Comparison
Smooths and overlays original shapes with POE envelopes to validate construction.

### Cell 12 — AEMO-Style POE Maximum Demand
Computes true POE maximum demand metrics by simulating many weather-years and
extracting one maximum per year.
This aligns exactly with AEMO’s POE definition.

### Cell 13 — Daily Shape Clustering
Applies K-means clustering to daily 24-hour input shapes to identify recurring
demand regimes and their seasonal behaviour.

### Cell 14 — Load Factor Analysis
Computes annual electricity load factors (average / peak) and plots trajectories
by region and scenario.

