## 👨‍💻 Author

**Name:** `Mula Ganesh`

**Roll No:** `DA25M019`

Assignment 6 for DA5401 - Data Analytics Lab  

# Credit Card Default Prediction: Missing Data Imputation Analysis

## 📋 Project Overview

This project implements and compares various **missing data imputation strategies** for credit card default prediction. We artificially introduce Missing At Random (MAR) values into the UCI Credit Card Default dataset and evaluate how different imputation methods affect the performance of a Logistic Regression classifier.

## 🎯 Objectives

- Implement MAR missing data mechanism based on customer demographics
- Compare 4 different imputation strategies:
  1. **Median Imputation** (Baseline)
  2. **Linear Regression Imputation**
  3. **Non-Linear Regression Imputation** (Random Forest)
  4. **Listwise Deletion** (Complete Case Analysis)
- Evaluate classification performance using Logistic Regression
- Provide data-driven recommendations for handling missing data in credit risk assessment

## 📊 Dataset

**Source:** UCI Credit Card Default Dataset  
**Samples:** 30,000 credit card clients  
**Features:** 24 features including:
- Credit limit (`LIMIT_BAL`)
- Demographics (`SEX`, `EDUCATION`, `MARRIAGE`, `AGE`)
- Payment history (`PAY_0` to `PAY_6`)
- Bill amounts (`BILL_AMT1` to `BILL_AMT6`)
- Payment amounts (`PAY_AMT1` to `PAY_AMT6`)

**Target Variable:** `default.payment.next.month` (Binary: 0 = No Default, 1 = Default)

## 🔧 Technologies Used

```python
- Python 3.8+
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
```

## 📁 Project Structure

```
├── Assignment6.ipynb            # Main Jupyter notebook
└── README.md                    # This file
```

## 🚀 Getting Started

### Prerequisites

Install required packages:

```bash
pip install numpy pandas scikit-learn matplotlib seaborn
```

### Running the Notebook

1. Clone this repository:
```bash
git clone <your-repo-url>
cd <your-repo-name>
```

2. Download the UCI Credit Card dataset and place it in the project directory

3. Open Jupyter Notebook:
```bash
jupyter notebook assignment_notebook.ipynb
```

4. Run all cells sequentially (Cell → Run All)

## 📈 Methodology

### Part A: Data Preprocessing and Imputation

#### 1. Introducing MAR Missing Values
- **Columns affected:** `BILL_AMT2`, `PAY_AMT5`
- **Dependency column:** `AGE`
- **Missing rate:** ~7.5% per column
- **Mechanism:** Sigmoid function based on normalized age values

#### 2. Imputation Strategies

**Strategy 1: Median Imputation**
- Replace missing values with column median
- Simple, fast baseline approach
- Preserves central tendency

**Strategy 2: Linear Regression Imputation**
- Train linear regression on complete cases
- Predict missing values using other features
- Assumes linear relationships

**Strategy 3: Non-Linear Regression Imputation**
- Train Random Forest Regressor on complete cases
- Captures complex, non-linear relationships
- More flexible but computationally intensive

**Strategy 4: Listwise Deletion**
- Remove all rows with any missing values
- Reduces dataset size but maintains data quality
- Unbiased if data is MCAR

### Part B: Model Training and Evaluation

- **Classifier:** Logistic Regression with balanced class weights
- **Train/Test Split:** 80/20 with stratification
- **Feature Standardization:** StandardScaler applied to all features
- **Evaluation Metrics:**
  - Accuracy
  - Precision (Class 0 and Class 1)
  - Recall (Class 0 and Class 1)
  - F1-Score (Class 0 and Class 1)
  - Macro F1-Score
  - Weighted F1-Score

### Part C: Comparative Analysis

#### Performance Comparison
Visual comparison of all four models across multiple metrics:
- Overall Accuracy
- F1-Score for Default Prediction (Class 1)
- Precision vs Recall
- Macro vs Weighted F1-Score

#### Key Findings

**Trade-off: Listwise Deletion vs Imputation**
- Listwise deletion may perform well when:
  - Sample size is large (can afford data loss)
  - Missingness is truly random (MCAR)
  - Data quality is critical
- Imputation is preferred when:
  - Sample size is limited
  - Missing rate is high (>15%)
  - Missingness is systematic (MAR/MNAR)

**Linear vs Non-Linear Imputation**
- Linear regression often outperforms non-linear methods because:
  - Financial data exhibits linear relationships
  - Simpler models are less prone to overfitting
  - Moderate missing rates favor simple approaches
  - Linear models are more stable and interpretable

## 🏆 Results

### Model Performance Summary

| Model | Accuracy | F1-Score (Class 1) | Macro F1 | Weighted F1 |
|-------|----------|-------------------|----------|-------------|
| A: Median Imputation | ~0.68 | ~0.47 | ~0.62 | ~0.71 |
| B: Linear Regression | ~0.68 | ~0.48 | ~0.62 | ~0.71 |
| C: Non-Linear Regression | ~0.68 | ~0.46 | ~0.61 | ~0.70 |
| D: Listwise Deletion | ~0.69 | ~0.49 | ~0.63 | ~0.72 |

*Note: Exact values may vary due to random seed*

### Key Insights

1. **Listwise Deletion** showed slightly better performance but at the cost of losing ~10% of data
2. **Linear Regression Imputation** provided the best balance between data preservation and performance
3. **Non-Linear methods** did not provide significant improvements over linear approaches
4. **Median Imputation** performed reasonably well as a simple baseline

## 💡 Recommendations

### Best Strategy: **Linear Regression Imputation**

**Reasons:**
1. ✅ Preserves all data points (30,000 samples)
2. ✅ Competitive classification performance
3. ✅ Theoretically sound (respects MAR assumption)
4. ✅ Computationally efficient
5. ✅ Deterministic and reproducible
6. ✅ Interpretable for regulatory compliance

### When to Use Alternatives:

**Use Listwise Deletion when:**
- Missing rate is very low (<5%)
- Sample size is very large (>50k)
- Data quality is paramount
- Regulatory requirements mandate real data only

**Use Non-Linear Imputation when:**
- Clear evidence of non-linear relationships
- Very large datasets (>100k)
- Domain knowledge suggests complexity
- Performance gains justify computational cost

**Use Median Imputation when:**
- Need quick baseline
- Exploratory analysis phase
- Missing rate is minimal (<2%)
- Computational resources are limited

## 📚 Learning Outcomes

This project demonstrates:

1. **Missing Data Mechanisms:**
   - Understanding MCAR, MAR, and MNAR
   - Implementing realistic missing data scenarios

2. **Imputation Techniques:**
   - Simple statistical methods (median)
   - Regression-based approaches (linear and non-linear)
   - Complete case analysis (listwise deletion)

3. **Model Evaluation:**
   - Comprehensive performance metrics
   - Trade-off analysis
   - Visual comparison techniques

4. **Practical Decision Making:**
   - Balancing theoretical soundness with practical constraints
   - Domain-specific considerations (financial data)
   - Interpretability vs complexity trade-offs



