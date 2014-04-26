

```r
# install 'reshape2' package if required
if (!require("reshape2")) {
    install.packages("reshape2")
}
```

```
## Loading required package: reshape2
```

```r

# load 'share2' package (to allow use of 'melt' and 'dcast')
library("reshape2")

# import test files
test_subjects <- read.table("./UCI HAR Dataset/test/subject_test.txt")
test_activities <- read.table("./UCI HAR Dataset/test/y_test.txt")
test_data <- read.table("./UCI HAR Dataset/test/X_test.txt", nrows = 2947)

# import train files
train_subjects <- read.table("./UCI HAR Dataset/train/subject_train.txt")
train_activities <- read.table("./UCI HAR Dataset/train/y_train.txt")
train_data <- read.table("./UCI HAR Dataset/train/X_train.txt", nrows = 7352)

# import additional files used for naming
activity_labels <- read.table("./UCI HAR Dataset/activity_labels.txt")
features <- read.table("./UCI HAR Dataset/features.txt")

# rename columns
colnames(test_subjects) <- "subject"
colnames(test_activities) <- "activity"
colnames(test_data) <- features[, 2]
colnames(train_subjects) <- "subject"
colnames(train_activities) <- "activity"
colnames(train_data) <- features[, 2]

# subset test_data
select_test_mean <- grep("mean()", names(test_data), fixed = TRUE)
select_test_std <- grep("std()", names(test_data), fixed = TRUE)
test_mean <- test_data[select_test_mean]
test_std <- test_data[select_test_std]

# subset train_data
select_train_mean <- grep("mean()", names(train_data), fixed = TRUE)
select_train_std <- grep("std()", names(train_data), fixed = TRUE)
train_mean <- train_data[select_train_mean]
train_std <- train_data[select_train_std]

# create single test data frame
test_df <- cbind(test_subjects, test_activities, test_mean, test_std)

# create single train data frame
train_df <- cbind(train_subjects, train_activities, train_mean, train_std)

# create single data frame containing all data
complete_df <- rbind(train_df, test_df)

# convert activity column from integer to factor
complete_df$activity <- as.factor(complete_df$activity)

# change activity labels from numbers to descriptive names
levels(complete_df$activity) <- activity_labels[, 2]

# melt data
molten_df <- melt(complete_df, id = c("subject", "activity"))

# generate means in final tidied data frame
tidied_df <- dcast(molten_df, subject + activity ~ variable, mean)

# generate .txt file
write.table(tidied_df, "./tidy.txt")
```


