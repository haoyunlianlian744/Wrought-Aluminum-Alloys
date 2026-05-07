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

### 8.nsga2_AHS2_optimization.ipynb
This notebook optimizes the T6 heat treatment parameters (aging temperature `Tage` and aging time `tage`) for AHS-2 aluminum alloy using NSGA-II. It must be run after File 7, which provides the champion model type and best hyperparameters saved in `model_selection/`. The AHS-2 subset (34 samples) is extracted from the full dataset and used to re-tune the surrogate models for domain-specific accuracy. NSGA-II then searches the continuous process space (Tage: 150~185°C, tage: 5~10h) to simultaneously maximize YS, UTS, and El, yielding an optimal process window of Tage = 171.0~172.5°C and tage = 5.2~6.8h.

### 9.visualization.ipynb
Used for result visualization.  
It generates:
- multi-model comparison plots
- predicted vs. experimental scatter plots on the test set
- SHAP interpretation plots  

These figures are used in the main manuscript and supplementary material.

### Dataset
This study compiled 524 valid wrought aluminum alloy samples from literature and industrial experiments. YS, UTS and elongation were selected as prediction targets, and alloy compositions along with heat treatment parameters were used as input features. The processed dataset supporting the findings of this study is available in Mendeley Data at https://doi.org/10.17632/gw8fvv7wth.1.

Among them, 429 samples were sourced from Hu et al. (2024, MSEA, DOI: 10.1016/j.msea.2024.147381), whose original dataset is available at https://github.com/UQ43815685/ageing_behaviour_Al_alloys_with_feature_screening.

The rest data were collected from supplementary literature and self-performed experiments. The source information of all samples is specified in the data table. 
