# Credit-Card-Fraud-Detection

## Introduction to the Data:
The data contains credit card transactions over a period of time, and the aim is to determine the fraudulent transactions so that the customers are not charged for items they did not purchase.

The data has 227,846 transaction examples, including 394 fraudulent ones.
There are 28 numerical attributes (v1 to v28), the 'time' attribute refers to the time between the current transaction and the first one, the 'amount' refers to the transaction amount, the 'class' is the label attribute which takes '1' in case of fraud transection and '0' otherwise.

The task is a classification task, which should determine the future fraudulent transactions depending on the given historical data. A detailed look at the data is imbalanced (the fraud is 0.173% of the total).
![image](https://user-images.githubusercontent.com/52135942/166114721-74dac5e8-b937-4289-b980-c27ce64cdf3c.png)

## Task 1 

### Basic Workflow 

In this initial stage of workflow:
 
•	We import the data from the .csv file to RapidMiner, by storing them in a local repository.
•	Change the type of class attribute from integer to binomial, and then substitute the values: 0 to ‘correct’, 1 to ‘fraud’.
•	Split the data into 30% test and 70% train using stratified sampling method, ensuring that the class distribution in the train and test set is the same as in the whole data set. We keep the test dataset to the end.
In the screenshot attached below, the process is provided for your reference.
![image](https://user-images.githubusercontent.com/52135942/166114730-abf8b4dd-7722-426d-a060-ce531aace961.png)

### Modeling (file: Final Exam basic model import) 

*Note: in this basic modelling, it took about one hour to train the data using KNN (k=5) for one-fold; therefore, my CPU did not help to do cross-validation on KNN in this stage.
Now let us take an overview of the behaviour of the data and apply three classification algorithms without any refinement.
The training and test data are obtained by executing the file Exam-1-import. 
The model is trained by KNN (k=5), decision tree, and Naïve Bayes (cross-valid-fold=10). 
The first observation is that KNN is much slower than others.

The accuracy is more than 99% for KNN and decision tree and about 97% for Naïve Bayes (validation and test data), which is suitable for all. Still, by looking closely, we see the recall of positive class (fraud) is only 5.08% in KNN increased to 67.67% in the decision tree (validation) and 76.27% decision tree (test), and 82.25% Naïve Bayes (validation) and 84.75% in naïve Bayes.

![image](https://user-images.githubusercontent.com/52135942/166114786-ea625137-b600-499b-979e-f86e444063a2.png)
