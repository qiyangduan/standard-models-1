# Churn Prediction by R
As we summarized before in [What Makes a Model](../what_makes_a_model.md), whenever we want to create a ready-to-integrate model, we have to make sure that the model can survive in real life complex environment. Though R is an excellent data exploring platform, constructing business app might be a little bit difficult. Based on many existing materials on Internet, I took a first shot. I will go through those steps to present my result:

|  Functions |  Script Files |
| -- | -- |
|  A very simple training and predicting program using Decision Tree (rpart) |  [churn_dt_rpart.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_dt_rpart.r) |
| Implement same model by Random Forest and add model persistence capabilities | [churn_rf_ranger.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_rf_ranger.r)|
| Adding RESTful web interface.  | [churn_rf_rook_json.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_rf_rook_json.r)|

You can download from github to run them.
The other files in [churn](https://github.com/qiyangduan/r_sample_programs/tree/master/churn) folder are useful data files.


# Very simple Decision Tree to Start With



> head(train_data,3)
  X_state_code X_tenure_days X_zip_code X_international_roaming_flag
1           KS           128        415                           no
2           OH           107        415                           no
3           NJ           137        415                           no
