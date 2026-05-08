# BUSA 695 Capstone: Real Estate Price Prediction

## Project Title

Real Estate Price Prediction for the BUSA 695 Capstone Project

## Capstone Goal

The goal of this project is to build and evaluate predictive models that estimate residential property prices using housing and location-related features. The project combines data cleaning, exploratory analysis, regression modeling, tree-based modeling, and geographic visualization to support a practical real estate pricing use case.

## Business Problem

Home prices vary widely across properties, regions, and property characteristics. Buyers, sellers, analysts, and real estate professionals need a structured way to estimate likely property values based on available listing information. This project addresses that problem by preparing housing data and testing predictive models that can estimate price from property features such as size, bedrooms, bathrooms, lot size, state, and zip-related location information.

## Dataset Flow

The project follows this data pipeline:

`realtor-data.csv` -> `realtor_master.csv` -> `cleaned_simple.csv` / `realtor_modeling.csv`

- `realtor-data.csv`
  Raw source dataset used as the starting point for the project.
- `realtor_master.csv`
  Cleaned master dataset created after missing-value handling, column removal, and status encoding.
- `cleaned_simple.csv`
  Simplified cleaned dataset with location fields removed for modeling workflows that do not require them.
- `realtor_modeling.csv`
  Modeling-ready dataset created for downstream predictive modeling, including the random forest workflow.

## Purpose of Each Notebook

### `project BUSA 695.ipynb`

This notebook performs the early data preparation steps. It loads the raw dataset, explores its structure, handles missing values, encodes the `status` field, and saves the cleaned master file `realtor_master.csv`.

### `cleaned_realtor_data.ipynb`

This notebook further reviews and filters the cleaned master dataset. It creates `cleaned_simple.csv`, removes unrealistic values and outliers, and explores relationships among important numeric variables.

### `realtor_modeling.ipynb`

This notebook prepares a modeling-ready dataset and tests multiple linear regression setups. It also creates `realtor_modeling.csv`, which is used later in the random forest notebook.

### `mapping.ipynb`

This notebook supports the geographic presentation portion of the project. It trains a random forest model for mapping use, adds predicted prices and errors to property records, geocodes zip codes, and creates an interactive housing map.

### `realtor_random_forest.ipynb/random_forest_model.ipynb`

This notebook develops and evaluates the main random forest model. It loads `realtor_modeling.csv`, trains the random forest model, saves model outputs, calculates evaluation metrics, and creates presentation-ready visualizations.

## Modeling Approach

The project uses multiple modeling stages:

- Data cleaning and preparation to improve data quality and create modeling-ready files
- Linear regression models as baseline comparison models
- Random forest regression as the main tree-based model
- Gradient boosting regression as an additional benchmark
- Cross-validation to evaluate model stability
- Residual and actual-vs-predicted visualizations to assess model behavior

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

## Visual Outputs Created

The project includes the following saved model evaluation visuals:

- `actual_vs_predicted_rf.png`
- `cross_validation_r2_scores.png`
- `feature_importance_top15_rf.png`
- `model_performance_comparison.png`
- `residual_distribution_rf.png`
- `residuals_vs_predicted_rf.png`

Additional zoomed chart cells were added in the random forest notebook for presentation use, with expected output filenames:

- `actual_vs_predicted_rf_zoomed.png`
- `residual_distribution_rf_zoomed.png`
- `residuals_vs_predicted_rf_zoomed.png`

## Project Output Locations

- Interactive map:
  `housing_map.html`
- Root-level model file:
  `rf_model.pkl`
- Random forest notebook model file:
  `realtor_random_forest.ipynb/random_forest_model.pkl`
- Random forest results summary:
  `realtor_random_forest.ipynb/model_results.txt`
- Random forest visuals:
  `realtor_random_forest.ipynb/visuals/`

## Limitations

- The project depends on large CSV and model files, which can be difficult to store and share in a standard GitHub repository.
- Some notebook paths are relative and depend on the working directory used when opening the notebooks.
- The random forest workflow uses sampled data in some steps to keep runtime manageable on local hardware.
- R² on the original price scale is lower than on the log scale, which suggests the model has more difficulty predicting extreme price values.
- The project structure currently mixes notebooks, outputs, data files, and models in the same root folder, which can reduce maintainability.

## Future Improvements

- Reorganize the repository into separate folders for notebooks, raw data, processed data, models, outputs, and backups
- Add a single reproducible pipeline script instead of relying only on notebook execution order
- Replace hard-coded paths with portable relative paths throughout the project
- Add feature selection and hyperparameter tuning for the random forest and gradient boosting models
- Evaluate additional algorithms and compare performance across more metrics
- Improve treatment of outliers and high-value homes
- Add a requirements file with pinned package versions for reproducibility

## Running the Project Locally

1. Clone or download the project folder to your local machine.
2. Create and activate a Python environment.
3. Install the required libraries, including:
   `pandas`, `numpy`, `matplotlib`, `scikit-learn`, `joblib`, `folium`, and `pgeocode`
4. Make sure the project data files are present in the root folder:
   `realtor-data.csv`, `realtor_master.csv`, `cleaned_simple.csv`, and `realtor_modeling.csv`
5. Open the notebooks in Jupyter Notebook or JupyterLab.
6. Run the notebooks in this general order:
   `project BUSA 695.ipynb`
   `cleaned_realtor_data.ipynb`
   `realtor_modeling.ipynb`
   `mapping.ipynb`
   `realtor_random_forest.ipynb/random_forest_model.ipynb`
7. Review the generated outputs, including the model files, the HTML map, the text summary, and the visual PNG files.

## Summary

This capstone project builds a full workflow for real estate price prediction, from raw data preparation through model evaluation and presentation outputs. The random forest model outperformed the gradient boosting benchmark on the reported metrics and provides the main final modeling result for the project.
