# DS4002-Project2

## Contents of Repository
This repository contains the code and documentation for conducting forecasting on unisex baby name trends. This repository contains a README file, LICENSE file, SCRIPTS folder, DATA folder, and OUTPUT folder. 

## Section 1: Software and Platform Section
- Software Used: RStudio (R)
- Packages Used: tidyverse, ggplot2, tree, randomForest, dplyr, tidyr, rpart
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
2. In R, upload the tidyverse, ggplot2, tree, randomForest, dplyr, tidyr, rpart packages
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

*TEST ASSUMPTIONS FOR HYPOTHESIS TESTING:*
1. In R, read in the updated csv file containing the data set with the sentiment scores
2. Use the Department Name column (containing different clothing types) to create three separate data frames containing only bottoms, only tops, and only dresses
  - The dplyr package is useful when doing this
3. Pull out only the compound sentiment scores for bottoms, tops, and dresses separately into three different vectors
4. Create a new data frame with the compound sentiment scores in one column and the clothing type (whether the item is a top, dress, or bottom) in the other column
5. Apply the aov() ANOVA function on our data
6. Create a qqplot to check the normality assumption for ANOVA (points should follow the line of normality if our data is normal)
7. Use the Bartlett test to check for constant variance within our data (the p-value should be less than 0.05 if our data has constant variance)

*ASSUMPTIONS NOT MET --- TURN TO NON-PARAMETRIC HYPOTHESIS TESTING*
1. First construct boxplots to visually compare the compound sentiment scores for tops, pants, and dresses with each other (just to get an idea of what we are working with)
2. Conduct the Kruskal-Wallis Test on all three groups of clothing items

*KRUSKAL-WALLIS TEST SIGNIFICANT --- CONDUCT FOLLOW-UP PAIRWISE TESTING:*
1. Use the PMCMR package on our data to conduct Dunn's Test for follow-up pairwise testing
  - This test will compare every possible pairing between the three groups of clothing items to see if their compound sentiment scores are different across their medians


