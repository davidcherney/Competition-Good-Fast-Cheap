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

This competition between 5 teams of data science fellow at General Assembly featured a different contraint for each team. Our team's constaint was a small number of samples. Teams were judged by their F1 score on the test set `test_data.csv` for which the incomes were not given.

- Samples from which we could train models: 6,513

- Samples to predict: 16,281.

---
## Constraints
#### Team Sample Constraint
- Your choice of algorithm
- Your choice of features
- Must use the cheap train sample


---
## DATA

[Income Census Dataset](https://archive.ics.uci.edu/ml/datasets/census+income)

---
## Methodology
---
#### **Data Cleaning**

- Checked for null values; there were none.
- Resolved inconsistancy between `work-class` values in  ['never worked' ,'without pay'] and `hours_per_week` non-zero.
- had some values that were '?' in categorical data that we one hot encoded, thus we did not need to impute.


#### **EDA**
- Looked at each feature individually and decided how to encode data. (e.g.s one hot encoding, drop feature)
- Looked for which features were most strongly correlated with income. 

#### Data Imbalance
We dealt with the imbalance of data, 76% income under 50k to 24% income over 50k, by upsampling the over 50k category. This improved our validation scores. 

#### **Feature Engineering**
- Dumified features in train, validation, and test datasets simultaneously to ensure representation of all categorical values in all datasets.
- Dropped features that 
    - we did not understand 
    - were unlikely to resolve income
    - contained categorical data better captured by another feature (e.g. years of school vs highest grade attended.)

## Modeing

We developed a stack model from the best version of KNN, Decision Tree Classifier, Bagging Classifier, Random Forest Classifier, and AdaBoost with Decision Trees. 

## Metrics


| data      | f1    | sensativity | specificity | precision |
| ---       | ---   | ---         | ---         | ---       |
| balanced  | 64.41 | 58.16       | 92.89       | 72.15     |
| unbalanced| 68.09 | 60.97       | 94.26       | 77.10     |

Training on balanced data resulted in a model with f1 score of 64.41% on validation data. This score is low because f1 score is the harmonic mean of precision and sensativity, both of which were low at 72.15% and 58.16%, respectively. By contrast, our specificity score of 92.89% indicates that our model is much better at accurately pointing out that a person makes less than $50k per year than at accurately pointing out when they make more than 50k per year. 


Training on the original unbalanced data gave a model with f1 score of 68.09%.  Precision and sensativity both went up by going back to unbalanced data, at 77.10% and 60.97% respectively.Surprisingly





We note here that we did not win because we made the mistake of augmenting  the over 50k category while the train and validation sets were concatenated. This artificially raised our validation accuracy by leaking training data into the validation set. The mistake, which gave an f1 score of 92.99% on validation data was corrected after the competition. However, that correction led to a low sensativity by effectively giving three times the weight to each data point in the over 50k category as points in the unnder 50k category. 


---
## Conclusion
The disadvantage of a small data set is a significant one; despite the sophistication and bredth of our binary classification model stacking, our sensativity score was very low. 

Interestingly, if the binarization had been the opposite, 1 for under 50k and 0 for over, our f1 score would have been very different 81.22%. This difference of 16.81 points reflects the specificity of our model over sensativity, which was likely due to data imbalance in a small dataset and to the effective trippling of our under 50k datapoints in data augmentation. We conclude that data augmentation is a dangerous way to deal with data imbalance, and that steps should be taken to understand the effects of the augmentation if if is applied. 




---
## Recommendations and Next Steps
The next steps for this project would be to further tune the models to see if we can get a more accurate model. We did some feature engineering, but just ran out of time. Thus being able to try more engineered features might help improve this model as well.
Ulitmately the best thing for this project would be more time to try more model parameters and features that take longer to run but could be more accurate.



