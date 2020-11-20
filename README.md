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
![alt text](https://scontent-lht6-1.xx.fbcdn.net/v/t1.0-9/126205700_3458553244260155_809034677528929086_n.jpg?_nc_cat=103&ccb=2&_nc_sid=730e14&_nc_ohc=J7T2YfNWqB4AX_MkY5C&_nc_ht=scontent-lht6-1.xx&oh=4a3138d2113b922138ed523b578ba874&oe=5FDCDCC5)
Kolmogorov-Smirnov:35.5
![alt text](https://scontent-lhr8-1.xx.fbcdn.net/v/t1.0-9/126310590_3458553237593489_4205011581836724134_n.jpg?_nc_cat=110&ccb=2&_nc_sid=730e14&_nc_ohc=qfkKMnRAQxEAX8ziPes&_nc_ht=scontent-lhr8-1.xx&oh=98e9eefcc6151f24a5ede591cae2fb43&oe=5FDD24A9)
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
