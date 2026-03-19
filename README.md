# 🚗 Used Car Price Prediction 
### Wings1 T15 Cloud Analytics and AI Challenge

## 📌 Project Overview
This project involves building a machine learning pipeline to predict the selling prices of used cars. [cite_start]The solution follows a structured approach from data ingestion in **AWS S3** to model training in **Amazon SageMaker**[cite: 12, 190].

---

## 🛠️ Tech Stack
* [cite_start]**Cloud Platform:** AWS (SageMaker, S3) [cite: 12, 205]
* **Language:** Python
* [cite_start]**Libraries:** Pandas, NumPy, Scikit-learn, Boto3, Joblib [cite: 222, 305]

---

## 📋 Machine Learning Workflow

### Task 1: Data Ingestion
* [cite_start]Dataset `car_cleaned_data.csv` was loaded from the S3 bucket `car-data` using `boto3`[cite: 223, 226].
* [cite_start]Data structure was explored using Pandas `head()` and `info()`[cite: 227].

### Task 2 & 3: Feature Engineering & Selection
* [cite_start]**Feature Creation**: Developed `car_age` calculated as $2024 - \text{year}$[cite: 232, 236].
* [cite_start]**Dropping Columns**: Removed `car name` and `year` as they were non-predictive[cite: 234].
* [cite_start]**X/y Definition**: Defined `X` by dropping `selling_price` and set `y` as the target variable[cite: 239, 240].

### Task 4 & 5: Preprocessing Pipeline
* [cite_start]**Log Transformation**: Applied `np.log1p()` to `km_driven` and `selling_price` to handle data skewness[cite: 244, 249].
* **Scaling & Encoding**: 
    * [cite_start]`StandardScaler` for numerical features (`km_driven`, `car_age`)[cite: 246].
    * [cite_start]`OneHotEncoder` for categorical features (`fuel`, `seller_type`, `transmission`, `owner`)[cite: 247].
* [cite_start]**ColumnTransformer**: Integrated transformations into a unified `preprocessor`[cite: 254, 256].

### Task 6: Model Pipeline
* [cite_start]Created a Scikit-learn `Pipeline` combining the `preprocessor` and `RandomForestRegressor`[cite: 266, 271].
* [cite_start]Set `random_state=8` for reproducibility[cite: 266].

### Task 7 & 8: Hyperparameter Tuning
* [cite_start]Performed `GridSearchCV` with **5-fold cross-validation** and **R2 scoring**[cite: 276, 278].
* **Best Parameters Found**:
    * `max_depth`: 10
    * `min_samples_split`: 2
    * `n_estimators`: 300

### Task 9 & 10: Evaluation
* [cite_start]Predictions were converted back to original currency scale using `np.expm1()`[cite: 295, 297].
* **Final Metrics**:
    * **R-squared**: 0.5489
    * [cite_start]**Mean Squared Error (MSE)**: 181,010,442,157.31 [cite: 300]

### Task 11: Cloud Deployment
* [cite_start]Serialized the model using `joblib`[cite: 305, 312].
* [cite_start]Uploaded `grid_search.pkl` to the `car-data` S3 bucket for model persistence[cite: 308, 309].

---

## 🚀 How to Run
1. Ensure AWS credentials are configured.
2. [cite_start]Run the SageMaker notebook instance `car-prediction-notebook`[cite: 212].
3. Execute the cells to process data and train the model.
4. [cite_start]Check the S3 bucket for the saved `.pkl` file[cite: 309].
