# Credit-risk-modeling

## Overview
* Creating Scorecard and estimating Expected Lost with main instruction from 365 Data Science's courses
* Data: Lending Group Loan Data from 2007 - 2018 
* Credit Score: 350-800
* Expected Lost (EL) = Probability of Default (PD) x Lost Given Default (LGD) x Exposure At Default (EAD)

## Data preparation
**Independent variable:** grade; home_ownership; addr_state; vertification_status; purpose; initial_list_status; term; emp_length; mths_since_issue_d; int_rate; mths_since_earliest_cr_line; delinq_2yrs; inq_last_6mths; open_acc; pub_rec; total_acc; acc_now_delinq; total_rev_hi_lim; annual_inc; mths_since_last_delinq; mths_since_last_record. 

## PD model
### Model
Split data 80:20, random_state : 42
* Logistic Regression
roc_auc_score: 74.1 
Picture 1
Kolmogorov-Smirnov:35.5
Picture 2
### Applying model
Creating Scorecard 

## LGD Model
Split data 80:20, random_state : 42
recovery rate = recoveries/funded_amnt
### Stage 1: check whether recovery rate is 0 or greater
* Logistic Regression
roc_auc_score: 66.5 
Picture 3
### Stage 2: if recovery rate is greater than 0, how much greater?
* Linear Regression
picture 4
### Combining 2 stages
LGD = lgd_stage_1 x lgd_stage_2

## EAD Model
Split data 80:20, random_state : 42
Credit conversion factor (CCF) = (funded_amnt - total_rec_prncp)/funded_amnt
EAD = CCF * funded_amnt
* Linear Regression
picture 5

## Expected Loss (EL)
EL = PD x LGD x EAD
EL/funded_amnt = 0.08
