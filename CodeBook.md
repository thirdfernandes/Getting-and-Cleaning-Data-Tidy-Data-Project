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

There are 5 parts:
1) Merges the training and the test sets to create one data set.
2) Extracts only the measurements on the mean and standard deviation for each measurement.
3) Uses descriptive activity names to name the activities in the data set
4) Appropriately labels the data set with descriptive variable names.
5) From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

Load the plyr and data.table libraries.
Load the provided data.
Extract the mean and standard deviation column names and data.
Process the data.
Merge data set.
