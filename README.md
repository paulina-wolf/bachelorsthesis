# Climate Change as a Conflict Catalyst

**Subnational Evidence on Environmental Shocks and Outbreaks of Violence**

Bachelor's thesis in Political Science, University of Mannheim (2025)
Author: Paulina Noée Wolf · Supervisor: Prof. Nan Zhang, Ph.D.

This repository contains the R code I wrote for my bachelor's thesis. The thesis examines whether climate shocks (temperature anomalies, precipitation anomalies and climate-related disasters) increase the probability of violent conflict in Africa. It also asks whether this effect depends on local conditions: agricultural dependence, the political exclusion of ethnic groups, and national climate vulnerability.

## Research design

- **Unit of analysis:** 1° × 1° grid cells across Africa, observed monthly from 1996 to 2010
- **Outcome:** whether a grid cell experienced at least one conflict fatality in a given month (UCDP GED)
- **Climate shocks:**
  - temperature and precipitation anomalies relative to a 1961–1990 baseline (CRU TS)
  - occurrence of climate-related disasters (EM-DAT)
- **Moderators:**
  - an agricultural season intensity index built from MODIS data (growing season length, vegetation amplitude, double cropping seasons)
  - the presence of politically excluded ethnic groups (GeoEPR/EPR)
  - country-level climate vulnerability (ND-GAIN)
- **Controls:** conflict in the previous month and economic activity measured by nighttime lights
- **Models:** linear probability models with fixed effects, estimated with `fixest`:
  - Model 1: cell-month level with cell, year and month fixed effects
  - Model 2: with country and year fixed effects, interacting shocks with vulnerability

  Standard errors are clustered by grid cell. All models are also estimated with climate shocks lagged by 3, 6 and 12 months.

## Files

| File | Purpose |
|---|---|
| `Bachelore_Thesis_Data_set_code__Paulina_Wolf.Rmd` | Builds the grid-cell panel: loads, cleans and spatially merges all data sources, constructs anomalies, indices and controls, and checks intermediate results with maps. Output: `ClimateConflict_BAdata_PaulinaWolf.csv` |
| `Bachelor_Thesis_Analysis_Code__Paulina_Wolf.Rmd` | Estimates all regression models (with and without time lags), creates the regression tables and the predicted-probability plot for the precipitation × agricultural intensity interaction |

Run the data set code first, then the analysis code.

## Data sources

The raw data are **not included** in this repository. Some providers (in particular EM-DAT) do not permit redistribution, and several files are large. All data are available from the original providers:

- **CRU TS 4.07** – monthly temperature and precipitation (Climatic Research Unit, University of East Anglia)
- **EM-DAT** – international disaster database (CRED, UCLouvain); custom request from April 2025
- **UCDP GED** – georeferenced conflict events (Uppsala Conflict Data Program)
- **DMSP-OLS Nighttime Lights, version 4** – stable lights for 1995, 2000, 2005 and 2010
- **ND-GAIN** – country vulnerability index (Notre Dame Global Adaptation Initiative)
- **MODIS Land Cover and Land Cover Dynamics** – land cover type, green-up, dormancy, EVI amplitude, number of growing cycles
- **GPW v4** – UN-adjusted population density (2000, 2005, 2010)
- **GeoEPR / EPR 2021** – settlement areas and political status of ethnic groups
- **Natural Earth** – country boundaries (via `rnaturalearth`)

## Requirements

R with the following packages:

`tidyverse`, `fixest`, `modelsummary`, `marginaleffects`, `margins`, `interactions`, `patchwork`, `kableExtra`, `webshot2`, `raster`, `terra`, `sf`, `ncdf4`, `rnaturalearth`, `geosphere`, `countrycode`, `R.utils`, `readxl`, `janitor`, `devtools`

## Notes

- The code is shared as it was written for the thesis. Some file paths point to my local folders and need to be adjusted before running.
- Code that only needs to run once, such as unzipping the raw data, is commented out but kept for reproducibility.
