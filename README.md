# TEAM MAGIC 8 BALL
---
## Team members
- Shania Thomas
- David Cherney
- Afolabi Cardoso
- Thomas Prich

---

## Problem Statement
Predict if a person's income is in excess of 50,000 given certain profile and certain and more specifically to generate predicted probabilities of incommes beign above 50,000 for each row in the test set. 

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

- Checked for null values
- removed hours-per-week that were zero from dataset
- had some values that were '?', we left as is


#### **EDA**
- Looked at each feature individually and selected the best features
- Used the heat map to check for most correlated values


#### **Feature Engineering**
- Dumified both test and train dataset
- Dropped features that didn't have a good correlation with wages

---
## Conclusion

After working on a combination of models, stacking the best version of KNN, Decision Tree Classifier, Bagging Classifier, Random Forest Classifier, and AdaBoost with Decision Trees provided the best overall cross val score and test score from our train test split. It also generated an f1 score of 93.16%. Please see the confusion matrix in the 'model' notebook for how the model predicted.

---
## Recommendations and Next Steps
The next steps for this project would be to further tune the models to see if we can get a more accurate model. We did some feature engineering, but just ran out of time. Thus being able to try more engineered features might help improve this model as well.
Ulitmately the best thing for this project would be more time to try more model parameters and features that take longer to run but could be more accurate.



