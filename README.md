---
title: "Getting and Cleaning Data Project
Activity Recognition Using Smartphones Dataset"
author: "Stelios Vorkas"
date: "Thursday, March 05, 2015"
output: html_document
---

The aim of this project is to combine a list of data files into a single dataset and obtain some summary statistics such as the mean and the standard deviation. The data files that are going to be used contain data from a series of experiments performed by Università degli Studi di Genova[1]. The experiments were carried out by 30 volunteers. Each person performed six activities(walking,walking upstairs,walking downstairs,sitting,standing,laying) having a smartphone on their waist that recorded different measurements.  
Using the smartphone's embedded accelerometer and gyroscope, 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz were recorded. The obtained dataset was randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.

1] "activity"          "subject"           "X_test"            "X_train"           "test_acc_x"       
 [6] "test_acc_y"        "test_acc_z"        "test_gyro_x"       "test_gyro_y"       "test_gyro_z"      
[11] "test_total_acc_x"  "test_total_acc_y"  "test_total_acc_z"  "train_acc_x"       "train_acc_y"      
[16] "train_acc_z"       "train_gyro_x"      "train_gyro_y"      "train_gyro_z"      "train_total_acc_x"
[21] "train_total_acc_y" "train_total_acc_z"


The objective of the following script is to merge the training and the test sets to create one data set.
Extract the measurements on the mean and standard deviation for each measurement. 
Uses descriptive activity names to name the activities in the data set
Appropriately labels the data set with descriptive variable names and finaly create an independent tidy data set with the average of each variable for each activity and each subject.

##Read test data
##triaxial body acceleration 
test_acc_x<-scan("UCI HAR Dataset/test/body_acc_x_test.txt")   
test_acc_y<-scan("UCI HAR Dataset/test/body_acc_y_test.txt")
test_acc_z<-scan("UCI HAR Dataset/test/body_acc_z_test.txt")

##triaxial angular velocity from gyroscope
test_gyro_x<-scan("UCI HAR Dataset/test/body_gyro_x_test.txt")
test_gyro_y<-scan("UCI HAR Dataset/test/body_gyro_y_test.txt")
test_gyro_z<-scan("UCI HAR Dataset/test/body_gyro_z_test.txt")

##subject identifier number
test_subject<-scan("UCI HAR Dataset/test/subject_test.txt")

##total body acceleration
test_total_acc_x<-scan("UCI HAR Dataset/test/total_acc_x_test.txt")
test_total_acc_y<-scan("UCI HAR Dataset/test/total_acc_y_test.txt")
test_total_acc_z<-scan("UCI HAR Dataset/test/total_acc_z_test.txt")

##Test set
X_test<-scan("UCI HAR Dataset/test/X_test.txt")

##activity labels (1:walking,2:walking upstairs,3:walking downstairs,4:sitting,5:standing,6:laying)
y_test<-scan("UCI HAR Dataset/test/y_test.txt")

##Read training data 
##triaxial body acceleration 
train_acc_x<-scan("UCI HAR Dataset/train/body_acc_x_train.txt")   
train_acc_y<-scan("UCI HAR Dataset/train/body_acc_y_train.txt")
train_acc_z<-scan("UCI HAR Dataset/train/body_acc_z_train.txt")

##triaxial angular velocity from gyroscope
train_gyro_x<-scan("UCI HAR Dataset/train/body_gyro_x_train.txt")
train_gyro_y<-scan("UCI HAR Dataset/train/body_gyro_y_train.txt")
train_gyro_z<-scan("UCI HAR Dataset/train/body_gyro_z_train.txt")

##subject identifier number
train_subject<-scan("UCI HAR Dataset/train/subject_train.txt")

##total body acceleration
train_total_acc_x<-scan("UCI HAR Dataset/train/total_acc_x_train.txt")
train_total_acc_y<-scan("UCI HAR Dataset/train/total_acc_y_train.txt")
train_total_acc_z<-scan("UCI HAR Dataset/train/total_acc_z_train.txt")

