# 📊 Papcorns Data Scientist Technical Assessment

This repository contains my solution for the **Papcorns Data Scientist technical case study**. The goal of this project was to analyze user-level behavior in a mobile app context and solve data science tasks including churn prediction and potential lifetime value (pLTV) estimation.

---

## 🧠 Objectives

The following business and analytics questions were addressed:

### ✅ Core Tasks
1. Total subscription revenue by country  
2. Number of trials started by Instagram users  
3. Acquisition channel classification (Paid vs Organic)  
4. Trial-to-subscription conversion rate (overall and by source)  
5. Median subscription duration by country  
6. Average lifetime value (LTV) by country  

### 🧪 Bonus Tasks
7. Predict churn probability for user #1002 (Clark Kent)  
8. Estimate potential LTV (pLTV) for user #1001 (Bruce Wayne)

---

## 📦 Dataset Description

The project uses a SQLite database (`papcorns.sqlite`) with the following structure:

### Table: `users`
- `id`: Unique user ID
- `created_at`: Signup date
- `attribution_source`: User acquisition channel (`instagram`, `tiktok`, `organic`)
- `country`: User country (`US`, `TR`, `NL`)
- `name`: Full name

### Table: `user_events`
- `id`: Unique event ID
- `created_at`: Timestamp
- `user_id`: Linked user ID
- `event_name`: One of `app_install`, `trial_started`, `subscription_started`, `subscription_renewed`, `subscription_cancelled`, etc.
- `amount_usd`: Amount charged for subscriptions (if applicable)

---

## 🛠️ Technologies Used

- Python 3.10
- SQLite3
- Pandas, NumPy
- Matplotlib, Seaborn
- LightGBM
- Scikit-learn
- SHAP
- Jupyter Notebook

---

## 📈 Analytical Approach

### Core Analysis (Tasks 1–6)

Detailed SQL + pandas-based exploration was performed.  
Segmentation, joins, and aggregations were used to compute key metrics including:

- Subscription revenue by country
- Conversion ratios by acquisition source
- Retention durations and median lifetime
- Revenue per user → LTV

---

## 🤖 Machine Learning Models

### 🎯 Bonus Task 7: Churn Prediction for Clark Kent

- **Model**: LightGBM Classifier  
- **Features**: Trial/subscription counts, renewal counts, total events, active days, acquisition source, and country (encoded)  
- **Clark Kent's Result**:
  - Only event: `app_install`
  - Days since last activity: 52
  - **Predicted churn probability: 35%**
- **Explainability**: SHAP values used to justify model output

### 🔮 Bonus Task 8: pLTV Prediction for Bruce Wayne

- **Model**: LightGBM Regressor  
- **Target**: `total_amount_usd`
- **Features**: Trial/subscription/renewal counts, activity span, country, acquisition source
- **Bruce Wayne's Result**:
  - Early behavior: app install → trial → subscription
  - Current spend: $9.99
  - **Predicted pLTV: $38.42**
- **Model Evaluation**:
  - MAE: $0.14
  - RMSE: $0.43
  - R² Score: 1.00
  - SHAP + residual analysis confirms prediction quality

---

## 📊 Key Insights

- Paid channels (Instagram, TikTok) deliver higher conversion rates and LTV.
- Subscription engagement and recent activity are key drivers of retention.
- US-based users generate longer subscription periods and more revenue.
- Passive users (like Clark Kent) are churn risks, even if not explicitly unsubscribed.

---

## 📌 Case Reasoning Per Task

Refer to the full breakdown in `Case Study` section within the notebook for:
- What method was used
- Why it was used
- What insights it generated
- Model interpretations

---

## ⚙️ Setup & Run Instructions

To run this project locally, follow the steps below.

### 1. Clone the Repository

```bash
clone this Repository
cd papcorns-ds-case