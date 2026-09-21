# Changing Health-Age Relationships Across the Pandemic

## Insights from Explainable Neural Networks

This repository contains the code, data-processing workflow, modelling experiments, and explainability analysis developed for an MSc Statistical Data Science dissertation investigating whether relationships between health indicators and chronological age changed across the COVID-19 pandemic period.

The study uses data from the **National Health and Nutrition Examination Survey (NHANES)** and compares traditional statistical models with nonlinear and machine-learning approaches.

## Project Overview

Ageing is associated with complex changes across cardiovascular, metabolic, liver, kidney, and other physiological systems. These relationships may be nonlinear and may not be fully represented by conventional linear models.

This project investigates whether explainable machine-learning models can identify nonlinear relationships between routinely measured health indicators and **chronological age**, and whether the relative importance of these indicators differs between pre-pandemic and post-pandemic NHANES samples.

Three modelling approaches are compared:

- **Linear Regression (LR)** as an interpretable statistical baseline
- **Generalized Additive Models (GAMs)** for flexible nonlinear relationships
- **Multilayer Perceptron (MLP)** neural networks for more complex nonlinear patterns and interactions

Explainability techniques are used to investigate how individual health variables contribute to model predictions.

## Research Objectives

The main objectives are:

1. Evaluate how well selected health indicators predict chronological age.
2. Compare linear, additive nonlinear, and neural-network modelling approaches.
3. Investigate nonlinear relationships between health indicators and age.
4. Use explainable AI techniques to interpret neural-network predictions.
5. Compare health-age relationships between pre-pandemic and post-pandemic NHANES samples.

The analysis is **predictive and associational rather than causal**. Differences between periods should not be interpreted as evidence that the COVID-19 pandemic directly caused changes in particular health indicators.

## Data

The project uses publicly available **NHANES** data.

### Variables

| Category | Variables |
| --- | --- |
| Demographic | Sex |
| Anthropometric | BMI |
| Cardiovascular | Systolic blood pressure, Diastolic blood pressure |
| Glycaemic | Glucose, HbA1c |
| Lipid | Total cholesterol, HDL cholesterol |
| Liver-related | Albumin, ALT, AST, GGT |
| Kidney-related | BUN, Creatinine |

**Target variable:** Chronological age in years.

## Repository Structure

```text
Changing-Health-Age-Relationships-Across-the-Pandemic-Insights-from-Explainable-Neural-Networks/
├── 2017-2018data/
├── datafiles/
├── postpandemic/
├── Dissertation_Pre_Post_Comparison.ipynb
├── linear regression 2017-2018.ipynb
├── linear regression post pandemic.ipynb
├── LICENSE
└── README.md
```

## Methodology

### Data Preparation

NHANES datasets are combined using the participant identifier (`SEQN`). Relevant demographic, examination, and laboratory variables are selected and transformed into a consistent modelling dataset.

The preprocessing workflow includes variable selection, dataset merging, missing-value handling, categorical-variable encoding, train/test splitting, and feature scaling where required.

### Linear Regression

Linear Regression provides an interpretable statistical baseline for assessing approximately linear relationships between health indicators and chronological age.

### Generalized Additive Model

The GAM extends linear regression by allowing predictors to have smooth nonlinear relationships with age:

```text
Age = β₀ + f₁(X₁) + f₂(X₂) + ... + fₚ(Xₚ) + ε
```

This provides a useful intermediate model between conventional linear regression and a neural network.

### Multilayer Perceptron

A feed-forward MLP neural network is used to capture more complex nonlinear relationships and interactions between health indicators.

## Model Evaluation

Predictive performance is evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- R²
- Cross-validation

## Explainable AI

### SHAP

**SHAP (SHapley Additive exPlanations)** is used to interpret the MLP and estimate the contribution of individual health indicators to its predictions.

Mean absolute SHAP values provide a measure of global feature importance and allow comparison of feature importance between the pre-pandemic and post-pandemic samples.

## Pre-Pandemic Results

For the 2017-2018 held-out test sample:

| Model | MAE | RMSE | R² |
| --- | ---: | ---: | ---: |
| Linear Regression | 10.792 | 13.295 | 0.431 |
| GAM | 9.273 | 11.422 | 0.580 |
| MLP | **8.347** | **10.608** | **0.638** |

The results show progressively stronger predictive performance when moving from Linear Regression to GAM and MLP, suggesting that nonlinear modelling captures additional predictive structure in the selected health indicators.

## Explainability Findings

In the pre-pandemic MLP analysis, systolic blood pressure had the largest mean absolute SHAP value.

Other influential predictors included ALT, BUN, HbA1c, AST, diastolic blood pressure, glucose, BMI, albumin, and HDL cholesterol.

The pre/post comparison also showed changes in the relative importance of some predictors. These differences represent **model-derived predictive associations** and should not be interpreted as causal effects of the pandemic.

## Key Contribution

The project combines increasingly flexible predictive models with explainability:

```text
Linear Regression
        ↓
Generalized Additive Model
        ↓
Neural Network
        ↓
Explainable AI
        ↓
Pre-Pandemic vs Post-Pandemic Comparison
```

This framework allows both predictive performance and changes in learned health-age relationships to be examined.

## Running the Project

Clone the repository:

```bash
git clone https://github.com/techie-code/Changing-Health-Age-Relationships-Across-the-Pandemic-Insights-from-Explainable-Neural-Networks.git
```

Enter the project directory:

```bash
cd Changing-Health-Age-Relationships-Across-the-Pandemic-Insights-from-Explainable-Neural-Networks
```

Launch Jupyter:

```bash
jupyter notebook
```

The main pre/post analysis is contained in:

```text
Dissertation_Pre_Post_Comparison.ipynb
```

## Limitations

NHANES is observational and cross-sectional. Therefore, this study identifies statistical and predictive associations rather than causal relationships.

Differences between pre-pandemic and post-pandemic models may reflect changes in the sampled population, measurement differences, sampling variability, changes in health patterns, model uncertainty, or broader temporal changes.

Consequently, observed differences should not automatically be attributed directly to COVID-19 or the pandemic.

## Author

**Aishwarya Lakshmi Sridharan**

MSc Statistical Data Science  
School of Mathematics

Developed as part of an MSc dissertation project.

## License

This project is distributed under the **Apache License 2.0**. See the `LICENSE` file for details.

## Acknowledgements

This project uses publicly available data from the **National Health and Nutrition Examination Survey (NHANES)** conducted by the U.S. National Center for Health Statistics.
