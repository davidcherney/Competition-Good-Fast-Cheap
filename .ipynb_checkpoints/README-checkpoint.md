# TEAM MAGIC 8 BALL
---
## Team members
- Shania Thomas
- David Cherney
- Afolabi Cardoso
- Thomas Prich

---

## Problem Statement
Predict if income is in excess of $50,000 given other census data. 

Further, generate predicted probabilities of incommes being above $50,000 for each row in the test set. 

This competition between 5 teams of data science fellows at General Assembly featured a different contraint for each team. Our team's constaint was a small number of samples. This constraint was known as The Cheap Constraint in the Cheap-Fast-Good competition.


Cheap Constraint:
- Samples from which we could train models: 6,513

- Samples to predict: 16,281

Teams were judged by their F1 score on the test set `test_data.csv` for which the incomes were not given.

---
## The Cheap Constraint:
- Your choice of algorithm
- Your choice of features
- Must use the cheap train sample with 6,513 samples
- Must generate predicions and probabilities for all 16,281 samples from train set


---
## DATA

[Income Census Dataset](https://archive.ics.uci.edu/ml/datasets/census+income)

---
## Methodology
---
### EDA Notebook: 
#### Data Cleaning

- Checked for null values; there were none.
- Resolved inconsistancy between `work-class` values in  ['never worked' ,'without pay'] and `hours_per_week` non-zero.
- had some values that were '?' in categorical data that we one hot encoded, thus we did not need to impute.


#### EDA
- Looked at each feature individually and decided how to encode data. (e.g.s one hot encoding, drop feature)
- Looked for which features were most strongly correlated with income. 


### Model notebook
#### Feature Engineering
- Dumified features in train, validation, and test datasets simultaneously to ensure representation of all categorical values in all datasets.
- Dropped features that 
    - we did not understand 
    - were unlikely to resolve income
    - contained categorical data better captured by another feature (e.g. years of school vs highest grade attended.)
- engineered one quadratic feature: since greater education likely linearly correlates to hourly py rate, income likley correlates with education times hours worked per week, a quadratic feature.


#### Data Imbalance
We learned from our mistakes in attempting to deal with the imbalance of data, 76% income under 50k to 24% income over 50k. 

##### Description of Mistake and Subsequent Correction 

**Initially** we upsampled the over 50k category, but made the mistake of augmenting  the over 50k category **while** the train and validation sets were concatenated. This artificially raised our validation accuracy by leaking training data into the validation set. The mistake was corrected after the competition.  The severity of this mistake is visable in the table of scores below. 

**Secondarily,** we balanced the training data only. The result was a much lower f1 score (0.65 vs 0.93). We believe that the source of this very low f1score comes from upsampling of the over 50k class leading to overfiting on the over 50k data poits by effectively giving three times the weight to each data point in the over 50k category as points in the unnder 50k category. 

**Finally,** we used the original unbalanced data to fit the model. This imporved variance, and all matrics except train set accuracy. Our belief that balancing data led to overfitting was supported by the gap between train and val accuraccy closing from 14 points to 2 points in going from augmented/balanced data to unbalanced data. 

## Modeing

We developed a stack model from the best version of KNN, Decision Tree Classifier, Bagging Classifier, Random Forest Classifier, and AdaBoost with Decision Trees. 

## Metrics

The following table documents our scores (in percentage) for model trained on 
- polluted data
- balanced data
- unbalanced data

| Data      | f1   |Sensativity|Specificity|Precision|Train Accuracy|Validation Accuracy|
| ---       | ---  | ---       | ---       | ---     | ---          | ---               |
| Polluted  | 92.99|96.04      |89.48      | 90.14   | 98.87        | 92.76             |
| Balanced  | 64.68|58.16      |93.13      | 72.84   | 98.83        | 84.71             |
| Unbalanced| 68.29|60.97      |94.42      | 77.60   | 88.43        | 86.37             | 

---
## Conclusion
The disadvantage of a small data set is a significant one; despite the sophistication and bredth of our binary classification model stacking, our sensativity score was very low.  Our model was trained on 4,884 samples with class sizes 3,708 and 1,176. Another group with tens of thousands of data points from which to train models were able to achieve a significantly higher f1 score of 85.8%. 

From our mistake, polluting validation data with training data in the data balancing process, we conclude that data augmentation is a dangerous way to deal with data imbalance;  steps should be taken to understand the effects of the augmentation if it is applied. 




---
## Recommendations and Next Steps
The next steps for this project would be to further tune the models to see if we can get a more accurate model. More engineered features might help improve this model as well.
Ulitmately the best thing for this project would be more time to try more model parameters and features that take longer to run but could be more accurate.