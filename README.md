

# 💳 Fraud Detection System

A **machine learning–based fraud detection system** that identifies fraudulent financial transactions using **behavioral feature engineering, logistic regression, random forest, and SHAP explainability**.

This project focuses on **real-world fraud patterns**, not just high transaction amounts.

---

## 📌 Project Overview

Financial fraud is rare but highly costly. This project builds a **proactive fraud detection model** using transaction behavior rather than rule-based flags.

### 🔍 Key Goals

* Detect fraudulent transactions with **high recall**
* Avoid data leakage
* Engineer **behavior-driven features**
* Provide **model interpretability** for business decisions

---

## 🧠 Dataset

* **Source:** `Fraud.csv`
* **Target variable:** `isFraud`
* **Highly imbalanced dataset**
* Fraud rate ≈ **0.13%**
* Download this dataset :https://drive.google.com/file/d/1Y2qI7Mm79LYOtjDcnFdYT-moNdw8oY9Z/view?usp=drive_link

---

## 🔧 Data Preprocessing & Cleaning

### ✔ Removed Columns

| Column                 | Reason                             |
| ---------------------- | ---------------------------------- |
| `isFlaggedFraud`       | Data leakage & low variance        |
| `nameOrig`, `nameDest` | High cardinality IDs → overfitting |

### ✔ Missing Values

* No missing values found

---

## 📊 Feature Engineering

Behavior-based features were created to capture fraud patterns:

```text
orig_balance_diff = oldbalanceOrg - newbalanceOrig
dest_balance_diff = newbalanceDest - oldbalanceDest
amount_to_oldbalance_ratio = amount / (oldbalanceOrg + 1)
```

📌 **Why this matters:**
Fraud is characterized by **abnormal balance movement**, not just large amounts.

---

## 📉 Log Transformation

Applied `np.log1p()` on skewed numerical features:

* `amount`
* `oldbalanceOrg`
* `newbalanceOrig`
* `oldbalanceDest`
* `newbalanceDest`

### Benefits:

* Reduces skewness
* Preserves fraud signals
* Handles zero values safely
* Industry best practice for financial data

---

## ⚠ Outlier Handling

* Outliers **were NOT removed**
* Fraud transactions are naturally extreme
* Used:

  * Log transformation
  * Tree-based models (robust to outliers)

---

## 🏗 Model Building

### 1️⃣ Logistic Regression

* `class_weight = balanced`
* Optimized for **high recall**

**Result:**

* ✔ Very high fraud recall
* ❗ Low precision (expected trade-off)

📌 *Business insight:*
Missing fraud is more costly than false alarms.

---

### 2️⃣ Random Forest Classifier

* Handles non-linear patterns
* Robust to outliers
* Used for **feature importance & explainability**

---

## 📈 Model Evaluation

* Stratified train-test split
* Classification report used
* Focus metrics:

  * Recall (fraud capture)
  * False positives
  * Business impact

---

## 🔍 Explainability (SHAP)

Used **SHAP (SHapley Additive exPlanations)** to:

* Interpret model decisions
* Identify top fraud-driving features
* Improve trust & transparency

📌 Key fraud indicators:

* Abnormal balance depletion
* High transaction-to-balance ratio
* `TRANSFER` and `CASH_OUT` transactions

---

## 📊 Key Insights

✅ Fraud ≠ just high amount
✅ Fraud = **abnormal balance behavior**
✅ Behavioral features outperform raw values
✅ IDs should never be used as predictors

---

## 🛡 Fraud Prevention Recommendations

* Real-time fraud scoring
* Adaptive authentication
* Velocity & transaction limits
* Continuous model monitoring
* A/B testing for controls
* Analyst feedback loop

---

## 🧪 How to Measure Effectiveness

* Fraud rate reduction
* False positive rate
* Financial loss savings
* Customer friction metrics
* Model drift monitoring

---

## 🛠 Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* Matplotlib
* SHAP
* Jupyter / Google Colab

---

## 👨‍💻 Author

**Dipanshu Mishra**
📧 Email: [mdipanshu713@gmail.com](mailto:mdipanshu713@gmail.com)
📞 Contact: 8454081928

---

## 🚀 How to Run

```bash
pip install pandas numpy scikit-learn matplotlib shap
```

```bash
python frud_detection_part_2.py
```
