# Credit-Card-Fraud-Detection-Rapidminer

## Introduction to the Data:
The data contains credit card transactions over a period of time, and the aim is to determine the fraudulent transactions so that the customers are not charged for items they did not purchase.

The data has 227,846 transaction examples, including 394 fraudulent ones.
There are 28 numerical attributes (v1 to v28), the 'time' attribute refers to the time between the current transaction and the first one, the 'amount' refers to the transaction amount, the 'class' is the label attribute which takes '1' in case of fraud transection and '0' otherwise.

The task is a classification task, which should determine the future fraudulent transactions depending on the given historical data. A detailed look at the data is imbalanced (the fraud is 0.173% of the total).

## Task 1 

### Basic Workflow 

In this initial stage of workflow:
 
•	We import the data from the .csv file to RapidMiner, by storing them in a local repository.
•	Change the type of class attribute from integer to binomial, and then substitute the values: 0 to ‘correct’, 1 to ‘fraud’.
•	Split the data into 30% test and 70% train using stratified sampling method, ensuring that the class distribution in the train and test set is the same as in the whole data set. We keep the test dataset to the end.
In the screenshot attached below, the process is provided for your reference.

![image](https://user-images.githubusercontent.com/52135942/166114844-782e30b3-72c5-4189-a9eb-62a592fceadf.png)

### Modeling (file: Final Exam basic model import) 

*Note: in this basic modelling, it took about one hour to train the data using KNN (k=5) for one-fold; therefore, my CPU did not help to do cross-validation on KNN in this stage.
Now let us take an overview of the behaviour of the data and apply three classification algorithms without any refinement.
The training and test data are obtained by executing the file Exam-1-import. 
The model is trained by KNN (k=5), decision tree, and Naïve Bayes (cross-valid-fold=10). 
The first observation is that KNN is much slower than others.

The accuracy is more than 99% for KNN and decision tree and about 97% for Naïve Bayes (validation and test data), which is suitable for all. Still, by looking closely, we see the recall of positive class (fraud) is only 5.08% in KNN increased to 67.67% in the decision tree (validation) and 76.27% decision tree (test), and 82.25% Naïve Bayes (validation) and 84.75% in naïve Bayes.

![image](https://user-images.githubusercontent.com/52135942/166114854-3c7427ff-0ceb-4388-b9c3-11ebf3608ca8.png)

In the screenshot attached above and below, the process is provided for your reference.

![image](https://user-images.githubusercontent.com/52135942/166114878-e4e8ccdc-70c2-44ec-a7b5-6b1374a6979b.png)

![image](https://user-images.githubusercontent.com/52135942/166114886-bf05c417-805c-4186-8395-5233e16b7bd1.png)

![image](https://user-images.githubusercontent.com/52135942/166114892-18226387-448a-49dc-a8bc-65aa6228f089.png)

![image](https://user-images.githubusercontent.com/52135942/166114896-b200e3d0-8cf6-4ef2-bd95-1232afcef03f.png)

We can assume that the decision tree's performance is much better than other algorithms and good precision and sufficient recall numbers by looking at the results.

## Task 2
### Data Preparation 
In this stage, the data is prepared for modelling and refinement:

*	The unprocessed training and test data are obtained by executing the file Exam-1-import (section 1).
*	By analyzing the data, there are no missing values
*	Any duplicated examples in the training set are checked and removed.
*	The training set is normalized (transformed to get variables with mean=0 and standard deviation std=1), a dimension reduction method (PCA) is applied (to keep 95% of the total variance, 27 attributes have remained in the output of the PCA, which gives the impression that the original data (numerical ones) is almost uncorrelated and might be the output of another PCA operation).
*	The normalized and PCA models are grouped to be applied on the test set later to keep the exact dimensions.
*	Finally, the preprocessed training and test data are stored in the local repository to save preprocessing time each time we run the model.

![image](https://user-images.githubusercontent.com/52135942/166115979-a939b09d-9e6c-441f-8db7-6b77359e8e69.png)

### Hyperparameter Optimization

The stored preprocessed training and test data set from the previous section avoid imbalance classes mentioned before. The classes (correct, fraud) are to be balanced using sample operation.

![image](https://user-images.githubusercontent.com/52135942/166116002-e5ca42ed-82df-4391-b143-fc7ff98fca04.png)
![image](https://user-images.githubusercontent.com/52135942/166116006-b28c5ab5-56a6-4336-adbb-8127a62e6f8f.png)

*	Decision Tree: the number of folds in cross-validation and the max depth of the tree are optimized using optimize parameter operation. The best result is by using cross-validation of 20 folds and tree with max-depth=4.

![image](https://user-images.githubusercontent.com/52135942/166116030-548d0655-9ec4-4d77-8fb3-581b075c606f.png)


Looking at the performance of the model on the test data, we obtain an accuracy of 96.15% with 88.98% recall of the fraud class (TNR), which is much better than the one in basic modelling, even though that the precision of the fraud is much lower (3.86%), but as mentioned above the actual fraud is more (to some extend). 

![image](https://user-images.githubusercontent.com/52135942/166116637-e5028d51-2568-4c33-9331-8ad2203ccdeb.png)

![image](https://user-images.githubusercontent.com/52135942/166116638-529ca7b5-0727-48ab-be26-482e59658723.png)


*	Naive Bayes: with optimizing the number of folds in the cross-validation, the accuracy of the test data is 94.01%, with an 88.98% recall of the fraud.

![image](https://user-images.githubusercontent.com/52135942/166116546-1f5b05df-82b7-41c5-ae3c-bef45f576cb6.png)

*	KNN: the number of folds is optimized between 2 and 12-fold, and k of the KNN model is optimized between 2 and 10, getting the best k=10 and cross-Val-fold=12.

![image](https://user-images.githubusercontent.com/52135942/166116648-039baf60-ce44-4ffe-87d4-4e7e932bf845.png)

![image](https://user-images.githubusercontent.com/52135942/166116653-e0bea61c-3958-4bb3-8f5d-fb6d8307b5dd.png)









