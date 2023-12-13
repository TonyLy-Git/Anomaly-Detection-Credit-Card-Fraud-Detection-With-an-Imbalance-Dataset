# Anomaly-Detection-Credit-Card-Fraud-Detection-With-an-Imbalance-Dataset

Link to creditcard.csv file (file was too big to attach): https://drive.google.com/file/d/1IJUkZI-TlPeGEaUqc18OCEqr9ynihtnL/view?usp=drive_link

Data can also be found at: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud

If you want to run the ipynb, you'll need to change the directory of where the data is stored in your Google Drive (if ran in Google Colab). 

Introduction

This project was undertaken to gain a better understanding on how to approach an imbalanced dataset. The purpose of the research was to analyze the dataset to propose a methodology model architecture of which we decided to imploy the anomaly detection methodology with the AutoEncoder architecture. 

Selection of Data

The dataset was taken from Kaggle. The dataset consists of 30 features with 2 predetermined classes: normal and fraudulent transaction. Of the 30 features, 28 are anonmylized due to confidentiality concerns. The features we do have information about are time (what hour in the day did the transaction occurred) and amount (transaction amount). The anonmylized data has been transformed into numerical values by the principle component analysis. The dataset is heavily imbalanced with 284,315 normal transactions to 492 fraudulent transaction; 99.83% of the transaction is normal. Since the dataset is heavily imbalanced, we decided to implement the anomaly detection approach, since the traditional classification approach is very sensitive to imbalanced dataset incomparison to anomaly detection. 

There wasn't any feature engineering, but more so data visualization to determine the approach methodology and model architecture. With the data visualization of comparing the density distribution of the two transaction types for each anonmylized feature, we found that 11 of the 28 features have a similar distribution (refer to either presentation slides or paper for the figures). With more than half of the features displaying different distributions, we decided to implement the AutoEncoder architecture. 

Methods

The AutoEncoder architecture is a model that has an encoder and decoder function. The encoder compresses the input into a smaller dimensional representation (known as the bottleneck). Then the decode takes the outputed representation and tries to recreate the input. Then the output is compared to the input and is measured by the reconstruction error. In our implementation, we want the model to learn the features of only normal transaction so that when it gets inputted a fraudulent transaction, it would won't be able to recreate the input based on the model's weights. Therefore, in theory, the fraudulent transaction should output a high reconstruction error and the normal transaction should output a low reconstruction error. 

Model: "sequential_3"
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
==============================================================
 dense_40 (Dense)            (None, 25)                775       
                                                                 
 dense_41 (Dense)            (None, 19)                494       
                                                                 
 dense_42 (Dense)            (None, 13)                260       
                                                                 
 dense_43 (Dense)            (None, 6)                 84        
                                                                 
 dense_44 (Dense)            (None, 6)                 42        
                                                                 
 dense_45 (Dense)            (None, 13)                91        
                                                                 
 dense_46 (Dense)            (None, 19)                266       
                                                                 
 dense_47 (Dense)            (None, 30)                600       
                                                                 
==============================================================
Total params: 2612 (10.20 KB)
Trainable params: 2612 (10.20 KB)
Non-trainable params: 0 (0.00 Byte)
_________________________________________________________________

The training hyperparameters consists of: 
Optimizer = Adam
Metrics = Accuracy
Epoch = 50
Batch size = 512
Learning rate = 1e-7

Results

Precision: 80.71%

Recall: 22.97%

F1-score: 35.76%

Discussion

We ended up with not optimal results based on the metrics above. The model did not perform well and was not able to detect majority of fraud detections. With this in mind, we understand that fraudulent transaction are purposely crafted to blend in with normal transaction. Thus, we wanted to develop a model that is trained on normal transaction to compare to fraud transaction to see where the threshold lies that separates the two transactions. We want to emphasize that we were more focused on the precision score based on the business reason of not wanting to cause panic due to false positives, which can disrupt the customers. 

We believe the with additional data visualization and fine-tuning of the model architecture can yield better results. 
