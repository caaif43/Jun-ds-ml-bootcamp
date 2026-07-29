# Final Project Proposal

**Date:** July 2026
**GitHub:** https://github.com/caaif43/ds-ml-bootcamps

---

# 1. Certificate Name

**Abdullahi Hassan Shire**

---

# 2. Project Title and Description

## Title

# Customer Shopping Purchase Prediction System

## Description

This project aims to build a Machine Learning system that predicts the purchase amount of customers based on their demographic information and shopping behavior. The system helps businesses better understand customer purchasing patterns, improve marketing strategies, and support business decision-making.

The project will include data preprocessing, model training, model evaluation, and deployment using FastAPI with a responsive web-based frontend. Users will be able to enter customer information through a modern dashboard and receive a predicted purchase amount in real time.

---

# 3. Problem Type

## Regression (Supervised Learning)

The objective is to predict the customer's purchase amount (a continuous numerical value).

### Output

Purchase Amount (USD)

---

# 4. Dataset

## Source

Customer Shopping Trends Dataset (Kaggle)

https://www.kaggle.com/datasets/iamsouravbanerjee/customer-shopping-trends-dataset/data

## Dataset Size

- 3,900 customer records
- 19 columns

## Target Column

Purchase Amount (USD)

## Main Features

- Age
- Gender
- Category
- Item Purchased
- Location
- Size
- Color
- Season
- Review Rating
- Subscription Status
- Payment Method
- Shipping Type
- Discount Applied
- Promo Code Used
- Previous Purchases
- Preferred Payment Method
- Frequency of Purchases

## Preprocessing Plan

- Perform Exploratory Data Analysis (EDA)
- Remove duplicate records
- Handle missing values
- Label Encode categorical variables
- Drop non-informative columns (Customer ID)
- Split the dataset into training (80%) and testing (20%) sets

---

# 5. Algorithms I Plan to Train

## Linear Regression

A simple baseline regression algorithm that models a linear relationship between input features and the target variable.

## Decision Tree Regressor

A tree-based algorithm capable of modeling non-linear relationships by learning decision rules from the training data.

## Random Forest Regressor

An ensemble learning algorithm that combines multiple decision trees (200 estimators) for better prediction accuracy and reduced overfitting.

---

# 6. Evaluation Plan

The models will be evaluated using:

- **Mean Absolute Error (MAE)** — average prediction error in USD
- **Root Mean Squared Error (RMSE)** — penalizes larger errors more heavily
- **R² Score** — measures the proportion of variance explained by the model

The best model will be selected based on the lowest MAE and RMSE, and the highest R² Score.

---

# 7. Deployment Sketch

## Frontend

A responsive web dashboard built using:
- HTML5
- CSS3 (Glassmorphism design, Dark/Light Mode)
- Vanilla JavaScript (Fetch API, LocalStorage for prediction history)

Features include a 17-field customer prediction form, animated result card, statistics panel, and prediction history.

## Backend

**FastAPI** — Python web framework for building REST APIs

- Swagger Documentation: `http://127.0.0.1:8002/docs`
- CORS enabled for cross-origin requests from the frontend

## API Endpoint

### Prediction Endpoint

```
POST /predict
```

### Full Example Input (17 fields)

```json
{
  "Age": 28,
  "Gender": 1,
  "Item_Purchased": 15,
  "Category": 2,
  "Location": 5,
  "Size": 1,
  "Color": 3,
  "Season": 2,
  "Review_Rating": 4.5,
  "Subscription_Status": 1,
  "Payment_Method": 2,
  "Shipping_Type": 1,
  "Discount_Applied": 0,
  "Promo_Code_Used": 0,
  "Previous_Purchases": 12,
  "Preferred_Payment_Method": 2,
  "Frequency_of_Purchases": 3
}
```

### Example Output

```json
{
  "Predicted Purchase Amount": 148.72
}
```

---

# 8. Repository Structure

```text
ds-ml-bootcamps/
│
├── dataset/
│   ├── shopping_trends.csv          ← original raw dataset
│   └── clean_shopping_data.csv      ← preprocessed dataset
│
├── steps/
│   ├── 01_data_exploration.ipynb    ← EDA notebook
│   ├── 02_processing.ipynb          ← Preprocessing notebook
│   └── 03_model_training.ipynb      ← Model training & evaluation
│
├── api/
│   └── app.py                       ← FastAPI application
│
├── frontend/
│   ├── index.html                   ← Dashboard UI
│   ├── style.css                    ← Styling
│   └── script.js                    ← API integration & logic
│
├── models/
│   ├── random_forest_model.pkl      ← Trained model
│   └── feature_columns.pkl          ← Feature column list
│
├── build_working_model.py           ← Model training script
├── requirements.txt
├── .gitignore
└── README.md
```

## Run Commands

```bash
# Train model
python build_working_model.py

# Start API server
uvicorn api.app:app --port 8002 --reload

# Serve frontend
python -m http.server 3000
```
