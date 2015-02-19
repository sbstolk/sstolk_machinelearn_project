
===========================
#Introduction
The purpose of this project is to create a predictive model for JawboneUp and FitBit data. The model will predict, based on movement data gathered by the wearable device, the manner in which the exercise was performed. 

#Data Preparation
First, the data was downloaded into two .csv files, containing a training set and a test set respectively. These were stored in the appropriate working directory. 
```r
setwd("C:/Users/Shaylon/Documents/R_programming")
TrainData <- read.csv("./pml-training.csv")
estData <-read.csv("./pml-testing.csv")
```
The 'classe' variable is the target of the prediction. There are 160 variables in total. 
The training set contains 99.9% of the observations (19622 observations) while the test set contains 20 observations. 
Before proceeding to analysis and model building, the data was cleaned. The first step was to remove any null values and replace them with zeros. 

```r
TrainData <- TrainData[, colSums(is.na(TrainData)) == 0]
TestData <- TestData[, colSums(is.na(TestData)) == 0]  
```
Since the prediction model will be focused on the information gathered by the accelerometers, there is no need to keep the large number of extraneous coloumns. These were removed as follows: 
```r
classe <- TrainData$classe
trainRemove <- grepl("^X|timestamp|window", names(TrainData))
TrainData <-<- TrainData[, !trainRemove]
TrainData <-TrainData[, !trainRemove]
TrainClean <- TrainData[, sapply(TrainData, is.numeric)
#
testRemove <-grepl("^X|timestamp|window", names(TestData))
TestData <- TestData[, !testRemove]
TestClean <- TestData[, sapply(TestData, is.numeric)]
```
Next, the training data was partitioned into a training set and a validation set so that the efficacy of the model could be evaluated prior to being run on the official test set.

```r
inTrain <- createDataPartition(TrainClean$classe, p=0.70, list=F)
TrainOne <- TrainClean[inTrain, ]
ValidateOne <- TrainClean[-inTrain, ]
```

#Model Building
The RandomForest algorithm was used to build the predictive model. To validate this model, and calculate the out-of-sample error, k-folds cross validation (five folds). 

```r
controlRf <- trainControl(method="cv", 5)
modelRf <- train(classe ~ ., data=TrainOne, method="rf", trControl=controlRf, ntree=250)
```


