# Credit-risk-modeling

## Overview
* Creating Scorecard and estimating Expected Lost inspired by 365 Data Science's courses
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

![alt text](Picture_1.jpg)

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

![alt text](https://scontent-lhr8-1.xx.fbcdn.net/v/t1.0-9/126728408_3458553240926822_7526151838200053673_n.jpg?_nc_cat=111&ccb=2&_nc_sid=730e14&_nc_ohc=vPgRqxAjYywAX-enUyS&_nc_ht=scontent-lhr8-1.xx&oh=af8ebbb58b31736a1a0fccd47373a293&oe=5FDD7264)
### Stage 2: if recovery rate is greater than 0, how much greater?
* Linear Regression

![alt text](https://scontent-lhr8-1.xx.fbcdn.net/v/t1.0-9/126468740_3458553310926815_5032070513226806318_n.jpg?_nc_cat=111&ccb=2&_nc_sid=730e14&_nc_ohc=7e9lQSfO9HsAX8HVsBn&_nc_ht=scontent-lhr8-1.xx&oh=5398cdb714a8f157ca6be560012e28bf&oe=5FDE0568)
### Combining 2 stages
LGD = lgd_stage_1 x lgd_stage_2

## EAD Model
Split data 80:20, random_state : 42
Credit conversion factor (CCF) = (funded_amnt - total_rec_prncp)/funded_amnt
EAD = CCF * funded_amnt

* Linear Regression

![alt text](https://scontent-lhr8-1.xx.fbcdn.net/v/t1.0-9/126817169_3458553314260148_2892255637931280419_n.jpg?_nc_cat=102&ccb=2&_nc_sid=730e14&_nc_ohc=0WCoGLZA9QAAX-Py0o8&_nc_ht=scontent-lhr8-1.xx&oh=9ef6eef2c2fd431a9f9c75b6d788a2a8&oe=5FDCDD40)

## Expected Loss (EL)
EL = PD x LGD x EAD

EL/funded_amnt = 0.08
