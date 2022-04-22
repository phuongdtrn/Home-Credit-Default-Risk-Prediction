# Home Credit Default Risk Prediction
Link to Kaggle competition: https://www.kaggle.com/c/home-credit-default-risk

## Background and Context
Home Credit is an international consumer finance provider, whose goal is to provide a safe experience for people who have little or no credit history. In order to create a positive borrowing experience for the customers, Home Credit utilizes a variety of data attributes to predict a customer’ ability to repay loan. However, there are still many untapped data sources that could be employed to help Home Credit better serve its customers. By having a full understanding of its data, Home Credit could guarantee that the clients’ ability to repay is not rejected and that loans are granted with principal and maturity.

## Methodology Overview
<img width="624" alt="Screen Shot 2022-04-22 at 6 02 27 PM" src="https://user-images.githubusercontent.com/77939423/164815453-0af69366-53c0-4307-988f-d19e2bbd0aa9.png">

## Field Generations
We generated some new fields to add on the existing attributes:
- Credit_overdue: Flag assigned to determine whether the applicant has had an overdue payment previously. If this has a value > 0, then there is some risk of late payments from this particular client.
- Debt_credit_ratio (total debt / total credit): For each line of client’s previous credit, if this has a value > 1, then it can serve as a flag for at-risk customers that have incurred debt well over their credit limit.
- Success_ratio (# of successful applications / # of applications): For every SK_ID_CURR, a ratio closer to 1 would signify that for the most part, this client has had successful loan applications in the past.
- Rejection_ratio (# of rejected applications / # of applications): For every SK_ID_CURR, a ratio > 0.5 would signify that this client has had more rejections than successful loan applications in the past. A higher value could be a useful feature to flag rejection of current applications.
- Avg_days_bet_rejection: Average days between each previous application rejection. A smaller value would indicate that the client has had more recent application rejections which could serve as a flag for determining that they are still not qualified for a loan.
- CreditCard Balance: Average credit card balance per SK_ID_CURR
- Credit_Card_Limit: Average credit card Limit balance per SK_ID_CURR
- Avg_vs_Min_Pay: Average payment compared to minimum required payment. This feature would indicate if, on average, the client makes payments above the established or contracted minimum payment amount.

## Model Building
We first ran individual models separately to get the best hyper-parameters using GridSearch and RandomizedSearch. After that, we implemented stacking, in which we are stacking up Logistic Regression, XGboost, Adaboost, LightGBM and RandomForest as the base estimators using the best parameters that we got from running them individually. The final estimator is taking the predictions of the previously tuned models as input, flowing through another XGBoost model in order to conduct predictions.
<img width="557" alt="Screen Shot 2022-04-22 at 6 07 35 PM" src="https://user-images.githubusercontent.com/77939423/164815837-309ae1f4-5276-41ab-8c39-3f055752d191.png">

## Results
Previously, Home credit had to go through the applications manually to identify whether a customer will be a loan defaulter or not. It was taxing, time-consuming, and also if not done correctly could lead to monetary losses for the company. The result above tells us that there is a 76.4% likelihood that our predictive model will better distinguish between the customers who are loan defaulters vs customers who are not.

Deploying this model gives Home Credit better decisive power when it comes to loan application acceptances or rejections. In line with their goal to support their clients through responsible loan grants, being able to better distinguish clients with the ability to pay will allow Home Credit to
maximize successful loan applications that will further empower underserved clients financially. Reducing unnecessary rejections will also help foster the relationship between Home Credit and their retailers by improving the overall client experience.
