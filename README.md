# Image-Classification
In this project, Image classification is conducted on multiple image classes.

## Goal of the project

 The main focus in this project is to develop a classification model. In this project 11 classes  of images are provided in dense matrix format and the training labels are provided as integers. The main task is to build a classification model the given dataset and provide the prediction for the test set data – as a submission to Kaggle. 


## Dataset Information

As briefly stated in the above section, the dataset contains images of 11 classes. Provided datasets are features extracted from images where the training and test data are in dense matrix, and training labels are provided as integers. The training dataset in composed of images described as 887-dimensional vectors highly unbalanced and has 887-dimensional vectors composed by concatenating the following features: 

       - 512 Histogram of Oriented Gradients (HOG) features 
       - 256 Normalized Color Histogram (Hist) features
       - 64 Local Binary Pattern (LBP) features 
       - 48 Color gradient (RGB) features 
       - 7 Depth of Field (DF) features 

The training dataset contain 18000 records and the test data consists of 3000 records as described below: 

       - train.dat: Training set (dense matrix, samples/images in lines, features in columns). 
       - train.labels: Training class labels (integers, one per line). 
       - test.dat: Test set (dense matrix, samples/images in lines, features in columns). 
       - format.dat: A sample submission with 3000 entries randomly chosen to be 1-11. 




# APPROACH

## A.	Feature Selection

The 887 features in the dataset are composed from different sources as described above. As a result, they have different contribution in the classification of the images. Hence, at this stage, I am applying feature selection algorithm to the datasets to help me:
 
        -	Reduce overfitting. 
        -   Improve Accuracy      
        -   Reduce Training Time

As a feature selection algorithm, I wrote a program to drop features where their values and standard deviation do not vary. Using this way, I was able to drop all the features that wouldn’t contribute much to our classifier and/or could otherwise mislead the classification algorithm.




## B.	Handling Data Imbalance

Data is said to be imbalanced if the instances of one class outnumber the other class/classes by a large proportion. Likewise, the training dataset provided is highly imbalanced. For example, the training data contains 8855 cars but only 2 bicycles and 0 people. Feeding this raw training data to the classifier can make the classifier highly biased in favor of the classes with higher records because the algorithm cannot learn about the minority classes due to lack of enough instances.

Therefore, handling this data imbalance is very crucial and necessary task in this assignment. To deal with this data imbalance, I used Synthetic Minority Over-Sampling Technique, abbreviated as SMOTE. This data balancing technique generates synthetic data for the minority classes.






## C.	Split Training Data 

For the purpose of validation of classification algorithm, I split the training data into training and validation subsets. Although the training set can be split at any proportion, 80% to 20% seemed to be optimal based on many trials. Hence, the training data is split into 80% training subset and 20% validation subset and fed to different classification algorithms for training. I have also used a GridSearchCV from the sklearn library that applies different parameters of classifiers by cross-validated grid-search over a parameter grid.  






## D.	Train and Compare Classification Algorithms

After splitting the data, I fed the training subset into classification algorithms. The first algorithm I tried was Support Vector Machines. For our dataset, SVM has very low performance. I further trained SVM using GridSearchCV to try different combinations of kernels and c values, which ended up at highest f1 score 54.05%, which is not satisfactory at all. 

Likewise, I trained Logistic Regression and Multilayer Perception Classifiers to compare their performance. However, their performance was not satisfactory either. Furthermore, I used GridSearchCV to try different combinations of their parameters, their performance was improved with some combinations but not satisfactory. 

Finally, I trained Voting Classifier – and ensemble method classifier which includes RandomForest, Adaboost, KNeighbors Classifier, XGB Classifier and Extra Tree Classifier and takes the result as a vote from these classifiers. The classifier has very great performance of f1 score 93.33%. Here are the confusion matrix and the classification report for the Voting Classifier.


