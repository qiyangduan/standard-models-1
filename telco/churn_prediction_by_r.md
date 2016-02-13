# Churn Prediction by R
As we summarized before in [What Makes a Model](../what_makes_a_model.md), whenever we want to create a ready-to-integrate model, we have to make sure that the model can survive in real life complex environment. Though R is an excellent data exploring platform, constructing business app might be a little bit difficult. Based on many existing materials on Internet, I took a first shot. I will go through those steps to present my result:

|  Functions |  Script Files |
| -- | -- |
|  A very simple training and predicting program using Decision Tree (rpart) |  [churn_dt_rpart.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_dt_rpart.r) |
| 0:3 | 1:3 |
| 0:4 | 1:4 |
| 0:5 | 1:5 |

* . The result is 
* Implement same model by Random Forest and add model persistence capabilities. The result is (churn_dt_rpart.r](
* Adding RESTful web interface. 
* It should be able to adjust itself according to the new data. This is could be ideally done by incremental model updating or a full retraing over new datasets. 
* 

You can download from github to run them.

