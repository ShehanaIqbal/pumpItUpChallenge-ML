# PumpItUp Challenge - ML

## Github Link
https://github.com/ShehanaIqbal/pumpItUpChallenge-ML

## Rank : 2101

# Visualization

Data were visualized and analysed with follwing techniques.
- Listing data types of all columns
- Printing the head of dataframes
- Listing the value counts of columns
- Listing unique values of columns
- Plotting bar plots with each label in unique colour
- Printing crosstabs against each other
- Plotting correlation maps including new features
- Ploting confution matrix

# Preprocessing steps & feature engineering

## Filling NaN values

- NaN values of columns with data type 'float' were filled with the mean of respective columns.
- NaN values of other columns of except the column 'scheme_name' were filled with the most occuring values of the respective columns.
- The column 'scheme_name' was removed since nearly 3/4th (35258) of the data rows did not contain a value for 'scheme_name'

## Column removal due to irrelavancy

- 'id' column was removed since it does no contribution towards classification

## Column removal due to redundancy
The following columns were found to be carrying redundant information when compared using crosstab. Hence they were removed from the dataframe.
-  'waterpoint_type',
-  'recorded_by',
-  'wpt_name',
-  'subvillage',
-  'date_recorded',
-  'scheme_name',
-  'installer',
-  'quantity_group',
-  'source_type',
-  'payment_type',
-  'region',
-  'extraction_type_group',
-  'waterpoint_type_group',
-  'quality_group',
-  'management_group'
-  'funder'

## Creating new features
Following new features were created.
  1. 'is_population_high' - if population is greater than the population mean value
  2. 'is_source_spring' - if the source is Spring
  3. 'is_source_shallow_well' - if the source is shallow well
  4. 'is_insufficient_and_soft' - if quantity is insufficient and water_quality is soft
  5. 'is_enough_and_soft' - if the quantity is enough and water_quality is soft
  6. 'water_quality_is_salty' - if water_quality is salty      
  7. 'water_quality_is_unknown' - if water_quality is unknown
  8. 'water_quality_is_soft' - if water_quality is soft
  9. 'amount_tsh_range' - grouping rows based on the value of amount_tsh 
  10. 'gps_height_is_zero' - if gps_height is zero
  11. 'gps_height_less' - if gps_height less than zero
  12. 'gps_height_more' - if gps_height more than zero
  13. 'is_num_private_zero' - if num_private is zero
  14. 'decade' - replacing construction year by the decade that it belongs to
  15. 'is_old_construction'- if construction is old (60s, 70s, 90s)
  16. 'is_new_construction'- if construction belongs to 2000-2009
  17. 'is_quantity_dry' - if quantity is dry
  18. 'is_quantity_enough' - if quantity is enough
  19. 'is_quantity_insuficient' - if quantity is insufficient
  20. 'is_funder_Government_Of_Tanzania' - if funder is Government_Of_Tanzania
  21. 'is_funder_Danida' - if funder is Danida
  22. 'is_funder_rwwsp' - if funder is Rwwsp
  23. 'is_extraction_type_class_gravity' - if extraction type class is gravity
  24. 'is_extraction_type_class_other' - if extraction type class is other
  25. 'is_never_pay' - if payment is 'never pay'

## categorical encoding

- During new feature creation, some important values from some columns were one hot encoded seperately(without encoding the whole column) since there are many other less contributing values in those columns which does not need to be one hot encoded.
- After feature ceration all the columns except the columns of float datatypes were categorically encoded.
- Labels were also categorically encoded.

## Oversampling - handing the imbalanceness of classes

- In order to handle the imbalanceness of test data, training data were oversampled with SMOTE.

## Split the data

- Data were split in the ration of 2:1 for training & testing purposes.

## Data normalization

- Data were normalized using RobustScaler

## Feature selection

- Feature selection was tried with RandomForestClassifier and trained the model with only selected features. Since the model performed poorly compared to training with all features, feature selection was not used to achieve the best accuracy. (But the commented code is available in the model-PumpItUp.ipynb)

# Building and training the model

Following algorithms were tried when choosing the best model.

  1. Random forest
  2. XGBoost
  3. KNN

Since XGBoost performed the best among all the tried out approaches, XGBoost was selected as the best model for training purposes.

# Evaluating the model

### Evaluation metrics used.

  1. accuracy_score - Provides the accuracy of the model
  2. balanced_accuracy_score - Provides the classwise balanced accuracy

Given below is the scores achieved by the submitted (last version) of the model.

    Accuracy:
    =========
    TRAIN: 0.9754318322023442
    TEST: 0.8614146601120957

    Balanced Accuracy:
    ==================
    TRAIN: 0.9754343630754786
    TEST: 0.8613801396006276
    
### Cofusion matrix for test data is given below.

![image](https://user-images.githubusercontent.com/47121844/133824124-89672bdf-29de-41ce-a4d0-07da6d4976f7.png)

### Rank on Drivendata 

file:///home/shehanaiqbal/Pictures/Screenshot%20from%202021-09-15%2022-45-46.png![image](https://user-images.githubusercontent.com/47121844/133824444-affbac3a-cba6-4fdd-8729-069f28b93a3c.png)

