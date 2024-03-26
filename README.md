# DS4002-Project2

## Contents of Repository
This repository contains the code and documentation for conducting forecasting on unisex baby name trends. This repository contains a README file, LICENSE file, SCRIPTS folder, DATA folder, and OUTPUT folder. 

## Section 1: Software and Platform Section
- Software Used: RStudio (R)
- Packages Used: tidyverse, ggplot2, tree, randomForest, dplyr, tidyr, rpart, rpart.plot
- Platform used: Mac

## Section 2: Map of Documentation 

- Outline or tree of hierarchy of folders and subfolders and list the files stored in each folder
```mermaid
graph TD;
    README.md;
    LICENSE.md;
    SCRIPTS-->unisex_names_project.rmd;
    DATA-->baby-names-state.csv;
    baby-names-state.csv-->UnisexNameData.csv;
    UnisexNameData.csv-->DataAppendix&References;
    OUTPUT-->TotalNumberofBabiesborneachyearwithatop10unisexnamefrom2020bysex.png;
    TotalNumberofBabiesborneachyearwithatop10unisexnamefrom2020bysex.png-->TotalNumberofBabiesborneachyearwithatop10unisexnamefrom2020bysex.png;
    TotalNumberofBabiesborneachyearwithatop10unisexnamefrom2020bysex.png-->TotalNumberofBabiesbornbynameeachyearfrom1910-2020withatop10unisexnamefrom2020.png;
    TotalNumberofBabiesbornbynameeachyearfrom1910-2020withatop10unisexnamefrom2020.png-->TotalNumberofBabiesborneachyearfrom1910to2020andtheirsex.png;
    TotalNumberofBabiesborneachyearfrom1910to2020andtheirsex.png-->TotalNumberofBabiesborneachyearfrom1910-2020withatop10unisexnamefrom2020.png;
```

## Section 3: Instructions for Reproducing Results

GET THE DATA:
1. Download the "baby-names-state" csv file from Data World into your computer
2. In R, upload the tidyverse, ggplot2, tree, randomForest, dplyr, tidyr, rpart, rpart.plot packages
3. Read in the CSV data file and save it as a data frame in R

CLEAN THE DATA:
1. Convert the "name," "sex," and "state_abb" columbs to factor data types
2. Create a "decades" column from the "year" column for each decade of years (ex. 1910-1919)
3. Create a "region" column from the "state_abb" column for the five regions of the US (ex. Northeast)
4. Filter data for only rows with a year = 2020 then filter for names with at least 1/3 babies being female and 1/3 babies born being male to determine unisex names
5. Take the top 10 names from this unisex list based on largest number of babies given the name
6. Filter entire dataset for only those with names in the top 10 unisex list and save dataframe as UnisexNameData.csv

CREATE EXPLORATORY PLOTS FOR EDA:
1. Use ggplot to create different bar plots that will help to visualize our data, where the year is on the x-axis and different variables are on the y-axis for each graph:
  - Count of babies (y-axis) for each year (x-axis)
  - Distribution babies by sex (y-axis) for each year (x-axis)
  - Count of babies for each name (y-axis) for each year (x-axis)
2. Save these plots into the OUTPUT folder

DATA PREP FOR BASIC CLASSIFICATION TREE MODEL BUILDING:
1. Read in the previously cleaned data as a csv file in R
2. Convert the "sex", "name", and "region" variables into factor variable types
3. Remove unnecessary columns from our current data frame -- this should include the "decades" column (which we won't need for analysis), the first column, and the "stat_abb" column
4. Use the uncount() function in R where the "weights" argument is set equal to the "count" column to expand our data based on the count column
   a. After this step each row should represent one single baby in our data set
5. Set the seed using set.seed(4002) --> you can use a random number but make sure to stay consistent throughout the project
6. Split our data set now into a training and a test data set with a 70/30 split

BASIC CLASSIFICATION TREE -- RECURSIVE BINARY SPLITTING:

1. Use the tree::tree(...,data=...) function from the tree library in R to create the first basic classification tree model
2. Apply summary() to the classification tree created above
   a. This will give you the significant variables used, the number of terminal nodes, the residual mean deviance, and also the misclassification error rate of the model (test error rate!)
3. Apply plot() and text() to the classification tree created in (1) to view the graphical output
4. Optional: Use the y response of our data set, the y response of our test data set, the tree we created in (1), the predict() function, and the table() function in R to create a confusion matrix

CLASSIFICATION TREE USING RPART PACKAGE IN R:
1. Use the rpart() and rpart.plot() functions from the rpart and rpart.plot packages in R to create classification trees that are more informative and visually appealing than the basic models we created above
   a. The rpart() method can be used on our data set to actually create the classification tree, while the rpart.plot() method is used to output the classification tree graphically

PRUNE THE CLASSIFICATION TREE:
1. You may need to use the tree::cv.tree() and tree::prune.misclass() functions on our initial basic classification tree model to remove some of the branches, reduce its complexity, or improve its general performance-- pruning a classification tree generally prevents overfitting of the data in the model
   a. Note that in our project, when we pruned the classification tree using our data set and then reapplied the plot() function on our tree to observe its graphical output, our tree looked exactly the same as before pruning-- in this specific case it appears that pruning the classification tree will not lead to significant improvements




