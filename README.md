# CS3244 - Prediction of Good & Bad Credit Records

## Overview of Problem

This project aims to analyse and predict creditworthiness by exploring credit records, performing feature engineering, and comparing the performance of various machine learning models.

Using credit score to determine approval for applications are a common risk control method in the financial industry.

It is important for financial institutions like banks to be able to approve applicants who will use the credit cards responsibly and are capable of repaying any loans. 

More information about the project is found in CS3244_Project.pdf.

## Problem Statement
The goal of this project is to identify the key features that influence credit score records for credit card approval in financial institutions.

## Key Questions:

1) At what point does inactivity count as ghosting for credit card companies?
2) How do their assets (car, property, etc.) determine their credit score records?
3) Which feature is the most important/has the highest correlation to a good credit score?

## Datasets

The dataset consists of two tables, `application_record` and `credit_record`, connected by the feature `ID`.

### `credit_record.csv`

The purpose of this dataset is to act as the target variable for our models. 
It contains three columns, `ID`, `MONTHS_BALANCE` and `STATUS`.

- `ID`: Represents the client number.
- `MONTHS_BALANCE`: Represents the record month, with 0 being the current month, -1 being the previous month, and so on.
- `STATUS`: Represents the status of the client’s loan repayment for that month:
  - `X`: No loans taken
  - `C`: Loan paid off
  - `0-5`: Number of months the loan is overdue

### `application_record.csv`

This dataset contains 18 features:

- `ID` (Primary Key)
- Personal Information: `code_gender`, `days_birth`
- Income & Employment: `name_income_type`, `occupation_type`, `amt_income_total`, `days_employed`, `flag_own_car`
- Education & Family: `name_education_type`, `name_fam_status`, `cnt_fam_member`, `cnt_children`
- Housing: `name_housing_type`, `flag_own_realty`
- Communication: `flag_mobil`, `flag_work_phone`, `flag_phone`, `flag_email`

## Feature Engineering 

Four new features were created:
1. Account Length: Sum of `months_balance` minus one.
2. X_Percentage: Percentage of months with `X` status (no loans taken).
3. C_Percentage: Percentage of months with `C` status (loan paid off).
4. Avg Months Overdue: Average number of months overdue, calculated by filtering rows where `STATUS` is a numerical value.

We determine a bad credit record as one where the client has never paid off a loan and the `Avg Months Overdue` is greater than the 95th percentile. This results in an unbalanced dataset.

## Models

We compared the performance of the following models:

- Logistic Regression
- Neural Network
- Random Forest

## Metrics

To evaluate the models, we used the following metrics:

- Accuracy
- F1 Score
- Precision-Recall Curve

## Results

### Without Rebalancing of Training Data

#### Accuracy 
The logistic regression model and the neural network model obtained an accuracy of 97.5%. The random forest model obtained a slightly higher accuracy of 97.7%.

#### Confusion Matrix
The logistic regression model and the neural network predicts no bad labels, while the random forest model predicts only a total of 39 bad labels.

#### F1 Score
The seemingly flawless recall and the remarkably high precision have led to an outstanding F1 score of 0.988, a result that appears too good to be true. 

These results raises a cautionary flag, prompting us to scrutinize the reliability of our model’s performance, especially given the imbalanced nature of the dataset. 

### With Rebalancing of Training Data

#### Rebalancing Method: 
Oversampling was used as the data preprocessing method to handle imbalanced classes. This approach outperformed undersampling, which resulted in the loss of significant information due to the severe class imbalance (from 28,000 to about 600 samples).

#### Model Performance: 
The Random Forest classifier was more accurate than the Logistic Regression model when using oversampling.

## Additional Notes

This project highlights the challenges of working with imbalanced datasets and the importance of careful evaluation of model performance, especially when the results seem "too good to be true." Further improvements and refinements can be made through techniques such as ensemble methods, hyperparameter tuning, and cross-validation.

