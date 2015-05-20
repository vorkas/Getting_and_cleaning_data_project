---
title: "CodeBook"
author: "Stelios Vorkas"
date: "Monday, May 18, 2015"
output: html_document
---


The data consists of a number of measurements taken from a group of 30 individuals. The subjects of the the 
experiment were splited into two groups; a test group and a train group. Each individual performed six activities(walking, walking upstais, walking downstairs, sitting, standing and laying). The measurement were recorded using smartphones attached to each subject's waist.

The measurements comprise of 3-axial linear accelereation and 3-axial angular velocity. The variables of the dataset 
are listed below:


Variables:

"activity": the activity performed by each subject. The variable has six levels (1:walking, 2:walking upstais, 
3:walking downstairs, 4:sitting, 5:standing 6:laying)         

"subject": 1 to 30 each number represents a subject of the experiment           

"X_test": Test set            

"X_train": Train set           

Tri-axial acceleration for test group
"test_acc_x"
"test_acc_y"        
"test_acc_z"        

Tri-axial Angular velocity for test group
"test_gyro_x"       
"test_gyro_y"       
"test_gyro_z"

Tri-axial total acceleration for test group
"test_total_acc_x"  
"test_total_acc_y"  
"test_total_acc_z"  

Tri-axial acceleration for train group
"train_acc_x"       
"train_acc_y"      
"train_acc_z"  

Tri-axial angular velocity for train group
"train_gyro_x"      
"train_gyro_y"      
"train_gyro_z"      

Tri-axial total acceleration for train group
"train_total_acc_x"
"train_total_acc_y" 
"train_total_acc_z"


Method:
The files were first read into R using the scan function. The subjects and activities of the test and train sets
were merged into two single vectors. The test and train files were treated as individual variables and were combined into a single dataframe.
Next the mean and standard deviation of each measurement were calculated. In addition, descriptive names were given to the levels of the activity variable.
Finally the mean for each variable for each activity for each subject were given as an independent tidy dataframe.
