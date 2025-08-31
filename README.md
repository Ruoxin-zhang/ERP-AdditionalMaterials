# Additional Materials for ERP Dissertation

**Title:** Mapping urban infrastructure access and exploring its relationship with deprivation using open data  
**Author:** Ruoxin Zhang  
**Programme:** MSc Data Science (Urban Analytics Pathway), University of Manchester  
**Submission Date:** 1 September 2025  

## 1. Purpose
These materials are provided to ensure **full reproducibility** of the dissertation.  

## 2. Repository Structure
```text
├── code/                      # Jupter book scripts for data processing and modelling
│   ├── Ghana/    
│   └── Uganda/           
│
├── outputs/                   # Selected analytical outputs (for verification)
│   ├── ghana_composite_index.csv
│   ├── uganda_composite_index.csv
│   ├── ghana_regression_results.txt
│   └── uganda_regression_results.txt
│
├── docs/
│   └── Technical_Appendix.pdf # Detailed step-by-step workflow
│
├── requirements.txt           # Python dependencies
└── README.md                  # This file
```

## 3. How to Reproduce
### 3.1 Environment Setup
Install Python (tested with **Python 3.10**) and required libraries:  
```bash
conda create -n urban python=3.10
conda activate urban
pip install -r requirements.txt
```

### 3.2 Data Preparation

Raw datasets are **not included** in this repository.
 They can be obtained from the following open sources (see `data_sources/` for detailed instructions):

- **OpenStreetMap (OSM):** POIs via Geofabrik 

  Ghana: https://download.geofabrik.de/africa/ghana.html

  Uganda: https://download.geofabrik.de/africa/uganda.html

- **GRDI:** [Global Relative Deprivation Index v1, NASA/CIESIN](https://doi.org/10.7927/3xxe-ap97?utm_source=chatgpt.com)

- **WorldPop:** Constrained individual countries 2020 UN adjusted (100m resolution)

  Ghana: https://hub.worldpop.org/geodata/summary?id=49691

  Uganda: https://hub.worldpop.org/geodata/summary?id=49721

  used for population weighting of infrastructure accessibility

- **GADM:** Administrative boundaries (Level-2)

  Ghana: https://gadm.org/download_country.html#google_vignette

  Uganda: https://gadm.org/download_country.html#google_vignette

**Preprocessing:**

- Select specific infrastructure POIs:
  - Education
  - Health Care
  - Commerce
  - Green Space
  - Public Transport

- Vector Geometry → Point on Surface

- Vector general → Delete Duplicate Geometries

- OSM POIs were cleaned and reprojected in **QGIS** into projected CRS:

  - Ghana → EPSG:32630 (UTM Zone 30N)
  - Uganda → EPSG:32636 (UTM Zone 36N)

- Exported as `.gpkg` (e.g., `shop_reprojected.gpkg`) for use in Python.

### 3.3 Run the Analysis (The analysis is organised into Jupyter Notebooks)

1. **Preprocess data (read gpkg, compute accessibility indicators):**

   ```
   jupyter notebook Code/Ghana/Ghana_SingleIndex.ipynb
   jupyter notebook Code/Uganda/Uganda_SingleIndex.ipynb
   ```

2. **Construct composite index (PCA):**

   ```
   jupyter notebook Code/Ghana/Ghana_CompositeIndex.ipynb
   jupyter notebook Code/Uganda/Uganda_CompositeIndex.ipynb
   ```

3. **Run regression and spatial analysis (OLS/SEM):**

   ```
   jupyter notebook Code/Ghana/Ghana_RegressionandSpatialModelling.ipynb
   jupyter notebook Code/Uganda/Uganda_RegressionandSpatialModelling.ipynb
   ```

------

## 4. Verification

The `outputs/` folder contains selected analytical results corresponding to the dissertation:

- Composite index for Ghana and Uganda
- Regression outputs (OLS/SEM)

These can be compared against newly generated results to verify reproducibility.
 Minor discrepancies may occur if data are re-downloaded, due to OSM/WorldPop updates or stochastic variation in PCA.

------

## 5. Notes

- **Data Availability:** Only metadata and sample files are provided. Full datasets must be re-downloaded from the original sources.
- **Dependencies:** Install dependencies using pip install -r requirements.txt. Versions reflect those used during the dissertation; later versions may also work but could produce minor differences.
- **Disclaimer:** Results are reproducible using open data; however, small variations may occur if analyses are re-run at a later date due to updated OSM/WorldPop datasets.
- **Contact:** *ruoxin.zhang@student.manchester.ac.uk*
