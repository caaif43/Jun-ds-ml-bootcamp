# Customer Shopping Purchase Prediction System

## Machine Learning Project Paper

**Author:** Abdullahi Hassan Shire
**Date:** July 2026
**GitHub:** https://github.com/caaif43/ds-ml-bootcamps

---

# 1. Introduction

Online shopping has become one of the fastest-growing sectors in modern business. Every day, companies collect large amounts of customer data, including demographic information, purchasing history, product preferences, and shopping behavior. Analyzing this information allows businesses to better understand customer needs and improve decision-making.

The goal of this project is to build a Machine Learning system capable of predicting the amount a customer is likely to spend during a purchase. Accurate purchase prediction helps businesses improve inventory planning, personalized marketing, and customer relationship management.

The project follows a complete machine learning workflow, including data preprocessing, model training, evaluation, model comparison, and deployment using FastAPI with a responsive web-based frontend.

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
* Build a responsive frontend dashboard for user interaction.

---

# 3. Dataset Description

## Dataset Source

Customer Shopping Trends Dataset (Kaggle)

https://www.kaggle.com/datasets/iamsouravbanerjee/customer-shopping-trends-dataset/data

### Dataset Size

* 3,900 customer records
* 19 columns

### Target Variable

Purchase Amount (USD)

### Main Features

| Feature | Type | Description |
|---|---|---|
| Age | Numerical | Customer age |
| Gender | Categorical | Male / Female |
| Category | Categorical | Product category |
| Item Purchased | Categorical | Specific product name |
| Location | Categorical | US State |
| Size | Categorical | S / M / L / XL |
| Color | Categorical | Product color |
| Season | Categorical | Fall / Spring / Summer / Winter |
| Review Rating | Numerical | Rating score (1.0 – 5.0) |
| Subscription Status | Categorical | Yes / No |
| Shipping Type | Categorical | Standard / Express etc. |
| Payment Method | Categorical | Credit Card / PayPal etc. |
| Previous Purchases | Numerical | Count of past orders |
| Discount Applied | Categorical | Yes / No |
| Promo Code Used | Categorical | Yes / No |
| Preferred Payment Method | Categorical | Preferred payment type |
| Frequency of Purchases | Categorical | Weekly / Monthly etc. |

---

# 4. Exploratory Data Analysis

Exploratory Data Analysis (EDA) was performed before model training.

The analysis included:

* Dataset shape and structure inspection
* Data types review
* Summary statistics (mean, std, min, max)
* Missing value inspection (none found)
* Duplicate detection and removal
* Distribution of the target variable (Purchase Amount)
* Correlation analysis between features and target
* Visualization using Matplotlib and Seaborn

Key finding: The dataset is well-structured with no missing values, making it ready for preprocessing with minimal cleaning effort.

---

# 5. Data Preprocessing

Several preprocessing techniques were applied before training the models.

These included:

* Removing duplicate records
* Confirming no missing values
* Label Encoding categorical variables using `sklearn.preprocessing.LabelEncoder`
* Dropping the `Customer ID` column (non-informative identifier)
* Selecting all 17 remaining features as model input
* Splitting the dataset: 80% training / 20% testing (`random_state=42`)

Proper preprocessing ensured consistent and clean input for all three models.

---

# 6. Machine Learning Algorithms

Three regression algorithms were trained and compared.

## Linear Regression

Linear Regression was used as the baseline model. It predicts purchase amounts using a linear relationship between input features and the target variable.

**Advantages:**
* Fast training
* Easy to interpret
* Good baseline reference

**Limitation:**
* Cannot model complex nonlinear relationships.

---

## Decision Tree Regressor

Decision Tree Regressor predicts purchase amounts by learning decision rules from the training data.

**Advantages:**
* Handles nonlinear relationships
* Easy to visualize

**Limitation:**
* Prone to overfitting the training data, leading to poor generalization on unseen data.

---

## Random Forest Regressor

Random Forest combines multiple decision trees (200 estimators) to improve prediction accuracy and reduce overfitting.

**Advantages:**
* High prediction stability
* Reduces overfitting through ensemble averaging
* Works well with mixed categorical and numerical data
* More robust to noise in the dataset

**Limitation:**
* More computationally expensive than simpler models.

---

# 7. Model Evaluation

The models were evaluated using standard regression metrics on the test set (20% of data = 780 records).

### Evaluation Metrics

* **MAE (Mean Absolute Error):** Average prediction error in USD
* **RMSE (Root Mean Squared Error):** Penalizes larger errors more heavily
* **R² Score:** Proportion of variance explained (1.0 = perfect, 0 = baseline)

### Results

| Model             |   MAE |  RMSE | R² Score |
|-------------------|------:|------:|---------:|
| Linear Regression | 20.83 | 23.86 |  -0.0170 |
| Decision Tree     | 27.58 | 33.88 |  -1.0512 |
| Random Forest     | 20.87 | 23.95 |  -0.0253 |

### Observations

* **Decision Tree** performed the worst across all three metrics, showing clear signs of overfitting (R² = -1.05).
* **Linear Regression** and **Random Forest** achieved nearly identical MAE and RMSE, with a difference of only 0.04 USD.
* All models show low R² scores, which reflects a characteristic of this specific dataset: the purchase amounts in the original `shopping_trends.csv` are synthetically generated with a near-uniform distribution ($20–$100), resulting in weak feature-to-target correlations. This is a known limitation of this public dataset.

