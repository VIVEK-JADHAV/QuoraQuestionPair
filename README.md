# QuoraQuestionPair

![FlaskApp](https://github.com/VIVEK-JADHAV/QuoraQuestionPair/blob/main/Images/FlaskApp.PNG)

### Problem Definition
In this challenge, two questions posted on Quora are given. The task is to classify whether the pair of questions are similar or dissimilar, making this a Binary Classification task.

### Dataset
The dataset provided by Kaggle has two files, train and test, although I am using only training data. The train file has 404290 question pairs. Each row has question1 and its id, question2 and its id and target variable, is_duplicate with values 0(dissimilar) and 1(similar).

### Performance Metric
The performance metric used is the ROC-AUC score. It is the area under the curve between True Positive rate and False Positive rate for different thresholds. It indicates  the probability with which a given question pair will be correctly classified.

### Exploratory Data Analysis
* #### Analysing Target Variable
The target variable, is_duplicate, is a binary variable with 0 and 1 as values. The percentage of similar questions were 36.92 and dissimilar questions were 63.07. There is significant representation of both the classes, hence, dataset is not imbalanced.

![TargetVariable](https://github.com/VIVEK-JADHAV/QuoraQuestionPair/blob/main/Images/Target.JPG)

* #### Analysing Input Variable
Created new features using question 1 and question2 like frequency of questions, count of words in questions, common words between the questions. Among them, the normalised word share was interesting. It's distribution showed that similar questions have higher word share than dissimilar questions, which logically makes sense.

![WordShare](https://github.com/VIVEK-JADHAV/QuoraQuestionPair/blob/main/Images/Wordshare.JPG)

### Data Pre-processing
* The first step is to clean the data. It involved removing stopwords,punctuations,html tags, words of length less than 3, expand short forms(they 'll to they will) and convert each word to lower case
* The data was split into train,validation and test such that distribution of target variable is maintained (stratified split).
* Using Tensorflow's tokenizer, the questions 1 and 2 were converted to tokens, with padding to support batch operation
* Glove vectors( which will be used in embedding layer in the model) is loaded, which gives 100 dimensional vector for each token

### Model
I have trained a Siamese network to differentiate between similar and dissimilar questions. In a nutshell, the siamese network finds a pattern for each underlying classes( which is unknown). If the pattern for both the questions match, they will be classified similar else, dissimilar.

![Model](https://github.com/VIVEK-JADHAV/QuoraQuestionPair/blob/main/Images/Model.JPG)

The model has the following layers:
* Input layer: 2 input layers with sequence of question1 and question2 tokens.
* Embedding layer: Converts tokens to 100 dimensional vector.
* Bi-Directional LSTM: This is a common layer for both the questions. After it is trained,it generates unique pattern for each underlying class and returns output for both question1 and question2.
* Distance layer: This layer outputs L1 norm between lstm outputs of question1 and question2. It differentiates between two classes. If the two questions are similar, the distance vector would have smaller values and vice-versa.
* Output layer: Single neuron with sigmoid activation.

The model was trained with Binary Cross Entropy loss and Adam optimiser.

![ROC](https://github.com/VIVEK-JADHAV/QuoraQuestionPair/blob/main/Images/ROC.JPG)

The threshold value for classifying was selected such that product of True Positive Rate and 1-False Positive Rate is maximum. It turned out to be 0.38. If the model retured a value greater than 0.38, it is classified as similar.

On the test dataset, the AUC score was 0.8 with high precision and recall.





