# QuoraQuestionPair

### Problem Definition
In this challenge, two questions posted on Quora are given. The task is to classify whether the pair of questions are similar or dissimilar, making this a Binary Classification task.

### Dataset
The dataset provided by Kaggle has two files, train and test, although I am using only training data. The train file has 404290 question pairs. Each row has question1 and its id, question2 and its id and target variable, is_duplicate with values 0(dissimilar) and 1(similar).

### Performance Metric
The performance metric used is the ROC-AUC score. It is the area under the curve between True Positive rate and False Positive rate for different thresholds. It indicates  the probability with which a given question pair will be correctly classified.

### Exploratory Data Analysis
* #### Analysing Target Variable
The target variable, is_duplicate, is a binary variable with 0 and 1 as values. The percentage of similar questions were 36.92 and dissimilar questions were 63.07. There is significant representation of both the classes, hence, dataset is not imbalanced.

* #### Analysing Input Variable
Created new features using question 1 and question2 like frequency of questions, count of words in questions, common words between the questions. Among them, the normalised word share was interesting. It's distribution showed that similar questions have higher word share than dissimilar questions, which logically makes sense.



