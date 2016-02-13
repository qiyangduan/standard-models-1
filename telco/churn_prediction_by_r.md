# Churn Prediction by R
As we summarized before in [What Makes a Model](../what_makes_a_model.md), whenever we want to create a ready-to-integrate model, we have to make sure that the model can survive in real life complex environment. Though R is an excellent data exploring platform, constructing business app might be a little bit difficult. Based on many existing materials on Internet, I took a first shot. I will go through those steps to present my result:

* A very simple training and predicting program using Decision Tree (rpart).
* It must have an interface to other systems. Ideally, a HTTP based RESTful Interface is needed.
* It must have its own testing 
* It should be able to adjust itself according to the new data. This is could be ideally done by incremental model updating or a full retraing over new datasets. 
* 
