# 🕵️‍♂️ Multi-Class Profile Detection: Bot, Real, Scam, and Spam

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Latest-orange.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Optimized-green.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626.svg)

Welcome to my machine learning project focused on social engineering threat detection. The primary objective here is to accurately classify user profiles into four distinct categories: **Bot**, **Real**, **Scam**, and **Spam**. 

As fake accounts and automated bots become more sophisticated, simple binary classification (Real vs. Fake) isn't always enough. I built this pipeline to see how different classification algorithms handle a more nuanced, multi-class dataset, and to figure out if complex model aggregation (ensembling) actually justifies its computational cost in this scenario.

---

## 📑 Table of Contents
1. [About the Dataset](#-about-the-dataset)
2. [Project Workflow & Methodology](#-project-workflow--methodology)
3. [Key Findings & Results](#-key-findings--results)
4. [Tech Stack](#-tech-stack)
5. [Repository Structure](#-repository-structure)
6. [How to Run It](#-how-to-run-it)
7. [Future Work](#-future-work)

---

## 📊 About the Dataset

The model is trained on a dataset of **15,000 generated user profiles**. 

*   **Target Classes:** 4 (`Bot`, `Real`, `Scam`, `Spam`)
*   **Feature Focus:** The dataset includes various behavioral and structural metrics typical of social media accounts (e.g., posting frequency, account age, follower-to-following ratios, keyword flags). 
*   *Note: Due to file size limits, the raw dataset might not be included in this repo, but the preprocessing scripts and feature definitions are fully documented in the notebooks.*

---

## 🧠 Project Workflow & Methodology

I ran the data through a complete machine learning lifecycle, comparing baseline performance with highly optimized versions. Here is the step-by-step breakdown:

1.  **Data Preprocessing:** Handled missing values, encoded categorical variables, and scaled numerical features to ensure algorithms like Logistic Regression weren't biased by feature magnitude.
2.  **Baseline Training:** Tested models out-of-the-box to establish a performance floor. I used **Random Forest**, **XGBoost**, and **Logistic Regression**.
3.  **Feature Selection:** Implemented **Recursive Feature Elimination (RFE)**. This was crucial for stripping out noisy, irrelevant features and identifying the core metrics that actually dictate an account's authenticity.
4.  **Hyperparameter Tuning:** Applied Grid/Random Search cross-validation to fine-tune the tree depths, learning rates, and estimators of the best-performing models to squeeze out maximum accuracy.
5.  **Ensemble Methods:** Combined the models using both **Hard Voting** (majority rules) and **Soft Voting** (probability-based) classifiers to test if a "wisdom of the crowd" approach could beat individual algorithms.

---

## 🏆 Key Findings & Results

One of the biggest takeaways from this experiment was that **more complex doesn't always mean better.** 

Initially, I hypothesized that the ensemble methods would easily sweep the board by compensating for individual model weaknesses. However, the data proved otherwise. Highly optimized, single tree-based models ended up outperforming the aggregated voting mechanisms on the test set.

| Model / Approach | 5-Fold CV Score | Test Set Accuracy |
| :--- | :---: | :---: |
| **XGBoost (Tuned)** | 0.9821 | **96.87%** |
| **Random Forest (Tuned)** | 0.9785 | **95.34%** |
| **Soft Voting Ensemble** | 0.9510 | 94.78% |
| **Hard Voting Ensemble** | 0.9388 | 92.24% |
| **Logistic Regression (Tuned)** | 0.8512 | 81.63% |

**Conclusion:** For this specific feature set, a highly optimized gradient boosting approach (XGBoost) is vastly more effective and resource-efficient than aggregating multiple models together. 

---

## 🛠 Tech Stack

*   **Language:** Python
*   **Data Manipulation:** `pandas`, `numpy`
*   **Machine Learning:** `scikit-learn` (for base models, metrics, RFE, Ensembles)
*   **Advanced Boosting:** `xgboost`
*   **Environment:** Jupyter Notebook / Google Colab

---

## 📂 Repository Structure

<img width="454" height="132" alt="image" src="https://github.com/user-attachments/assets/ceb51c5f-f4a5-41e6-a89f-b1a428558169" />
