# Hazardous Asteroid Prediction AI

## Project Information

| Field | Details |
|---|---|
| Project | Hazardous Asteroid Prediction AI |
| Author | Shaahamad Syed |
| Program | Machine Learning Internship |
| Domain | Machine Learning / Data Science |
| Year | 2026 |
| GitHub | https://github.com/shaahamadsyed |

## Project Overview

This project develops a machine learning system to classify near-Earth objects as **Hazardous** or **Non-Hazardous** using asteroid characteristics.

The project uses supervised binary classification and includes data preprocessing, exploratory data analysis, feature selection, model development, class-imbalance handling, threshold tuning, model evaluation, feature importance analysis, and a prediction interface.

## Objective

The main objective is to build a machine learning model that can estimate the probability that an asteroid is hazardous based on available asteroid characteristics.

The target variable is:

- `0` = Non-Hazardous
- `1` = Hazardous

## Dataset

The dataset contains near-Earth object information including:

- Estimated minimum diameter
- Estimated maximum diameter
- Relative velocity
- Miss distance
- Absolute magnitude
- Hazardous classification

During preprocessing, redundant and constant columns were removed.

The final model uses the following features:

1. `est_diameter_min`
2. `relative_velocity`
3. `miss_distance`
4. `absolute_magnitude`

The dataset contains **90,836 records**.

The target distribution is imbalanced:

- Non-Hazardous: 81,996
- Hazardous: 8,840

Therefore, accuracy alone was not used to evaluate the models.

## Project Workflow

### 1. Data Preprocessing

The dataset was inspected for:

- Missing values
- Duplicate records
- Data types
- Class distribution
- Constant features
- Redundant features

The target variable was converted from Boolean values into binary values.

The data was divided into training and testing sets using stratified sampling.

Feature standardization was performed using `StandardScaler`.

### 2. Exploratory Data Analysis

Exploratory analysis included:

- Hazardous vs Non-Hazardous class distribution
- Feature distributions
- Boxplots
- Grouped statistical analysis
- Correlation analysis
- Feature relationships with the target variable

The analysis showed differences between hazardous and non-hazardous objects in several numerical features.

### 3. Feature Selection

The following features were selected for model development:

- Estimated minimum diameter
- Relative velocity
- Miss distance
- Absolute magnitude

`est_diameter_max` was excluded because it is essentially a fixed multiple of `est_diameter_min`.

Constant features such as `orbiting_body` and `sentry_object` were also excluded.

Identifiers such as `id` and `name` were not used as predictive features.

### 4. Model Development

The following classification models were evaluated:

- Logistic Regression
- Random Forest
- Gradient Boosting

Class-imbalance handling was also evaluated using:

- Class weighting
- Sample weighting

Evaluation focused on multiple metrics rather than accuracy alone.

### 5. Threshold Tuning

Because the hazardous class is the minority class, the default classification threshold of `0.50` was evaluated.

A threshold of `0.25` was selected based on F1 score during threshold analysis.

This threshold increases the sensitivity of the model to hazardous objects while changing the precision/recall trade-off.

### 6. Model Evaluation

The final Random Forest model achieved the following results on the held-out test set at the selected threshold:

| Metric | Score |
|---|---:|
| Accuracy | 88.38% |
| Precision | 44.13% |
| Recall | 73.08% |
| F1 Score | 55.03% |
| ROC-AUC | 93.20% |
| PR-AUC | 58.75% |

The model evaluation also includes:

- Confusion matrix
- ROC curve
- Precision-Recall curve
- F1-score comparison

### 7. Feature Importance

Random Forest feature importance was used to examine the relative contribution of the selected features.

The feature importance values were:

| Feature | Importance |
|---|---:|
| Miss Distance | 29.92% |
| Relative Velocity | 26.82% |
| Estimated Diameter | 22.44% |
| Absolute Magnitude | 20.82% |

These values represent model-based feature importance and should not be interpreted as causal relationships.

## Final Model

The final deployed model is a:

**Random Forest Classifier**

Configuration:

- Number of estimators: 200
- Random state: 42
- Classification threshold: 0.25

The trained model and preprocessing objects were saved using `joblib`.

## Prediction Interface

The notebook includes an interactive prediction interface.

The user provides:

- Estimated diameter
- Relative velocity
- Miss distance
- Absolute magnitude

The system then returns:

- Hazard probability
- Classification threshold
- Hazardous / Non-Hazardous prediction

Example input:

```text
Estimated diameter: 0.1
Relative velocity: 45000
Miss distance: 38000000
Absolute magnitude: 23
