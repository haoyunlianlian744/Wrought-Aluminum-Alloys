# Project Overview

This project develops a machine-learning workflow for predicting the tensile properties of wrought aluminum alloys, including yield strength (YS), ultimate tensile strength (UTS), and elongation (El). The workflow covers data merging, missing-value imputation, outlier screening, dataset splitting, model selection, and visualization.

## Notebook Description

### 1.random_forest_prediction(5).ipynb
Used for random-forest-based prediction and repeated evaluation.  
This notebook mainly serves as an auxiliary file for some preprocessing or comparison tasks.

### 2.dedup_and_merge(5).ipynb
Used for merging multi-source data and removing duplicate samples.  
It generates the deduplicated base dataset.

### 3.missing_value_imputation(8).ipynb
Used for missing-value imputation.  
A staged supervised imputation strategy is adopted:
- Stage 1: impute UTS
- Stage 2: impute YS
- Stage 3: impute El  

This notebook also compares 12 candidate models and evaluates the effect of imputation on downstream modeling performance.

### 4.outlier_detection(5).ipynb
Used for outlier screening.  
A three-layer strategy is applied:
- physical-boundary checking
- correlation-based abnormality detection
- PCA + K-means distance-based outlier detection  

This notebook outputs the cleaned dataset used for final modeling.

### 5.distribution_evaluation(5).ipynb
Used for data distribution analysis and EDA.  
It generates descriptive statistics, variable ranges, and related visualizations.

### 6.train_test_split(5).ipynb
Used for dataset splitting.  
It compares random split, stratified split, and SPXY split, and evaluates distribution consistency between the development set and the test set. The final split used for formal modeling is determined here.

### 7.model_selection_6.ipynb
Used for formal modeling and model selection.  
Main tasks include:
- Stage 1 fixed-parameter screening of six candidate models
- champion model selection
- Stage 2 Optuna hyperparameter optimization
- independent test-set evaluation
- export of final result tables and prediction details

### 8.visualization.ipynb
Used for result visualization.  
It generates:
- multi-model comparison plots
- predicted vs. experimental scatter plots on the test set
- SHAP interpretation plots  

These figures are used in the main manuscript and supplementary material.

## Recommended Execution Order

The notebooks are recommended to be run in the following order:

2.dedup_and_merge  
→ 3.missing_value_imputation  
→ 4.outlier_detection  
→ 5.distribution_evaluation  
→ 6.train_test_split  
→ 7.model_selection_6  
→ 8.visualization

## Notes

The final formal modeling uses the cleaned dataset and 16 directly measurable input variables:

Si, Fe, Cu, Mn, Mg, Cr, Zn, V, Ti, Zr, Ni, Be, Sc, Tsol, Tage, tage.

The prediction targets are:
- YS
- UTS
- El
