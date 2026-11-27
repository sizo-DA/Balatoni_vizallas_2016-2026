# Lake Balaton Water Level Data Analysis (2016–2026)

## Project overview

This repository documents an end-to-end exploratory data analysis (EDA) workflow using surface water-level measurements from the Siófok monitoring station (station ID: 2888) on Lake Balaton, Hungary. The dataset covers **30 September 2016 to 30 September 2026**.

The project demonstrates the full analytical workflow: source-data inspection, data-quality assessment, data migration, reconsideration of the original analytical scope, exploratory analysis, and preparation of analysis-ready datasets.

## Data source and scope

The source data were obtained as CSV files from the Hungarian Water Management Data Portal ([data.vizugy.hu](https://data.vizugy.hu)). The original files contain water-level measurements and, where available, water temperature measured near the water surface.

The primary variable in the final analysis is **surface water level (cm)**. Water temperature was part of the initial plan, but its coverage proved too sparse for a meaningful analysis over the full period. The project therefore retains all records with a valid timestamp and numeric water-level value, regardless of whether a water-temperature value is available.

The first and last calendar years are incomplete: the data begin on 30 September 2016 and end on 30 September 2026. Annual comparisons must treat these two years separately from complete calendar years.

## Analytical workflow

The work is organized into six sequential Jupyter notebooks:

1. **Data source inspection** – examines source files, file sizes, encodings, delimiters, column structures, and missing values without modifying the raw data.
2. **Initial data migration** – creates an initial combined dataset requiring valid timestamp, water level, and water temperature.
3. **Project reassessment** – evaluates the coverage of water-temperature observations and documents the decision to focus the main analysis on water level.
4. **Water-level data migration** – rebuilds the dataset using valid timestamps and numeric water-level measurements, independently of water-temperature availability.
5. **Exploratory data analysis (EDA)** – examines data quality, temporal coverage, measurement frequency, time-series behaviour, annual/monthly/seasonal statistics, extremes, and short-term changes.
6. **EDA results and analytical datasets** – consolidates key checks, investigates duplicate timestamps, and creates measurement-level and daily analysis datasets.

The notebooks should be run in numerical order. Notebook 03 uses outputs from notebook 02; notebook 05 uses the migrated dataset from notebook 04; notebook 06 uses the data and reports produced in the preceding analysis steps.

## Key findings

- The final migrated water-level dataset contains **221,802 records**.
- The observed water levels range from **27 cm to 154 cm**; the overall mean is **100.32 cm** and the median is **103 cm**.
- The source-data quality summary reported 2,395 records with water-temperature values out of 221,805 water-level records (approximately **1.08%**). This limited coverage was insufficient for the planned joint analysis. The 221,805 figure belongs to the preliminary source-quality summary; the final migrated water-level dataset contains 221,802 records.
- Measurement frequency changed substantially around 2022. The median interval between measurements was 30 minutes in 2016–2021 and 15 minutes from 2022 onward. The median number of daily records increased from approximately 26–29 to 96.
- In complete years from 2022 to 2025, between 95.62% and 97.53% of days contain exactly 96 measurements.
- April has the highest overall monthly mean water level (112.55 cm), while September has the lowest (80.45 cm). The seasonal means are descriptive summaries and do not, by themselves, establish statistically significant seasonality.

## Data products

The project produces two principal analysis datasets:

- **Measurement-level dataset** – preserves individual observations and detailed temporal information, including duplicate-timestamp indicators.
- **Daily dataset** – provides daily mean, median, minimum, maximum, range, measurement count, and the number of records belonging to duplicate timestamps.

Supporting CSV reports and figures are stored in the `reports/` directory. The detailed Hungarian documentation in `docs/hu/` describes the notebooks, generated files, methods, findings, and possible follow-up work.

## Repository structure

```text
Balatoni_vizallas_2016-2026/
├── README.md
├── Raw_data_2016-2026/          # Original, unchanged source CSV files
├── data/
│   ├── interim/                 # Intermediate migration outputs
│   └── processed/               # Validated and analysis-ready datasets
├── notebooks/                   # Six sequential Jupyter notebooks
├── reports/
│   └── figures/                 # Tables and generated figures
└── docs/
    └── hu/                      # Detailed Hungarian project documentation
```

## Data handling principles

- Original source CSV files are preserved unchanged.
- Source filename and original row number are retained during migration.
- Individual measurements are not aggregated during the migration stage.
- Duplicate timestamps are investigated rather than automatically removed.
- Extreme values are flagged for review, not automatically classified as errors or deleted.
- Partial calendar years are distinguished from complete years.
- File size and annual record count alone are not treated as evidence of a change in measurement frequency; timestamp intervals and daily record counts are examined.

## Limitations

This is a descriptive and exploratory analysis of measurements from a single monitoring station. It does not explain the causes of water-level changes, estimate changes in the lake's water volume, quantify evaporation, or build a forecasting model. External explanatory variables—such as precipitation, wind, air temperature, atmospheric pressure, or water-management operations—are outside the scope of this project.

Water-level changes alone cannot be interpreted as evaporation or as direct changes in the lake's water volume. Duplicate timestamps and unusual observations require contextual review before any decision to exclude or correct them.

## Possible next steps

Potential follow-up work, treated as separate projects, includes:

- detailed analysis of long-term trends and seasonal components using a consistent time resolution;
- integration of meteorological and water-management data, including precipitation, wind, air temperature, atmospheric pressure, and Sió sluice operations;
- analysis of relationships and possible time lags between water level and external variables;
- development and evaluation of forecasting models only after the temporal structure, measurement-frequency change, and relevant explanatory variables have been assessed.

## Documentation language

The repository's main `README.md` is in English. Detailed project documentation is available in Hungarian under `docs/hu/`.
