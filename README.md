# Forecasting-Mini-Course-Sales

[Forecasting Mini-Course Sales](https://www.kaggle.com/competitions/playground-series-s3e19/)

---
### About the Competition
- **Task:** Predict sales numbers by country by store by product for the year of 2022. There are 5 countries, 3 stores and 5 products. Therefore, the task is to predict predict sales for year 2022 (365 days) for 75 distinct country-store-product combinations.
- **Eval Metric:** According the competition host at Kaggle, "Submissions are evaluated on SMAPE between forecasts and actual values." 

---
### Modeling
**FB Prophet**
- Model 1: Prophet model wtih yearly and weekly seasonality plus holiday information for each country.
  - Results (by country):
    - Argentina    39.00
    - Canada       17.23
    - Estonia      12.24
    - Japan         6.09
    - Spain        12.48
  - Average SMAPE: 17.41
- Model 2: Smoothing the Covid year (2020) first and re-fit with the Model 1 configuration
  - Results (by country):
    - Argentina    13.40
    - Canada       17.36
    - Estonia      23.06
    - Japan         5.79
    - Spain         9.15
  - Average SMAPE: 13.75
- Model 3: Prophet model with grid search
  - 3 hyperparameters to tune:
    - `changepoint_prior_scale`
    - `seasonality_prior_scale`
    - `seasonality_mode` 
  - Results (by country):
    - Argentina    13.57
    - Canada        8.83
    - Estonia       9.20
    - Japan         4.31
    - Spain         9.48
  - Average SMAPE: 9.08

---
### Discussion
Below are things that I learned:

**Prophet**
- It is my first time using Prophet. Overall, I learnt:
  - How to fit a model with seasonality
  - How to incorporate holiday information into the model (huge plus)
  - How to train a multivariate model
  - How to do grid search with Prophet
  - How to evaluate model with `cross_validation` and `performance_metrics` functions
- In certain circumstances, training a Prophet model could be slow due to train error. The log would throw out the meassage that goes "Optimization terminated abnormally. Falling back to Newton."

**Leaderboard Probing**
- The most complicated thing with this competition is, it needs leaderboard probling since there is a data construction error by Kaggle, which is well documented in this [post](https://www.kaggle.com/competitions/playground-series-s3e19/discussion/425538). Therefore, there would be cases that my grid search model would not outperform my baseline model after introducing multipliers to the predictions. 

Things I wished I could do for improvement:
- Leaders in the competition were able to lower their SMAPES under 5 with a GLM model/Ridge Regression model. I saw they added sin and cos info based on the day of the week/month. Will implement those on my next attempt.
- Find ways to improve multivariate models.
