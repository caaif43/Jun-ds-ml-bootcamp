git add project_paper.md project-proposal-sample.md# Final Project Proposal

**Date:** July 2026

---

# 1. Certificate Name

**Abdullahi Hassan Shire**

---

# 2. Project Title and Description

## Title

# Customer Purchase Prediction System

## Description

This project aims to build a Machine Learning system that predicts the purchase amount of customers based on their demographic information and shopping behavior. The system helps businesses better understand customer purchasing patterns, improve marketing strategies, and support business decision-making.

The project will include data preprocessing, model training, model evaluation, and deployment using FastAPI. Users will be able to enter customer information through an API and receive a predicted purchase amount.

---

# 3. Problem Type

## Regression (Supervised Learning)

The objective is to predict the customer's purchase amount.

### Output

Purchase Amount (USD)

---

# 4. Dataset

## Source

Customer Shopping Trends Dataset (Kaggle)

https://www.kaggle.com/datasets/iamsouravbanerjee/customer-shopping-trends-dataset/data

## Dataset Size

- 3,900+ rows
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
- Encode categorical variables
- Scale numerical features
- Split the dataset into training and testing sets

---

# 5. Algorithms I Plan to Train

## Linear Regression

A simple baseline regression algorithm.

## Decision Tree Regressor

A tree-based algorithm capable of modeling non-linear relationships.

## Random Forest Regressor

An ensemble learning algorithm that combines multiple decision trees for better prediction accuracy.

---

# 6. Evaluation Plan

The models will be evaluated using:

- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- R² Score

The best model will be selected based on the highest R² Score and the lowest prediction errors (MAE and RMSE).

---

# 7. Deployment Sketch

## Frontend 

Simple HTML page or React interface.

## Backend

FastAPI

Swagger Documentation

/docs

## API Endpoint

### Prediction Endpoint

POST /predict

### Example Input

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
  "Previous_Purchases": 12
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
customer-purchase-prediction/
│
├── dataset/
│   └── shopping_trends.csv
│
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   └── 03_model_training.ipynb
│
├── api/
│   └── app.py
│
├── models/
│   ├── random_forest_model.pkl
│   └── feature_columns.pkl
│
├── README.md
├── requirements.txt
└── project_paper.md
```

## Planned Commands

```bash
python src/train.py

uvicorn api.app:app --reload
```

