# Churn Prediction by R
As we summarized before in [What Makes a Model](../what_makes_a_model.md), whenever we want to create a ready-to-integrate model, we have to make sure that the model can survive in real life complex environment. Though R is an excellent data exploring platform, constructing business app might be a little bit difficult. Based on many existing materials on Internet, I took a first shot. I will go through those steps to present my result:

|  Functions |  Script File Name |
| -- | -- |
|  A very simple training and predicting program using Decision Tree (rpart) |  [churn_dt_rpart.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_dt_rpart.r) |
| Implement same model by Random Forest and add model persistence capabilities | [churn_rf_ranger.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_rf_ranger.r)|
| Adding RESTful web interface over saved the model from [churn_rf_ranger.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_rf_ranger.r).  | [churn_rf_rook_json.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_rf_rook_json.r)|

You can download all those scripts from github repository [r_sample_programs](https://github.com/qiyangduan/r_sample_programs) for your testing. Once you get into the repository, click "Download ZIP" button to download all files.
The files in [churn/data](https://github.com/qiyangduan/r_sample_programs/tree/master/churn/data) folder are the data files used by the scripts.


# Very simple Decision Tree to Start With

We will first implement the basic function by a commonly used algorithm CART. CART and C4.5 are the two most widely used Decision Tree algorithms. In 2006, ICDM (by Xindong Wu et. al) listed [Top 10 algorithms in data mining](http://www.cs.uvm.edu/~icdm/algorithms/10Algorithms-08.pdf). C4.5 might be a bit better. However maybe because of patent issue, CART seems more popular in R world. So I chose CART for this simple test.

I use Caret package in this test. It wrapped up [many packages](http://topepo.github.io/caret/modelList.html) and created a unified interface. This is really useful for R users, because each model in R is implemented with very different APIs and user interfaces. 
Without this unification, the data scientists have memorize all different API. I guess this inconvenience drove some of the R users to the Python side. Scikit-learn, for example, have very clean and consistent API (fit, predict, transform) for all algorithms. We will see that in the Python Churn model chapter.

To run the program ([churn_dt_rpart.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_dt_rpart.r)), you first change file locations to your downloaded files:

```r
apply_file = "C:\\qduan\\Stanmo\\git\\bitbucket\\src\\stanmo_website_proj\\app\\static\\data\\churn_sample_apply.csv"
train_file = "C:\\qduan\\Stanmo\\git\\bitbucket\\src\\stanmo_website_proj\\app\\static\\data\\churn_sample_input.csv"
```

Then the first step is to read in the files and do some quick transformation. The loaded data train_data contains over 400 rows. In the original data, 1 stands for Churner and 0 stands for non-churner. 

```r
churn_data = read.csv(train_file, fill = TRUE) # 1 column
# Convert 1/0 to T/F since Caret do regression instead of classification over numerical values
churn_data[churn_data$X_churn_flag == 1,]$X_churn_flag = "T"
churn_data[churn_data$X_churn_flag == 0,]$X_churn_flag = "F"
# drop customer id column, because it is the unique ID and should not be treated as a feature
drops <- c("X_customer_id")
train_data=churn_data[,!(names(churn_data) %in% drops)]


\> head(train_data,3)
  X_state_code X_tenure_days X_zip_code X_international_roaming_flag
1           KS           128        415                           no
2           OH           107        415                           no
3           NJ           137        415                           ```

Traing the model in R is as simple as a single line. I believe this is why R is so loved by most of statisticians.  This model will later be saved onto the disk for future prediction usage. 

```r
churn_model <- train(X_churn_flag~., method="rpart",data=train_data) 
```
We then load from another group of customer profiles with only 50 rows for testing. The variable apply.predicted will contain the prediction churn result. This can be offloaded as csv file for further processing.

As you may see, the accuracy is quite disappointing. Only about 12.5% accuracy.

```r
apply.predicted<-predict(churn_model,newdata=apply_data)
> table(apply.predicted,apply_data$X_churn_flag)
apply.predicted  F  T
              F 41  7
              T  0  1
              
```

# Using Random Forest for Reconstruction

In 
