# Water Potability Analysis

This project explores a water potability dataset and builds a basic machine learning workflow to predict whether a water sample is labeled as potable based on physicochemical water-quality indicators.

The goal of this project is not to develop a production-level drinking water safety tool, but to practice a complete data analysis workflow, including data quality assessment, exploratory data analysis, missing-value handling, model training, and model comparison.

## Dataset

The dataset contains 3,276 water samples and 10 columns. Each sample includes several water-quality features:

- pH
- Hardness
- Solids
- Chloramines
- Sulfate
- Conductivity
- Organic carbon
- Trihalomethanes
- Turbidity
- Potability

`Potability` is the target variable, where:

- `0` = non-potable
- `1` = potable

## Project Workflow

The analysis includes the following steps:

1. Load and inspect the raw dataset
2. Check data tidiness and data quality
3. Visualize feature distributions and relationships
4. Compare two missing-value handling methods:
   - KNN imputation
   - Complete-case analysis
5. Train and evaluate classification models:
   - Majority-class baseline
   - Logistic regression
   - Random forest
6. Compare model performance using accuracy, ROC-AUC, precision, and recall

## Methods

### Missing-Value Handling

Two missing-value strategies were compared:

- **KNN Imputation**: Missing values were imputed after scaling the features. The train-test split was performed before imputation to avoid data leakage.
- **Complete-Case Analysis**: Rows with missing values were removed before model training.

### Models

Three types of models were evaluated:

- **Baseline model**: Always predicts the majority class
- **Logistic regression**: A simple linear classification model
- **Random forest**: A tree-based ensemble model that can capture non-linear relationships

## Key Results

The random forest model performed better than logistic regression and the baseline models under both missing-value handling methods.

| Missing Data Method | Model | Accuracy | ROC-AUC | Precision Class 1 | Recall Class 1 | Recall Class 0 |
|---|---|---:|---:|---:|---:|---:|
| KNN Imputation | Baseline | 0.610 | 0.500 | 0.000 | 0.000 | 1.000 |
| KNN Imputation | Logistic Regression | 0.610 | 0.553 | 0.000 | 0.000 | 1.000 |
| KNN Imputation | Random Forest | 0.659 | 0.656 | 0.640 | 0.285 | 0.898 |
| Complete-case Analysis | Baseline | 0.596 | 0.500 | 0.000 | 0.000 | 1.000 |
| Complete-case Analysis | Logistic Regression | 0.596 | 0.510 | 0.500 | 0.006 | 0.996 |
| Complete-case Analysis | Random Forest | 0.692 | 0.742 | 0.724 | 0.387 | 0.900 |

## Main Findings

- The target classes are moderately imbalanced, with more non-potable samples than potable samples.
- Most individual features have weak linear correlations with `Potability`.
- Logistic regression performs close to the baseline, suggesting that a simple linear model does not capture enough useful patterns in this dataset.
- Random forest achieves better overall performance and a higher ROC-AUC score.
- However, recall for potable water samples remains limited, meaning the model still misses many positive cases.

## Limitations

This project is exploratory and has several limitations:

- The dataset does not include contextual information such as sampling location, date, or measurement method.
- Model performance is limited, especially for identifying potable samples.
- No hyperparameter tuning was performed.
- The results should not be used as a real-world drinking water safety assessment.

## Tools Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Jupyter Notebook
