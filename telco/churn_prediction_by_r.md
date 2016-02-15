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
churn_model <- train(X_churn_flag~., method="rpart",data=train_data) ```
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

Every year KDD acquires a different kinds of dataset and present a new challenge to the data miners. It is the [KDD Cup](http://www.kdd.org/kdd-cup). In 2009, KDD presented the anonymized [customer profile from Orange](http://www.kdd.org/kdd-cup/view/kdd-cup-2009/Data) and ask participants to predict who is going to churn. This is exactly the problem we are talking about. At the end, Random Forest became the winning algorithms. Check [this](http://jmlr.csail.mit.edu/proceedings/papers/v7/niculescu09/niculescu09.pdf) for more details. In fact, most of the top 10 winners are using certain sorts of Random Forest. Since then, the Random Forest became the No.1 choice for predicting churn, and maybe for other lots of classifications as well.

To use Random Forest instead of CART, we still change this line of code:
```r
churn_model <- train(X_churn_flag~., method="rpart",data=train_data) ```

to:
```r
churn_model <- train(X_churn_flag~., method="ranger",data=train_data) 
```
All the rest of code remains exactly same, thanks to Caret package. Finally, you can see the new prediction accuracy:
```r
> table(apply.predicted,apply_data$X_churn_flag)
               
apply.predicted  F  T
              F 41  4
              T  0  4
```


You can simplly run program ([churn_rf_ranger.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_rf_ranger.r)) to see this magic.

# Adding the Web Interface
To be able to serve real time prediction request, batch prediction is not enough. In modern IT environment, RESTful API would be easist way to integrate with our existing systems. To expose meaningful RESTful api, a mini web framework is desired. 

There seems to be a few choices to integrate R models into a modern web application:
* **Shiny**: from the same company of RStudio. I did only a quick check. Shiny seems to provided a library using which you can create nice and **shiny** charts. But according [this this post](https://groups.google.com/forum/#!topic/shiny-discuss/-JYOXAeLCtI), they do not have plan to expose RESTful API for other front end to consume R models.
* [**OpenCPU**](https://www.opencpu.org/): OpenCPU seems provided a way to expose a specific R function to web using [Javascript Library](https://www.opencpu.org/jslib.html). However, this also requires client application 
* [RServe](http://www.rforge.net/Rserve/): This seems more like a bridge from other programming languages (java?) to call R functions, like [this sample program](http://www.studytrails.com/R/RServe/RServe-Java-First-Program.jsp).
* [Rook](https://cran.r-project.org/web/packages/Rook/index.html): This is a real web framework, with which we can create web serves and it runs on R environment. I also found a very useful sample program([A simple web application using Rook](http://anythingbutrbitrary.blogspot.kr/2012/12/a-simple-web-application-using-rook.html) ) as the start point.


Using Rook, we create a RESTful webservice to acception prediction request in JSON format and return R predictions in JSON again. You can run file [churn_rf_rook_json.r](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_rf_rook_json.r) to try it. 

When you execute the program(churn_rf_rook_json.r) in R console, at the end, it should automatically open a web browser showing this page:
![Initial page of R web service ](https://raw.githubusercontent.com/qiyangduan/standard-models-1/master/img/rook_r_json_init_page_1.png)

This initial page will accept the json request and post to the real API. This page will issue the HTTP POST request and display the result:

At the R console you should see those output:
```r
> R.server$start()
starting httpd help server ... done

Server started on host 127.0.0.1 and port 25046 . App urls are:

        http://127.0.0.1:25046/custom/churn_app
        http://127.0.0.1:25046/custom/churn_json
        
```        

Now **'/custom/churn_json'** is our API, and you can point your client application to this URL and post the json content.


The magic of serving R prediction to web service happens in a small function write.json_churn.HTML:
```r
write.json_churn.HTML <- function(request, response, churn_model) {
    if ("json_df" %in% names(request$POST())) {
```

The json string from file [churn_testing.json](https://github.com/qiyangduan/r_sample_programs/blob/master/churn/churn_testing.json) can be used for testing. You can simply paste the string into the text area in the inital page for testing. 


Internally, the JSON string is captured by Rook engine and passed into the function through this command:
```r
write.json_churn.HTML(request, response, churn_model)
```
In this function,  we parse the JSON string into a data frame by jsonlite package and then call the loaded model to predict the data frame. The tranined model is saved in previous two sections, and we simplely load it into the global namespace. 
```r
        dfjson = request$POST()$json_df 
        # print(dfjson)
        churn_df = fromJSON(dfjson)
        churn_df$X_churn_flag='?'
        # print(str(churn_df))
        result_df <- churn_df[c("X_customer_id")]
        
        ... ...
        
        response$write(toJSON(result_df))
        
```

At the end, you will see a result like this:
```r
[{"X_customer_id":"duan","predicted_churn_flag":"F"},{"X_customer_id":"Qiyang","predicted_churn_flag":"F"}]
```

Your client application should now parse this by your own languages and libraries and do the rest.