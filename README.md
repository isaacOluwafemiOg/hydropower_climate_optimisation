# IBM SkillsBuild Hydropower Climate Optimisation Challenge

This repository contains the code and methodology used for the **IBM SkillsBuild Hydropower Climate Optimisation Challenge** 9th place submission with and RMSE score of 
4.650396507 on the private leaderboard.

The notebook, [`ibm_skillsbuild_9th.ipynb`](./ibm_skillsbuild_9th.ipynb), handles data preprocessing, model training, and forecasting of daily energy consumption (in kWh) for selected consumer devices.

---

## 🔍 Methodology

The modeling approach involves two stages:

1. **Classification**: A model predicts whether daily energy consumption is zero or non-zero.
2. **Regression**: A separate model forecasts the amount of energy consumed when it's non-zero.

---

## ⚙️ Running the Notebook

To run the notebook successfully, ensure the following variables are set to appropriate file paths:

- `TRAIN_DATA_PATH`: Path to the training data CSV file.
- `SAMPLE_SUBMISSION_PATH`: Path to the sample submission CSV file.

The above train data and sample submission files can be found on the competition page: https://zindi.africa/competitions/ibm-skillsbuild-hydropower-climate-optimisation-challenge/data

The code is written in Python and runs on a CPU runtime in under **25 minutes**.

---

## 📘 Notebook Overview

### 1. Importing Libraries
The following libraries are used:

- `pandas==2.2.3`
- `numpy==1.26.4`
- `scikit-learn==1.2.2`
- `xgboost==2.0.3`
- `scipy==1.15.2`

---

### 2. Reading and Preprocessing Data

- Dropped irrelevant columns such as `'consumer_device_9'` and `'consumer_device_x'`.
- Filtered out instances of consumer devices not present in the test data to optimize computation and model relevance.

---

### 3. Feature Engineering

- Extracted datetime features: **year**, **quarter**, and **month**.
- Aggregated intraday data into **daily energy consumption**.
- Included **14-day historical energy consumption** values.
- Computed statistics on historical values such as **mean**, **minimum**, and **trend coefficient**.

---

### 4. Model Development and Training

- **Classifier**: XGBoost model to detect zero consumption days.
- **Regressor**: XGBoost model to predict non-zero consumption values.
- Feature subsets for each model are defined using `sel_ind_cl` and `sel_ind_reg`.

#### Evaluation Metrics:

- **Classifier**: Stratified 5-fold cross-validation using **F1 score**.
  - **F1 Score**: `0.968`
- **Regressor**: 5-fold cross-validation using **Root Mean Squared Error (RMSE)**.
  - **RMSE**: `3.795`

---

### 5. Prediction and Submission

- Performed **autoregressive forecasting** for 31 days beyond the last training date.
- Applied the same preprocessing and feature engineering steps as in training.
- Predictions were made using:
  - Classifier → determines zero or non-zero consumption.
  - Regressor → predicts actual values for non-zero instances.
- Combined results and saved as:  
  **`ibm_skillsbuild_9th.csv`** in the working directory.

---

## 📁 Output

- `ibm_skillsbuild_9th.csv`: Final predictions file.


