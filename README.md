# QuoraQuestionPair

### Problem Definition
In this challenge, two questions posted on Quora are given. The task is to classify whether the pair of questions are similar or dissimilar, making this a Binary Classification task.

### Dataset
The dataset provided by Kaggle has two files, train and test, although I am using only training data. The train file has 404290 question pairs. Each row has question1 and its id, question2 and its id and target variable, is_duplicate with values 0(dissimilar) and 1(similar).

### Performance Metric
The performance metric used is the ROC-AUC score. It is the area under the curve between True Positive rate and False Positive rate for different thresholds. It indicates  the probability with which a given question pair will be correctly classified.

### Exploratory Data Analysis
* #### Analysing Target Variable

