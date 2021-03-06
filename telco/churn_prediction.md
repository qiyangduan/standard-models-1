# Churn Prediction
Churn management seems to be an eternal business problem for most of Telecom operators.  When a subscriber terminate the current service, we call it him a churner. 

Normally we see higher churn rate for prepaid business than for postpaid business. Developing countries also observe higher churn rate than developed countries.  
According to this [blog](http://ipcarrier.blogspot.tw/2015/07/based-on-its-churn-rates-netflix-is-way.html),  even in developed countries like USA, monthly churn rate could go up to 5%. This means that each year, Sprint lose half of all its prepaid subscribers.

![Churn Stats](https://lh3.googleusercontent.com/H4kvIvyq-XldLz0jwFKYP4mbyiORZ3tOqkFplxwji1LyWAyTyaqha5LKhPzj5oGVc_G5FbeY8peZJueiMI-mf11-hCZCwPMBnjpzBjGDSefll-bSfs_bqikJIof_kIhCb3zeNmY)

Losing customer means lost of monthly subscription income. Also operators have to spend more money to win back new customers. Therefore, a good churn management solution is very important to every telecom operator.

## Business Problem
There may be minor differences of defining a churner in different operators. For example one operator may treat those prepaid subscribers who did not use the service for 3 months as already churned. Another operator may define only those who canceled services as churned. You may simply choose a definition consistent to your organization.

Those are the common reasons of churning:
* Customer is unhappy about the previous service provider
* Customer need a new handset.
* Customer is interested with competitor's promotion offer
* Contract expired

Corresponding to those different reasons, subscribers may show certain patterns before they churn:
* Customer may call service center to complain about the service.
* Customer has been using the current handset for over two years, and most users with similar model use it only for 1.5 years.
* Customer has call competitors service center hotline several times.
* Customer's contract has only 60 years left.

All those information can be extracted from either CRM customer profile or from historical usage data. We call those information the features.

With those features and a few data mining algorithms, we can actually predict who will going to churn in next a few months. Then we can take some proactive actions to prevent customer from actual churning. This is the goal of all churn management solutions. If we can predict who will churn, certain retention actions may be applied:
* Give a special discount to attract customers into a new contract with new handset. For example,  normally iphone is sold at $199 for 2 year contract. If we know that customer is looking for new handset and may churn, we can give 15% discount and sell only for $169 for 2 years contract. 
* Pre-deposit and big bonus for exchange of 2 years commitment. We can also launch targeted promotion to only those potential churners, in which if they pre-deposit $100 they can get additional $100 in their account. Meanwhile customer must commit to another 1 or 2 years subscription.
* Give certain low-cost services for free, like email service, ring back tones (RBT), musci, video acess, etc.


All those said, the most important step is how to predict who is going to churn. 

## Related Work
Before diving into our solution, let's take a look what's out there. You may find it odd enough that given such a long-standing problem and standard techniques of solving it, no good enough  application has been made to tackle this problem. Those are the solutions I can find so far. The first list would be from some commercial vendors.

### SAS Miner and Telecom solutions
SAS miner is the world leading commercial data mining tool according to the Garnter report. 

![Gartner Data Mining](http://www.kdnuggets.com/em/gartner-2014-mq-advanced-analytics.jpg)

SAS's core value is in those algorithms. However, along those years of implementing models for Telecom Industry, SAS did accumulate some domain knowledge and built a few models. 
As part of a suite of Telecommunications solutions, SAS provided those solutions:
* SAS Customer Retention for Telecommunications
* SAS Strategic Performance Management for Telecommunications
* SAS Campaign Management for Telecommunications
* SAS Customer Segmentation for Telecommunications
* SAS Cross-Sell and Up-Sell for Telecommunications
* SAS Payment Risk for Telecommunications
* SAS Customer Profitability for Telecommunications

There are a few papers available about using SAS to prediction the Churners. Junxiang Lu et.al. showed a typical process how to predict churners ([Predicting Customer Churn in the Telecommunications Industry –– An Application of Survival Analysis Modeling Using SAS](http://www2.sas.com/proceedings/sugi27/p114-27.pdf) ) .  The code in this paper can be used to build a very simple offline churn model in SAS miner. Also this papers listed this most important features used during the churn prediction:
- Primary household member’s age
- Gender and marital status
- Number of adults
- Primary household member’s occupation
- Household estimated income and wealth ranking
- Number of children and children’s age
- Number of vehicles and vehicle value
- Credit card
- Frequent traveler
- Responder to mail orders
- Dwelling and length of residence 

Carmelina Collado et al summarized their experience of implementation project using SAS Churn solution ( in 
[Implementation of a Customer Retention, Cross-Sell, Up-Sell and Payment Risk Solution using SAS Telecommunications Intelligence Solutions for Orange Dominicana](http://www2.sas.com/proceedings/forum2008/122-2008.pdf)). You may find some project management information for planning a similar project in this paper, but not much technical details are revealed.

### IBM mining solutions
IBM acquired SPSS at 2009 and built the modern mining capability around SPSS offering. IBM did not seem to wrap up churn solution the way SAS did, but they provided some good insight about how to leverage social media to tackle the churn problem in this paper ([Minimize customer churn with analytics](http://www.targetmarketingmag.com/promo/minimizecustomerchurn.pdf))

Before SPSS acquisition, IBM was selling the DB2 Miner. At 2001, IBM published a [redbook](http://www.amazon.com/Mining-Business-Telecoms-Intelligent-Redbooks/dp/0738422967) regarding how to deal with Telecom business problems with DB2 miner. In this book, IBM provided detailed steps about: 
* how to segment your customers
* how to prediction churners
* how to determine Life Time Value (LTV) of each customer
* how to detect fraud cases

You may also find lots standard brochures like
[this](ftp://public.dhe.ibm.com/software/data/sw-library/spss/IBM_SPSS_Telco_Churn_datasheet.pdf) regarding those commercial software, but those are not much useful.

### R
R is open source, free and good. Most of job by SAS can also be done by R. If it can not be done, you probably should go find another workaround instead for paying for this specific feature.

There are some papers about how to predict churners in R. The solutions using R looks more like academic papers since R users are mostly Statisticians. So I would cite them in the academic way:   
* Kaur, Manpreet, and Dr Prerna Mahajan. "[Churn Prediction in Telecom Industry Using R.](https://www.erpublication.org/admin/vol_issue1/upload%20Image/IJETR032129.pdf)" International Journal of Engineering and Technical Research (IJETR) ISSN: 2321-0869.

### Microsoft
Microsoft is not a big player in data mining domain. However, Afaq Alam Khan et al published a paper about how to predict churners in ISP:
* Khan, Afaq Alam, Sanjay Jamwal, and M. M. Sepehri. "[Applying data mining to customer churn prediction in an internet service provider](https://www.researchgate.net/profile/Mohammad_Mehdi_Sepehri/publication/49587595_Khan_A.A._Applying_Data_Mining_to_Customer_Churn_Prediction_in_an_Internet_Service_Provider_9(7)_8-14/links/5408883c0cf2187a6a6998df.pdf)." International Journal of Computer Applications 9.7 (2010): 8-14.

Though this paper used Microsoft Mining as the tool, the general steps about how to load data, how to extract features and the algorithms to run classification (decision tree & logistic regression) can be applied to any other mining platform.

One thing worth mentioning is that Microsoft acquired Revolution in 2015.  Microsoft would have stronger presence in this domain. 

### Academic Papers and Other Mining Tools
[MiningMart](http://mmart.cs.uni-dortmund.de/research/index.html)([1](http://mmart.cs.uni-dortmund.de/caseBase/ChurnPredictionCase/case.html)) seems to be a research project and can be [downloaded](https://sourceforge.net/projects/miningmart/) from Sourceforge.  MiningMart also provided a business mining model library called [MiningMart Case Base](http://mmart.cs.uni-dortmund.de/caseBase/index.html), including Churn, Sales Analysis and Targeted Promotion (call center NIT).

Telecom Italy used MiningMart to solve the churn problem ([paper](http://www-ai.cs.uni-dortmund.de/PublicPublicationFiles/richeldi_perrucci_2002b.pdf), [slides](http://www-ai.cs.uni-dortmund.de/MMWEB/downloads/presentations/OneDaySeminar/pdf/MMartSeminarFeb03_TILAB.pdf)). The paper provided very detailed information how to create a mining model. 


John Hadden et al try to run "[Churn Prediction using Complaints Data](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.193.4005&rep=rep1&type=pdf)". The paper is here:
* Hadden, John, et al. "Churn prediction using complaints data." Proceedings Of World Academy Of Science, Engineering and Technology. 2006. 

In this paper, John Hadden et al used many attributes from customer interaction, instead of traditional usage history: 
* No. of Complaints
* No. of appointments made for repair
* Type of customer
* No. of missed appointments
* No. of appointments made to a customer
* If an order has been placed

John achieved 82% accuracy by Decision Tree, which is better than regression and Bayesian Neural Network. It is very interesting that John's regression was actually a real Linear Regression with a few coefficients multiplying the previous list of factors.

Jiayin Qi et al. used logistic regression to predict the churners in fixed line telecom. This paper contains details about features used in the model and the algorithm settings:
* Qi, Juayin, et al. "[Churn prediction with limited information in fixed-line telecommunication](http://www.wcl.ece.upatras.gr/CSNDSP/contents/Sessions/Presentations/B5%20-%20Network%20Planning%20I/B5.1.pdf)." Symposium on Communication Systems Networks and Digital Signal Processing. 2006.


## Different Solutions
### Models for Different Customer Segments
In Telecom, different group of subscribers would show different pattern, especially about the loyalty. For example, postpaid customers are generally more loyal than prepaid customers; elder people are more stable than young people. To maximize the prediction accuracy, it is desired to create different Churn Models for those customer segments. I have seen many Telecom Operators creating over a few hundreds Churn models for different purposes.

There should be at least those different line of businesses:
* Prepaid Mobile
* Post paid Mobile
* Fixed Line & Fixed Broadband
* Enterprise Customer

### Simple Prediction over BSS Customer Profiles
The customer attributes acquired from CRM system are most widely used in the most of the telecom operators. Using a sample 
[churn data] (http://www.dataminingconsultant.com/DKD.htm), YHAT team create a very instructive [blog](http://blog.yhat.com/posts/predicting-customer-churn-with-sklearn.html) handling Churn problem using Python Scikit-Learn.  You can start by trying this program.

For easier churn prediction and future model development, we created stanmo package in Python.

### Data Preparation
Different algorithms take different type of data as input. Numerical data is warmly welcomed by most of famous algorithms. In the real life, order amount or total usage amount are intrinsicly numerical. So most of time, you don't worry about it and simply feed those data into the algorithms and wait for the magic. Certain algorithms may perform better if you normalized the data before giving it to the algorithm, like SVM.

On the contrary to the numerical data, categorical data and text data are hated by machine learning algorithms.  However, the categorical values are too common in our life to ignore. When we deal with customer data, we may find more categorical data than numerical ones. For example, customer gender, education level,  post code, marital status are all categorical, yet they are very important determining customer profile. You may want to encode those categorical values in  one-of-K 0/1 values. In Scikit-learn document ([preparation section](http://scikit-learn.org/stable/modules/preprocessing.html#encoding-categorical-features)), a few commonly used techniques are presented. You will need to apply those transformations to your own data.

Commercial mining tools may come with automatical data preparation, since they are facing not-so-proficient customers. For example:
* [Oracle Automatic Data Preparation](https://docs.oracle.com/cd/B28359_01/datamine.111/b28129/xform_data.htm) (or ADP) can handle categorical and numerical with outliers according to certain predefined rules.
* Other tools like [SPSS](http://www-03.ibm.com/software/products/en/spss-data-preparation),  Microsoft all claim that they have automatic data preparation though I can find very limitted documents.

In our churn problem, most of time the input would be a customer profile mixed with numerical and categorical values. In stanmo model, we created a class named ChurnInputDataEncoder to transform the data. ChurnInputDataEncoder has two main functions:

```python
    def fit(self,input_df=None):
    def transform(self,input_df=None):
```   
Given a training dataset, the fit function will look into the data distributions and create define proper rules to encode the data to be algorithm-friendly. 
First of all, you may want to specify data types of certain known columns to make sure the auto-encoder do not mess them up. In stanmo, the types are specified in curr_sdf.column_name_types. 
The following rules are created:
* If the attribute is not defined:
  * if the data is numerical, take as one attribute
  * if the data is categorical and if it contains less than 10 values, convert them into one-in-K encoded columns. This encoder is saved for futher decoding.
* if the attributes is defined as categorical, convert them into one-in-K encoded columns. This encoder is saved for futher decoding.


## Churn Prediction by Random Forest
In 2009, Orange donated their data for KDD Cup. Of all participants, Random forest becomes the winner. So in the model, we create the model by Random Forest as the default algorithm. You may choose to use decision tree or SVM for the same problem, but you probabily will find RF perform better.

Now let's start building our churn prediction model. We will use stanmo prebuilt churn model and some BSS data. For detailed information about how to use stanmo, please refer to [github](https://github.com/qiyangduan/stanmo).

The first step is to create a model by:
```sh
# stanmo create churn1 --spec=churn.ChurnMiningModel
# stanmo list models
```

Command 'stanmo list models' should return the list of models in stanmo.Before you can use the model, you should feed in some data to fit the model. Two data files are shipped with the package under $stanmo/data. You can use those files to fit your first model and test the prediction::

    # stanmo fit churn1 --input_file=~/anaconda2/envs/conda1/lib/python2.7/site-packages/stanmo/data/churn_source.csv --instance=1
    # stanmo list models

You can predict your data by two different ways. One is through the console in a batch style, as the following::
    # stanmo predict churn1 --input=~/anaconda2/envs/conda1/lib/python2.7/site-packages/stanmo/data/churn_apply.csv --output=/tmp/churn_apply_result1.csv
    # cat /tmp/churn_apply_result1.csv

In the 3rd column of tmp/churn_apply_result1.csv, you will find the predicted churn result. Now you can send this list to your call center to run the retention program.


Another way of running prediction is to start a http server and run the prediction through the REST API::
    # stanmo runserver churn1 --port=5011 &    


### Model Precision Monitoring
In your complex IT system, even for the same custoemr segment, you may have multiple churn models instead of one. Each of those models are created by different algorithms and different parameters. It is desired to have a continuous monitoring and election machanism to select the best model automatically.

When you want to switch from your original model to a new model (may be considering this stanmo churn model), you also want a A/B testing machanism. If you find new model performs even worse than original one, you can switch back. This makes the model users feel much more comfortable to adapt new technologies.


## Adding More Features

### Historical Usage Patterns
### Customer Experience 
### Telecom Social Circle features
### Social Media Usage
Like what IBM proposed.(IBM_SPSS_Telco_Churn_datasheet.pdf)
### Deep learning to improve accuracy
There are a few publications on the Internet regarding how to leverage Deep Learning for churn prediction problem. 
* [Deep Learning for Customer Churn Prediction](https://moz.com/devblog/deep-learning-for-customer-churn-prediction/), by Matt Peters. Matt described how to prediction churners for Moz subscribers. 
* Wise Athena applied [Deep Learning to prediction churners](http://wiseathena.com/blog/2014/12/applying-deep-learning-to-churn-prediction) in a Telecom Operator. Fanany provide a [review on Tumblr](http://fananymi.tumblr.com/post/113919770989/review-on-the-first-deep-learning-for-churn). In this paper, authors listed the source data they used (CDR and topup records) and the algorithms (Multilayer feedforward network). However, the implementation details are rather vague.
* how to determine Life Time Value (LTV) of each customer
* how to detect fraud cases

However, so far, I have not found any source code for easier replication of their result. So here I created a new program to run the churn prediction : 

### Handset life cycle prediction
We can build a handset life cycle model to calculate new handset opportunity.


# Churn Prediction by R
a