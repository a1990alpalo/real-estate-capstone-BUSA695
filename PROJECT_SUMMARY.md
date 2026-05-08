# Project Summary

## Project Purpose

This project is a BUSA 695 capstone focused on real estate price prediction. The goal is to clean and prepare housing data, build predictive models, compare model performance, and create visual outputs that help explain the results. The project also includes a map-based output to show how predicted prices and pricing errors can be viewed geographically.

## Full Project Workflow

The project starts with raw housing data and moves through several stages:

1. Load and clean the original realtor dataset
2. Save a cleaned master dataset
3. Create simplified and modeling-ready datasets
4. Build and compare predictive models
5. Save model files and performance results
6. Create model evaluation charts
7. Create an interactive housing map

## Dataset Flow

The project follows this main dataset flow:

`realtor-data.csv` -> `realtor_master.csv` -> `cleaned_simple.csv` / `realtor_modeling.csv`

- `realtor-data.csv`
  Raw source data
- `realtor_master.csv`
  Cleaned master dataset
- `cleaned_simple.csv`
  Simplified dataset without selected location columns
- `realtor_modeling.csv`
  Modeling-ready dataset used for downstream predictive work

## Purpose of Each Notebook

### 1. `project BUSA 695.ipynb`

**Purpose**

This notebook performs the first stage of data preparation. It loads the raw realtor dataset, explores the columns and missing values, fills or removes missing data where needed, encodes the `status` field, and saves the cleaned master dataset.

**Input files**

- `realtor-data.csv`

**Output files**

- `realtor_master.csv`

### 2. `cleaned_realtor_data.ipynb`

**Purpose**

This notebook further reviews the cleaned dataset, removes unrealistic values and outliers, and creates a simplified dataset for modeling workflows that do not need location variables. It also includes early exploratory plots and summary checks.

**Input files**

- `realtor_master.csv`

**Output files**

- `cleaned_simple.csv`

### 3. `realtor_modeling.ipynb`

**Purpose**

This notebook prepares a modeling-ready version of the housing data and tests multiple linear regression setups. It also saves the processed dataset used later by the random forest workflow.

**Input files**

- `realtor-data.csv`
- `realtor_master.csv`

**Output files**

- `realtor_modeling.csv`

### 4. `mapping.ipynb`

**Purpose**

This notebook supports the geographic part of the project. It trains a random forest model for mapping use, adds predicted prices and pricing errors to property records, geocodes zip codes into latitude and longitude, and creates an interactive map.

**Input files**

- `realtor_master.csv`
- `cleaned_simple.csv`

**Output files**

- `rf_model.pkl`
- `housing_map.html`

### 5. `realtor_random_forest.ipynb/random_forest_model.ipynb`

**Purpose**

This notebook develops and evaluates the main random forest model. It loads the prepared modeling dataset, samples data for training, saves the trained model, calculates evaluation metrics, compares the random forest model against a gradient boosting benchmark, and creates saved visualizations.

**Input files**

- `realtor_modeling.csv`

**Output files**

- `realtor_random_forest.ipynb/random_forest_model.pkl`
- `realtor_random_forest.ipynb/model_results.txt`
- PNG chart files in `realtor_random_forest.ipynb/visuals/`

## Final Random Forest Metrics

- R² log scale: `0.6151227871499995`
- R² original scale: `0.26330050491614987`
- MAE: `218208.65499609793`
- CV R² mean: `0.6240778965994925`
- CV R² std: `0.006651619998622336`

## Gradient Boosting Benchmark Metrics

- R² log scale: `0.5388068019269903`
- R² original scale: `0.18757307485169483`
- MAE: `242385.1623070141`

## Explanation of the Visuals Folder

The folder `realtor_random_forest.ipynb/visuals/` stores the saved PNG charts created by the random forest notebook. These charts are used to explain model performance and include actual-versus-predicted plots, residual plots, feature importance, model comparison, and cross-validation results.

Current saved visual outputs include:

- `actual_vs_predicted_rf.png`
- `cross_validation_r2_scores.png`
- `feature_importance_top15_rf.png`
- `model_performance_comparison.png`
- `residual_distribution_rf.png`
- `residuals_vs_predicted_rf.png`

The random forest notebook also includes additional zoomed chart cells designed for presentation use, with these expected filenames:

- `actual_vs_predicted_rf_zoomed.png`
- `residual_distribution_rf_zoomed.png`
- `residuals_vs_predicted_rf_zoomed.png`

## Explanation of the Folium Map Output

The file `housing_map.html` is the interactive map created by `mapping.ipynb`. It uses Folium to display housing-related data on a map after zip codes have been converted to latitude and longitude. This output helps connect the pricing analysis to a geographic view for presentation and interpretation.

## Suggested Order to Review or Run the Files

The recommended order is:

1. `README.md`
2. `PROJECT_SUMMARY.md`
3. `project BUSA 695.ipynb`
4. `cleaned_realtor_data.ipynb`
5. `realtor_modeling.ipynb`
6. `mapping.ipynb`
7. `realtor_random_forest.ipynb/random_forest_model.ipynb`

This order follows the project flow from raw data preparation to cleaned datasets, modeling, mapping, and final model evaluation visuals.

## Notes About Files Ignored by `.gitignore`

The root `.gitignore` is set up to exclude common generated, large, or temporary files from version control. It ignores:

- Python cache folders and bytecode files
- Notebook checkpoint folders
- Virtual environment folders
- Model files such as `*.pkl`
- Data files such as `*.csv` and `*.xlsx`
- Output files such as `*.html`, `*.png`, `*.jpg`, and `*.jpeg`
- Backup notebook files such as `*.backup.ipynb` and `*.before_*.ipynb`
- Operating system clutter files such as `.DS_Store` and `Thumbs.db`

This helps keep the repository focused on source notebooks and project documentation rather than large generated artifacts.

## Summary

This capstone project builds a complete workflow from raw real estate data to cleaned datasets, predictive models, model comparison results, saved visuals, and an interactive map. The random forest model is the main final model and outperformed the gradient boosting benchmark on the reported metrics.