##Train set
X_train<-scan("UCI HAR Dataset/train/X_train.txt")

##activity labels (1:walking,2:walking upstairs,3:walking downstairs,4:sitting,5:standing,6:laying)
y_train<-scan("UCI HAR Dataset/train/y_train.txt")

##create a single data frame
library(dplyr)
subject<-c(test_subject,train_subject)  ##create a single vector that contains both the test and train participants
activity<-c(y_test,y_train)  ##create a single vector of the activitis performed by both the test and train subjects

##merge train and test data to create a single data set
data<-cbind(subject,activity,X_test,X_train,test_acc_x,test_acc_y,test_acc_z,test_gyro_x,test_gyro_y,test_gyro_z,test_total_acc_x,test_total_acc_y,test_total_acc_z,train_acc_x,train_acc_y,train_acc_z,train_gyro_x,train_gyro_y,train_gyro_z,train_total_acc_x,train_total_acc_y,train_total_acc_z)
data<-as.data.frame(data)
data<-tbl_df(data)
##remove unecessary objects from global environment
rm(test_subject,train_subject,subject,activity,X_test,X_train,test_acc_x,test_acc_y,test_acc_z,test_gyro_x,test_gyro_y,test_gyro_z,test_total_acc_x,test_total_acc_y,test_total_acc_z,train_acc_x,train_acc_y,train_acc_z,train_gyro_x,train_gyro_y,train_gyro_z,train_total_acc_x,train_total_acc_y,train_total_acc_z,y_test,y_train)
##extract mean and standard deviation for each measurement
mean_data<-summarize(data,mean(X_test),mean(X_train),mean(test_acc_x),mean(test_acc_y),mean(test_acc_z),mean(test_gyro_x),mean(test_gyro_y),mean(test_gyro_z),mean(test_total_acc_x),mean(test_total_acc_y),mean(test_total_acc_z),mean(train_acc_x),mean(train_acc_y),mean(train_acc_z),mean(train_gyro_x),mean(train_gyro_y),mean(train_gyro_z),mean(train_total_acc_x),mean(train_total_acc_y),mean(train_total_acc_z))
sd_data<-summarize(data,sd(X_test),sd(X_train),sd(test_acc_x),sd(test_acc_y),sd(test_acc_z),sd(test_gyro_x),sd(test_gyro_y),sd(test_gyro_z),sd(test_total_acc_x),sd(test_total_acc_y),sd(test_total_acc_z),sd(train_acc_x),sd(train_acc_y),sd(train_acc_z),sd(train_gyro_x),sd(train_gyro_y),sd(train_gyro_z),sd(train_total_acc_x),sd(train_total_acc_y),sd(train_total_acc_z))
##replace levels of activity with descriptive activity names
data$activity<-factor(data$activity,levels=c(1,2,3,4,5,6),labels=c("walking","walking upstairs","walking downstairs","sitting","standing","laying"))

##group data by activity and subject
grouped_data<-group_by(data,activity,subject)
##return the average for each variable for each activity and each subject
avg_act_subj<-summarize(grouped_data,mean(X_test),mean(X_train),mean(test_acc_x),mean(test_acc_y),mean(test_acc_z),mean(test_gyro_x),mean(test_gyro_y),mean(test_gyro_z),mean(test_total_acc_x),mean(test_total_acc_y),mean(test_total_acc_z),mean(train_acc_x),mean(train_acc_y),mean(train_acc_z),mean(train_gyro_x),mean(train_gyro_y),mean(train_gyro_z),mean(train_total_acc_x),mean(train_total_acc_y),mean(train_total_acc_z))

write.table(avg_act_subj,file="tidy dataset.txt",row.name=FALSE)



[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012

This dataset is distributed AS-IS and no responsibility implied or explicit can be addressed to the authors or their institutions for its use or misuse. Any commercial use is prohibited.

Jorge L. Reyes-Ortiz, Alessandro Ghio, Luca Oneto, Davide Anguita. November 2012.