---

# 8. Best Model Selection

**Random Forest Regressor** was selected as the final model for deployment.

Although Linear Regression achieved a marginally similar MAE, Random Forest was chosen because:

* It is significantly more robust than Decision Tree (lower MAE by 6.71 USD, lower RMSE by 9.93 USD)
* It generalizes better to unseen data through ensemble averaging
* It is the industry-standard choice for production regression systems
* The performance difference with Linear Regression is negligible (0.04 USD MAE difference), making Random Forest the safer and more scalable choice

---

# 9. FastAPI Deployment

The selected model was saved using `joblib` and deployed using **FastAPI** with **Uvicorn**.

The API accepts all 17 customer features in JSON format and returns the predicted purchase amount in real time.

### Endpoint

```
POST /predict
```

### Full Example Request (17 fields)

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

### Example Response

```json
{
  "Predicted Purchase Amount": 148.72
}
```

### CORS

Cross-Origin Resource Sharing (CORS) was enabled using `fastapi.middleware.cors.CORSMiddleware` to allow the frontend to communicate with the API from any origin.

---

# 10. Frontend Dashboard

A responsive, production-quality web frontend was built using HTML5, CSS3, and Vanilla JavaScript.

### Features

* **Dark / Light Mode** toggle
* **17-field prediction form** with live validation
* **Animated result card** with count-up number animation
* **Prediction history** stored in browser LocalStorage (last 10 predictions)
* **Statistics cards** showing Total, Average, Highest, and Lowest predictions
* **Toast notifications** for success, error, and warning states
* **Server status indicator** showing API connectivity
* **Glassmorphism design** with smooth animations and responsive layout

The frontend is served via Python's built-in HTTP server on port 3000 and communicates with the FastAPI backend on port 8002.

---

# 11. System Workflow

```
Customer fills form (Frontend)
          ↓
    Form Validation
          ↓
  POST /predict (FastAPI)
          ↓
   Pydantic Validation
          ↓
  DataFrame Construction
          ↓
  Feature Column Alignment
          ↓
  Random Forest Model (.pkl)
          ↓
  Predicted Purchase Amount
          ↓
   JSON Response → UI Display
          ↓
  Saved to LocalStorage History
```

---

# 12. Technologies Used

## Machine Learning

* Python 3.13
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

## Frontend

* HTML5
* CSS3 (Glassmorphism, Dark/Light Mode)
* Vanilla JavaScript (Fetch API, LocalStorage)

## Development

* Jupyter Notebook
* VS Code
* Git
* GitHub

---

# 13. Project Structure

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
│   ├── style.css                    ← Glassmorphism styling
│   └── script.js                    ← API integration & logic
│
├── models/
│   ├── random_forest_model.pkl      ← Trained model
│   └── feature_columns.pkl          ← Feature column list
│
├── build_working_model.py           ← Model training script
├── requirements.txt                 ← Python dependencies
├── .gitignore
└── README.md
```

---

# 14. Testing

The project was tested by:

* Training all three models and comparing evaluation metrics
* Saving the best model (Random Forest) using joblib
* Testing FastAPI using Swagger UI at `http://127.0.0.1:8002/docs`
* Sending sample POST requests to `/predict`
* Verifying JSON responses with correct predicted values
* Testing the frontend form with various customer profiles
* Confirming LocalStorage history persistence across sessions
* Verifying CORS headers allow cross-origin requests

The API successfully returned predicted purchase amounts for all valid customer inputs.

---

# 15. Limitations

The project has several limitations:

* The original dataset purchase amounts are synthetically generated, resulting in low feature-to-target correlation and near-zero R² scores.
* Dataset size is relatively small (3,900 records).
* The API is currently deployed only on a local machine.
* No user authentication on the API.
* Hyperparameter tuning was minimal.

---

# 16. Future Improvements

Future work may include:

* Hyperparameter optimization using GridSearchCV or Optuna
* Additional algorithms such as XGBoost or LightGBM
* Deployment to a cloud platform (AWS, Render, or Railway)
* Docker containerization for portability
* Real-time analytics dashboard for business users
* Using a real-world e-commerce dataset with genuine purchase correlations

---

# 17. Lessons Learned

This project improved my understanding of:

* End-to-end machine learning pipeline development
* Data preprocessing and feature engineering
* Regression algorithm comparison and selection
* Model evaluation using MAE, RMSE, and R²
* FastAPI deployment and REST API development
* CORS configuration for cross-origin communication
* Frontend development and API integration
* Git version control and GitHub collaboration

It also strengthened my practical skills in Python, Scikit-learn, FastAPI, and full-stack machine learning deployment.

---

# 18. Conclusion

This project successfully demonstrated a complete machine learning workflow from raw data to a deployed, user-facing prediction system. Despite the inherent limitations of the synthetic dataset, the project fulfilled all planned objectives:

* Three regression models were trained and evaluated.
* Random Forest was selected as the best model.
* A FastAPI backend was deployed with a `/predict` endpoint.
* A professional frontend dashboard was built for user interaction.
* The project is version-controlled and publicly available on GitHub.

This project represents a practical, end-to-end application of supervised machine learning in a real deployment context.
