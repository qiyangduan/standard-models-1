# What Makes a Model 
To many data scientist, a model means a script which can load some data, fit a model and then predict another dataset, or draw some nice charts. The prediction would be delivered to another engineering team as a CSV file. Then it is the engineering team's responsibility to figure out how to embed this file into the business flow. Most of the time, they have to develop another presentation server to bridge the knowledge to front tier. 

To make the model live by itself in the real business environment, it must have those features:
* It must have the traditional core function of ingesting data, fitting model and Predicting over new data.
* It must have an interface to other systems. Ideally, a HTTP based RESTful Interface is needed.
* It must have its own testing 
* It should be able to adjust itself according to the new data. This is could be ideally done by incremental model updating or a full retraing over new datasets. 

Only the data science team knows the strength and weakness of a model. Just like the full stack programmer in devops, now let's work full stack to make this *live* model.  
