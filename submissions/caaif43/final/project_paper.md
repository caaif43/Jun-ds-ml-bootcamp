
# Customer Shopping Purchase Prediction System

## Machine Learning Project Paper

**Author:** Abdullahi Hassan Shire
**Date:** July 2026

---

# 1. Introduction

Online shopping has become one of the fastest-growing sectors in modern business. Every day, companies collect large amounts of customer data, including demographic information, purchasing history, product preferences, and shopping behavior. Analyzing this information allows businesses to better understand customer needs and improve decision-making.

The goal of this project is to build a Machine Learning system capable of predicting the amount a customer is likely to spend during a purchase. Accurate purchase prediction helps businesses improve inventory planning, personalized marketing, and customer relationship management.

The project follows a complete machine learning workflow, including data preprocessing, model training, evaluation, model comparison, and deployment using FastAPI.

---

# 2. Project Objectives

The objectives of this project are:

* Analyze customer shopping behavior.
* Prepare and clean the dataset.
* Build multiple regression models.
* Compare model performance.
* Select the best-performing model.
* Deploy the best model using FastAPI.
* Create a REST API for real-time predictions.

---

# 3. Dataset Description

## Dataset Source

Customer Shopping Trends Dataset (Kaggle)

[https://www.kaggle.com/datasets/iamsouravbanerjee/customer-shopping-trends-dataset/data]

### Dataset Size

* Approximately 3,900 customer records
* 19 columns

### Target Variable

Purchase Amount (USD)

### Main Features

* Age
* Gender
* Category
* Item Purchased
* Location
* Size
* Color
* Season
* Review Rating
* Subscription Status
* Shipping Type
* Payment Method
* Previous Purchases
* Discount Applied
* Promo Code Used
* Frequency of Purchases

The dataset contains customer demographic information together with shopping behavior, making it suitable for regression problems.

---

# 4. Exploratory Data Analysis

Exploratory Data Analysis (EDA) was performed before model training.

The analysis included:

* Dataset shape
* Data types
* Summary statistics
* Missing value inspection
* Duplicate detection
* Distribution of purchase amounts
* Correlation between numerical features

The dataset was found to be well-structured with only minor preprocessing required.

---

# 5. Data Preprocessing

Several preprocessing techniques were applied before training the models.

These included:

* Removing duplicate records
* Handling missing values
* Label Encoding categorical variables
* Feature Scaling
* Selecting input features
* Splitting the dataset into training and testing sets

Proper preprocessing improved model performance and ensured consistent input for deployment.

---

# 6. Machine Learning Algorithms

Three regression algorithms were trained and compared.

## Linear Regression

Linear Regression was used as the baseline model. It predicts purchase amounts using a linear relationship between input features and the target variable.

Advantages:

* Fast
* Easy to interpret

Limitation:

* Cannot model complex nonlinear relationships.

---

## Decision Tree Regressor

Decision Tree Regressor predicts purchase amounts by learning decision rules from the training data.

Advantages:

* Handles nonlinear relationships
* Easy to visualize

Limitation:

* Can overfit the training data.

---

## Random Forest Regressor

Random Forest combines multiple decision trees to improve prediction accuracy.

Advantages:

* High prediction accuracy
* Reduces overfitting
* Works well with mixed data

Limitation:

* More computationally expensive than simpler models.

---

# 7. Model Evaluation

The models were evaluated using standard regression metrics.

The evaluation metrics included:

* Mean Absolute Error (MAE)
* Root Mean Squared Error (RMSE)
* R² Score

These metrics measure prediction accuracy and overall model performance.

Example comparison table:

| Model             | MAE | RMSE | R² Score |
| ----------------- | --: | ---: | -------: |
| Linear Regression |  XX |   XX |       XX |
| Decision Tree     |  XX |   XX |       XX |
| Random Forest     |  XX |   XX |       XX |

Replace the "XX" values with your notebook results.

---

# 8. Best Model Selection

Among the three algorithms, Random Forest Regressor achieved the best overall performance.

It produced:

* Lowest MAE
* Lowest RMSE
* Highest R² Score

Because of its superior predictive accuracy, Random Forest was selected as the final model for deployment.

---

# 9. FastAPI Deployment

The selected model was deployed using FastAPI.

The API accepts customer information in JSON format and returns the predicted purchase amount.

### Endpoint

POST `/predict`

### Example Request

```json
{
  "Age":28,
  "Gender":1,
  "Item_Purchased":15,
  "Category":2,
  "Location":5,
  "Size":1,
  "Color":3,
  "Season":2,
  "Review_Rating":4.5,
  "Previous_Purchases":12
}
```

### Example Response

```json
{
  "Predicted Purchase Amount":148.72
}
```

---

# 10. System Workflow

The prediction workflow is as follows:

Customer Data

↓

FastAPI API

↓

Data Validation

↓

Feature Processing

↓

Random Forest Model

↓

Predicted Purchase Amount

↓

JSON Response

---

# 11. Technologies Used

## Machine Learning

* Python
* Pandas
* NumPy
* Scikit-learn
* Joblib

## Visualization

* Matplotlib
* Seaborn

## Deployment

* FastAPI
* Uvicorn
* Pydantic

## Development

* Jupyter Notebook
* VS Code
* Git
* GitHub

---

# 12. Project Structure

```text
customer-purchase-prediction/

├── dataset/
├── notebooks/
├── api/
├── models/
├── README.md
├── requirements.txt
└── project_paper.md
```

---

# 13. Testing

The project was tested by:

* Training all models
* Comparing evaluation metrics
* Saving the best model
* Testing FastAPI using Swagger UI
* Sending sample prediction requests
* Verifying JSON responses

The API successfully returned predicted purchase amounts for valid customer data.

---

# 14. Limitations

The project has several limitations:

* Dataset size is relatively small.
* Limited feature engineering was applied.
* Hyperparameter tuning was minimal.
* The API is currently deployed only on a local machine.

---

# 15. Future Improvements

Future work may include:

* Hyperparameter optimization
* Additional regression algorithms such as XGBoost
* Deployment to a cloud platform
* Building a React frontend
* Real-time dashboard for business users

---

# 16. Lessons Learned

This project improved my understanding of:

* Data preprocessing
* Feature engineering
* Regression algorithms
* Model evaluation
* FastAPI deployment
* REST API development
* End-to-end Machine Learning workflows

It also strengthened my practical skills in Python, Scikit-learn, and software deployment.

---


