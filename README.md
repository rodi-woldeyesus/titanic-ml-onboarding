# Titanic ML Onboarding Project 

This repository contains my Titanic onboarding project for a machine learning internship. 

# Models

- Logistic Regression (81% accuracy)
- CatBoost (83% accuracy)

# Repository Structure

- data/ - Titanic dataset files from Kaggle
- notebooks/ - Jupyter notebooks for model development evaluation
- environment.yaml - Conda environment configuration
- .gitignore - Excludes generated files from version control

# Notebooks

1) 01_logistic_regression.ipynb

- Builds and Evaluates a Logistic Regression model for predicting Titanic passenger survival. 

2) 02_catboost.ipynb

- Builds and evaluates a CatBoost model for predicting Titanic passenger survival. 

# Environment Setup

- conda env create -f environment.yaml
- conda activate titanic-ml