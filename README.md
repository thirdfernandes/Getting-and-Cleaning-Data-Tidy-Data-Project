# Getting-and-Cleaning-Data-Tidy-Data-Project


Instructions

The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set.
Review criterialess 
The submitted data set is tidy.
The Github repo contains the required scripts.
GitHub contains a code book that modifies and updates the available codebooks with the data to indicate all the variables and summaries calculated, along with units, and any other relevant information.
The README that explains the analysis files is clear and understandable.
The work submitted for this project is the work of the student who submitted it.
Getting and Cleaning Data Course Projectless 
The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. You will be graded by your peers on a series of yes/no questions related to the project. You will be required to submit: 1) a tidy data set as described below, 2) a link to a Github repository with your script for performing the analysis, and 3) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Here are the data for the project:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

You should create one R script called run_analysis.R that does the following.

Merges the training and the test sets to create one data set.
Extracts only the measurements on the mean and standard deviation for each measurement.
Uses descriptive activity names to name the activities in the data set
Appropriately labels the data set with descriptive variable names.
From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
Good luck!

Project Steps:
Download the data source. 
The download should give you a UCI HAR DataSet folder.
Place run_analysis.R in the same folder that UCI HAR DataSet is and then set it as the working directory. Run source and it will generate tiny_data.txt in your working directory with the desired text file.

###Copy of Script:

## Goal: to create on R script called run_analysis.R that does the following:

## 1) Merges the training and the test sets to create one data set.
## 2) Extracts only the measurements on the mean and standard deviation for each measurement.
## 3) Uses descriptive activity names to name the activities in the data set
## 4) Appropriately labels the data set with descriptive variable names.
## 5) From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

##Setting working directory after downloading the dataset to the desktop 
setwd("~/Desktop/UCI HAR Dataset")


##Loading useful libraries for merging data sets

library(plyr)

library(data.table)

subjectTrain = read.table('./train/subject_train.txt',header=FALSE)

xTrain = read.table('./train/x_train.txt',header=FALSE)

yTrain = read.table('./train/y_train.txt',header=FALSE)

subjectTest = read.table('./test/subject_test.txt',header=FALSE)

xTest = read.table('./test/x_test.txt',header=FALSE)

yTest = read.table('./test/y_test.txt',header=FALSE)

##The following steps are to help combine the data sets into one data set and organize it

xDataSet <- rbind(xTrain, xTest)

yDataSet <- rbind(yTrain, yTest)

subjectDataSet <- rbind(subjectTrain, subjectTest)

xDataSet_mean_std <- xDataSet[, grep("-(mean|std)\\(\\)", read.table("features.txt")[, 2])]

names(xDataSet_mean_std) <- read.table("features.txt")[grep("-(mean|std)\\(\\)", read.table("features.txt")[, 2]), 2]

##Adding descriptive names to describe the data set better and define all the variables

yDataSet[, 1] <- read.table("activity_labels.txt")[yDataSet[, 1], 2]

names(yDataSet) <- "Activity"

names(subjectDataSet) <- "Subject"

singleDataSet <- cbind(xDataSet_mean_std, yDataSet, subjectDataSet)

names(singleDataSet) <- make.names(names(singleDataSet))

names(singleDataSet) <- gsub('Acc',"Acceleration",names(singleDataSet))

names(singleDataSet) <- gsub('GyroJerk',"AngularAcceleration",names(singleDataSet))

names(singleDataSet) <- gsub('Gyro',"AngularSpeed",names(singleDataSet))

names(singleDataSet) <- gsub('Mag',"Magnitude",names(singleDataSet))

names(singleDataSet) <- gsub('^t',"TimeDomain.",names(singleDataSet))

names(singleDataSet) <- gsub('^f',"FrequencyDomain.",names(singleDataSet))

names(singleDataSet) <- gsub('\\.mean',".Mean",names(singleDataSet))

names(singleDataSet) <- gsub('\\.std',".StandardDeviation",names(singleDataSet))

names(singleDataSet) <- gsub('Freq\\.',"Frequency.",names(singleDataSet))

names(singleDataSet) <- gsub('Freq$',"Frequency",names(singleDataSet))

## Putting the data into a table

Data2<-aggregate(. ~Subject + Activity, singleDataSet, mean)

Data2<-Data2[order(Data2$Subject,Data2$Activity),]

###Copy of CodeBook:

CodeBook

This codebook describes the various data, transformations, variables and other work performed needed to clean up the data.

The data source: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

Data Set Information can be found here: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

The dataset includes the following files:

'README.txt'

'features_info.txt': Shows information about the variables used

'features.txt': List of all features

'activity_labels.txt': Links the class labels with their activity name

'train/X_train.txt': Training set

'train/y_train.txt': Training labels

'test/X_test.txt': Test set

'test/y_test.txt': Test labels

'train/Inertial Signals/total_acc_x_train.txt', 'total_acc_x_train.txt', 'total_acc_z_train.txt':

The acceleration signal from the smartphone accelerometer (depending on the axis) in standard gravity units ('g').

'train/Inertial Signals/body_acc_x_train.txt': Subtract the gravity from the total acceleration

'train/Inertial Signals/body_gyro_x_train.txt': Angular velocity vector measured by the gyroscope for each window sample measured in radians/second.

Transformation details

There are 5 parts: 1) Merges the training and the test sets to create one data set. 2) Extracts only the measurements on the mean and standard deviation for each measurement. 3) Uses descriptive activity names to name the activities in the data set 4) Appropriately labels the data set with descriptive variable names. 5) From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

Load the plyr and data.table libraries. Load the provided data. Extract the mean and standard deviation column names and data. Process the data. Merge data set.

