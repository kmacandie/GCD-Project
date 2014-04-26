# Getting and Cleaning Data
## Peer Assessment
### `run_analysis.R`

The file 'run_analysis.R' is an R script that processes the contents of the zip file 'UCI HAR Dataset.zip' and generates a text file called 'tidy.text' that contains a tidy data set which represents a summary of a portion of the data contained within the zip file.

The zip file must be in the working directory for the script to execute. (The script checks for the presence of the zip file).

The script requires the `reshape2` package, which will be installed and loaded automatically if necessary.

The original data and a description of the data can be downloaded from the following link:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones#

The script performs the following functions:

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive activity names. 
5. Creates a second, independent tidy data set with the average of each variable for each activity and each subject. 

An understanding of how the script works can be obtained by reading the comments contained within the code.

A detailed description of the variables is contained within the 'features_info.txt' file inside the zip file.
