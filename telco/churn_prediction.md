# Churn Prediction
Churn management seems to be an eternal business problem for most of Telecom operators.  When a subscriber terminate the current service, we call it him a churner. 

Normally we see higher churn rate for prepaid business than for postpaid business. Developing countries also observe higher churn rate than developed countries.  
According to this [blog](http://ipcarrier.blogspot.tw/2015/07/based-on-its-churn-rates-netflix-is-way.html),  even in developed countries like USA, monthly churn rate could go up to 5%. This means that each year, Sprint lose half of all its prepaid subscribers.

![Churn Stats](https://lh3.googleusercontent.com/H4kvIvyq-XldLz0jwFKYP4mbyiORZ3tOqkFplxwji1LyWAyTyaqha5LKhPzj5oGVc_G5FbeY8peZJueiMI-mf11-hCZCwPMBnjpzBjGDSefll-bSfs_bqikJIof_kIhCb3zeNmY)

Losing customer means huge lost of monthly subscription income. Also operators have to spend more money to win back new customers. Therefore, a good churn management solution is very important to every telecom operator.

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







## Different Solutions
### Simple Prediction over BSS Customer Profiles
### Customer Experience 
### Social interaction features
### Deep learning to improve accuracy
### Handset life cycle prediction
We can build a handset life cycle model to calculate new handset opportunity.

## Churn Prediction by Random Forest

In 2009, Orange donated their data for KDD Cup. Of all participants, Random forest becomes the winner.

# Churn Prediction by R
a