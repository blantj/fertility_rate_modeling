# Fertility Rate Modeling

## Introduction
I set out to build a model that could classify an NCAA Basketball player's position based on their game statistics and then to determine the feature importances in classifying players.  I scraped the college basketball stats and position data from the Sports Reference website and read it into Pandas, resulting in 4,753 datapoints across 25 feaures after scrubbing.  I modeled the data into 2 classes, Guards and Forwards, using 6 classification models.  The top performing model was a Weighted Soft Voting Classifier that included XGBoost, KNN and Adaboost. This model outperformed the baseline Stratified Dummy Classifier model with a test f1 score of .829 vs. .446. Important features in classifying NCAA Basketball players' positions were Blocks (.28), Offensive Rebounds (.17) and 3 Point Attemps (.11).

## Obtain Data
I obtained my data through SQL queries from BigQuery publicly available datasets. Country feature data came from the World Bank National Indicators database, while the fertility data came from the Census Bureau International database. After merging the two datasets, I had 188 datapoints across 12 features.

## Scrub Data

<a href="url"><img src="https://github.com/blantj/fertility_rate_modeling/blob/main/Images/unscrubbed_df_info.png" align="middle" height="250" width="250" ></a>

In order to scrub my dataset, I first dropped all features where more than 25% of values were missing, as well as other columns with data not needed for EDA or modeling. I next dropped all countries with more than 2 missing columns values in order to avoid having to impute an excessive number of feature values for these rows. I finally filled in all remaining missing values with feature means. After scrubbing, the fertility dataset included 10 features across 169 datapoints.

## Explore Data

<a href="url"><img src="https://github.com/blantj/fertility_rate_modeling/blob/main/Images/class_chart.png" align="middle" height="200" width="250" ></a>

The fertility replacement class dataset was slightly imbalanced with 76 non-replacement fertility rates and 93 replacement fertility rates representing a 55–45 split. I subsequently upsampled the non-replacement fertility rate class with smote in order to achieve class balance.

<a href="url"><img src="https://github.com/blantj/fertility_rate_modeling/blob/main/Images/correlation_heatmap.png" align="middle" height="250" width="250" ></a>

Of the 10 features in the final dataset, 7 had somewhat bell-shaped distributions, while 3 had long tail distributions. While there were some correlation among the dataset features, it did not rise to the point of needing to remove any independent variables as the two most correlated features, Urban Population % and Self Employment %, had a not unreasonable correlation of -.68.

## Model Data

<a href="url"><img src="https://github.com/blantj/fertility_rate_modeling/blob/main/Images/model_performance.png" align="middle" height="200" width="600" ></a>

The baseline fertility replacement classification model, a dummy classifier, had an f1 score of .58 and an accuracy score of .53. The next model I built, a KNN classifier, outperformed the baseline model with an f1 score of .82 and an Accuracy score of .81. The top performing model was the Adaboost model with an f1 score of .85 and an Accuracy score of .84.

## Analyze Results

<a href="url"><img src="https://github.com/blantj/fertility_rate_modeling/blob/main/Images/feature_importances.png" align="middle" height="250" width="250" ></a>

In terms of feature importances, the Adaboost model had several leading features of more or less equal importance. This included Urban Population % and Urban Population Growth, both at .15, followed by Self Employed population, Population Growth Rate and Population Density at .14. Only one feature, GDP Per Capita, was not included in the model at all, while GDP Per Capita Growth had an importance of .02. It appears that the most influential features included a couple features that were possibly correlated, so with more time I would like to try modeling with some of these features removed to see how this affects feature importances.


# Github Files
[Obtain_scrub.ipynb](https://github.com/blantj/fertility_rate_modeling/blob/main/Obtain_scrub.ipynb) :  Obtain and scrub Fertility Replacement Classification data

[Modeling.ipynb](https://github.com/blantj/fertility_rate_modeling/blob/main/Modeling.ipynb) :  Fertility Replacement Classification modeling

# Sources
Sports Reference: https://cloud.google.com/bigquery/public-data
