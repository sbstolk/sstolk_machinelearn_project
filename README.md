
===========================
#Introduction
The purpose of this project is to create a predictive model for JawboneUp and FitBit data. The model will predict, based on movement data gathered by the wearable device, the manner in which the exercise was performed. 

#Data Analysis
First, the data was downloaded into two .csv files, containing a training set and a test set respectively. These were stored in the appropriate working directory. 
```r
setwd("C:/Users/Shaylon/Documents/R_programming")
TrainData <- read.csv("./pml-training.csv")
estData <-read.csv("./pml-testing.csv")
```
The 'classe' variable is the target of the prediction. There are 160 variables in total. 
The training set contains 99.9% of the observations (19622 observations) while the test set contains 20 observations. 

#Model Building
