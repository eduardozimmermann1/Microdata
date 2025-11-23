README — Fine-Grained Poverty and Insecurity Index (FIPI) for Guaramirim, Brazil

Author: Eduardo Dietrich Zimmermann
Last update: November 2025
Version: 1.0
License: CC-BY 4.0
Corresponding research: Small-Area Social Vulnerability in Low-Capacity Municipalities: A CadÚnico-Based Spatial Index for Guaramirim, Brazil (submitted)

🎯 Overview

This repository contains the fully reproducible Python pipeline developed for the construction, robustness evaluation, and spatial analysis of the Fine-Grained Poverty and Insecurity Index (FIPI) for the municipality of Guaramirim, Santa Catarina, Brazil.

All figures included as annexes in the accompanying paper are generated directly from this code.

The pipeline uses CadÚnico administrative microdata, neighborhood shapefiles, and public school administrative records, and produces:

Neighborhood-level FIPI scores

Uncertainty and sensitivity measures

Spatial autocorrelation diagnostics (Moran’s I, LISA)

External validation outputs (Bolsa Família coverage, school supply)

Choropleth maps and tables used in the article’s annexes

The code is written to be transparent, replicable, and runnable in any low-capacity municipal IT environment.

📂 Folder Structure
/
├── main.py                        # Full pipeline (ETL → FIPI → PCA → Spatial stats → Figures)
│
├── Datasets/
│   ├── Dados Cad 04-11-25.xlsx    # CadÚnico microdata (de-identified)
│   ├── ESCOLAS_GUARAMIRIM.xlsx    # Public schools per neighborhood
│   ├── GUARAMIRIM_SC - Bolsa...   # Bolsa Família & CadÚnico monitoring report (PDF)
│
├── Shapefiles/
│   ├── limitesGuaramirim.*        # Municipal boundary
│   ├── bairrosGuaramirim.*        # Neighborhood polygons (22)
│
├── Outputs/
│   ├── guaramirim_fipi_bairros.png
│   ├── guaramirim_fipi_table.png
│   ├── correlation_matrix.png
│   ├── lisa_moran_scatterplot.png
│   ├── lisa_clusters_map.png
│   ├── lisa_significant_map.png
│   ├── cadunico_guaramirim_agg_bairros_en.csv
│   ├── pbf_coverage_by_bairro.csv
│   ├── schools_coverage_by_bairro.csv
│   ├── agg_with_pca.csv
│   ├── fipi_sensitivity_analysis.csv
│   ├── uncertainty_measures.csv
│   ├── spatial_stats_summary.csv
│   ├── spatial_with_lisa.geojson
│
└── README.md                      # (this file)


Obs.: Folder names in your screenshot were mapped to this structure for publication quality. Keep exactly these names in the ZIP.

⚙️ How to Run
1. Requirements

Python ≥ 3.10

Required libraries (install via pip):

pip install pandas numpy geopandas scikit-learn libpysal matplotlib openpyxl

2. Run the pipeline

Inside the project folder:

python main.py


All outputs will be written to the Outputs/ folder.

🔍 What the Pipeline Does
1. Data Cleaning and Transformation

Standardizes CadÚnico variables (income, expenditures, sanitation)

Parses numeric fields with Brazilian locale conventions

Handles missing values and identifies outliers (|z| > 3)

2. Construction of Vulnerability Indicators

Extreme poverty (BRL 218 threshold)

Crowding (≥ 3 persons/bedroom)

Food expenditure burden (≥ 40%)

IVD composite (6 binary housing–sanitation deficits)

3. Index Aggregation and Standardization

Computes neighborhood-level proportions

Builds FIPI using standardized z-scores

Produces ranking table

4. Internal Consistency Checks

Correlation matrix

PCA loadings and explained variance

5. Uncertainty Estimation

Binomial-based standard errors

SE for composite index

6. Sensitivity Analysis

PCA-based variant

PCA-weighted variant

Double-weight IVD variant

Rank correlations

7. Spatial Statistics

Queen contiguity weights

Global Moran’s I

LISA quadrant map

Significance map (p < 0.05, permutation-based)

8. External Validation

FIPI × Bolsa Família coverage

FIPI × Schools per 1,000 families

Correlations and summary tables

9. Figure Generation

All maps & tables reproduced in the article’s annexes.

📜 Citation

If you use this repository or adapt the FIPI methodology, please cite:

Zimmermann, E.D. (2025).
Small-Area Social Vulnerability in Low-Capacity Municipalities:
A CadÚnico-Based Spatial Index for Guaramirim, Brazil.
Zenodo. https://doi.org/10.5281/zenodo.17682923


(Replace with your DOI after upload.)

📝 Notes for Reproducibility

All personally identifiable variables were removed or anonymized.

Geographic analysis excludes non-geocoded neighborhoods grouped as OUTROS.

Monetary values are expressed in BRL.

Because CadÚnico is a full administrative census of low-income households, all standard errors reflect finite-population variability, not sampling error.