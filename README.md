# Employee Attrition Prediction

This repository contains the notebooks and datasets used for the paper *Explainable Machine Learning for Employee Attrition Prediction Using Individual and Voting Classifiers*.

The study compares ReliefF and MultiSURF feature selection with individual classifiers and soft- and hard-voting ensembles on two datasets:

- IBM HR Analytics Employee Attrition dataset
- Saudi employee attrition survey

F1 is the primary evaluation metric. The feature count is selected using five-fold cross-validation on the training partition. Target encoding, scaling, feature ranking, and SMOTE are fitted using training-fold data only. The untouched 20% holdout partition is used to compare the fitted candidates and identify the best observed configuration. Because multiple candidates are compared on the same holdout, this final comparison should be interpreted cautiously.

## Repository structure

```text
ibm/
  ibm-notebook.ipynb
  WA_Fn-UseC_-HR-Employee-Attrition.csv
saudi/
  saudi-notebook.ipynb
  Original Dataset of Employee Attrition.xlsx
requirements.txt
```

Both notebooks include:

1. Data cleaning and preprocessing
2. Fold-local ReliefF and MultiSURF ranking
3. Feature-count optimisation using mean CV F1
4. Individual and voting-classifier comparison
5. Three-seed stability analysis of selected voting configurations
6. Holdout evaluation
7. SHAP summary, dependence, local-case, and no-SMOTE checks

## Main reported results

- IBM: ReliefF with a voting classifier (Gradient Boosting and XGBoost) obtained held-out F1 of 0.494 and recall of 0.404.
- Saudi: MultiSURF with a voting classifier (Random Forest and XGBoost) obtained held-out F1 of 0.804 and recall of 0.777. It tied MultiSURF-XGBoost on held-out F1.

## Running the notebooks

Create a Python environment, install the dependencies, and launch Jupyter from the repository root:

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

Run each notebook from its own dataset directory so that its relative dataset path resolves correctly. The full model comparison is computationally intensive because feature ranking and preprocessing are repeated within the cross-validation folds.

## Reproducibility notes

- The main random seed is 42.
- Seeds 42, 43, and 44 are used for the fixed-configuration stability analysis.
- The three-seed analysis covers voting configurations only. It does not estimate uncertainty in the complete model- and feature-selection procedure.
- The Saudi target is retrospective. It records whether respondents have previously left an employer rather than tracking a future departure.
- SHAP results describe fitted associations and should not be interpreted as causal effects.
