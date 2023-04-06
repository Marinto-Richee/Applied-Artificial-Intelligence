# Implementation of Bayesian Classifier
## AIM
To Construct a Bayes Classifier to classify Iris dataset using Python.
## ALGORITHM
Input: 
- X: the training data, where each row represents a sample and each column represents a feature.
- y: the target labels for the training data.
- X_test: the testing data, where each row represents a sample and each column represents a feature.

Output:
- y_pred: the predicted labels for the testing data.

1. Create a BayesClassifier class with the following methods:
   1. __init__ method to initialize the Gaussian Naive Bayes classifier from scikit-learn.
   2. fit method to fit the classifier to the training data using the Gaussian Naive Bayes algorithm from scikit-learn.
   3. predict method to make predictions on the testing data using the fitted classifier from scikit-learn.
2. Load the Iris dataset using the load_iris function from scikit-learn.
3. Split the data into training and testing sets using the train_test_split function from scikit-learn.
4. Create a BayesClassifier instance.
5. Train the classifier on the training data using the fit method.
6. Make predictions on the testing data using the predict method.
7. Evaluate the classifier's accuracy using the accuracy_score function from scikit-learn.

## PROGRAM
```python3
import numpy as np
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import GaussianNB
from sklearn.metrics import accuracy_score

class BayesClassifier:
  def __init__(self):
    self.clf=GaussianNB()
  
  def fit(self,X,y):
    self.clf.fit(X,y)

  def predict(self,X):
    return self.clf.predict(X)
  
iris=load_iris()
X_train,X_test,y_train,y_test=train_test_split(iris.data,iris.target,test_size=0.3,random_state=38)

clf=BayesClassifier()
clf.fit(X_train,y_train)
y_pred=clf.predict(X_test)
accuracy=accuracy_score(y_test,y_pred)
print("Accuracy: ",accuracy)
```

## OUTPUT
![image](https://user-images.githubusercontent.com/65499285/230391925-576f0532-c376-4cfc-819f-99e3eaf8b551.png)

## RESULT
Thus, Bayes classifier for Iris dataset is implemented successfully.
