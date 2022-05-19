# Credit-risk-modeling

## Overview
* Creating Scorecard and estimating Expected Lost inspired by 365 Data Science
* Data: Lending Club Loan Data from 2007 - 2018 
* Model: Linear and Logistic Regression
* Expected Lost (EL) = Probability of Default (PD) x Lost Given Default (LGD) x Exposure At Default (EAD)

## Data preparation
**Independent variable:** grade; home_ownership; addr_state; vertification_status; purpose; initial_list_status; term; emp_length; mths_since_issue_d; int_rate; mths_since_earliest_cr_line; delinq_2yrs; inq_last_6mths; open_acc; pub_rec; total_acc; acc_now_delinq; total_rev_hi_lim; annual_inc; mths_since_last_delinq; mths_since_last_record. 

## PD model
### Model
Split data 80:20, random_state : 42

* Logistic Regression

roc_auc_score: 74.1 

![alt text](https://github.com/DamHTran/Credit-risk-modeling/blob/master/Images/Picture_1.jpg)

Kolmogorov-Smirnov:35.5

![alt text](https://github.com/DamHTran/Credit-risk-modeling/blob/master/Images/picture_2.jpg)
### Applying model
Creating Scorecard 

## LGD Model
Split data 80:20, random_state : 42
recovery rate = recoveries/funded_amnt
### Stage 1: check whether recovery rate is 0 or greater
* Logistic Regression

roc_auc_score: 66.5 

![alt text](https://github.com/DamHTran/Credit-risk-modeling/blob/master/Images/picture_3.jpg)
### Stage 2: if recovery rate is greater than 0, how much greater?
* Linear Regression

![alt text](https://github.com/DamHTran/Credit-risk-modeling/blob/master/Images/picture_4.jpg)
### Combining 2 stages
LGD = lgd_stage_1 x lgd_stage_2

## EAD Model
Split data 80:20, random_state : 42
Credit conversion factor (CCF) = (funded_amnt - total_rec_prncp)/funded_amnt
EAD = CCF * funded_amnt

* Linear Regression

![alt text](https://github.com/DamHTran/Credit-risk-modeling/blob/master/Images/picture_5.jpg)

## Expected Loss (EL)
EL = PD x LGD x EAD

EL/funded_amnt = 0.08
