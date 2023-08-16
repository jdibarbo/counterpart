Repository for the Counterpart challenge. 

To run the notebook included in this repository, you have to create an environment using the included .yml file. To do so, you should go to the repository via cmd and run conda env create -f environment.yml. This file creates the *counterpart* environment.

# Overview
The assignment for the challenge was to fill in the missing data in the test set using the train set. 

To do this, I train two classification models:
- A binary classification model to estimate the *Value* feature -which I understand would be the target for a churn model-
- A multi-class classification model to estimate the *Status* feature, which I assume corresponds to the company's status: Non profit, private or publicly traded

I assume:  
- each website corresponds to a company
- the state feature corresponds to the state where the company is located
- revenue is the company's revenue in the previous year

# Data cleaning
Some light data cleaning was performed to remove some duplicate companies. 

# Metrics
- *Accuracy*: overall correctness of predictions (how many instances were predicted correctly out of all instances)
- *Recall*: evaluates the proportion of actual positive instances correctly identified by the model (out of all positive instances, how many did the model predict as positive?) 
- *Precision*: measures the proportion of correctly predicted positive instances (out of all instances predicted as positive, how many were actually positive?)
- *F1 score*: is the harmonic mean of the Recall and Accuracy metrics.

# Conclusions
The main metric we consider in both models is *recall*, as we're most interested in identifying all those that positive. <br>
This is particularly important in the churn model, where it's not as important to have false positives but to try to capture as many of the positive class as possible to prevent churn. <br>

The RF results are exactly the same as the dummy model in both cases. This means: 

- the models are just predicting the most frequent category
- the features are not giving enough explanatory value to the model, i.e. the model is underfitting the data. 

Some things that could be tried to improve the results: <br>
1) for each model, it would be necessary to have more information:
     - for the churn model: about the company such as activity, number of years it's a client, if there's information about the number of employees and its variation over time, the company's history in counterpart, etc.
     - for the multi-class model: also information about the company such as the sector it's in, investment rounds maybe? and information related to that. 
2) Data on those companies whose revenue is "Undefined" would also help, as currently, almost 25% of companies fall into this category.
3) reduce dimensionality in cities, as it can't be used as is. There are too many cities for this to be used as a feature. It would be useful if it could be at a higher level, maybe jurisdiction or even state. <br>
4) If the models are still underfitting with an RF classifier with the new features, it could benefit to try a different algorithm:
    - for the churn model it could be an XGBoost model
    - for the multi-class model it could be an SVM model 
5) Some over/under sampling could be included to try to get a better prediction for the target, but this would likely not be fruitful if we don't add predictive features. 