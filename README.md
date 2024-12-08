
---
## Introduction

In this project, we examine a dataset of major power outages in the U.S. from January 2000 to July 2016 from publicly available datasets from the Department of Energy's (DOE) Office of Electricity Delivery and Energy Reliability, the U.S. Energy Information Administration (EIA), the National Oceanic and Atmospheric Administration (NOAA), the National Climatic Data Center (NCDC), the U.S. Department of Labor, Bureau of Labor Statistics, and the U.S. Census Bureau. This data coalesces information on major outage patterns and characteristics of the U.S. states, like climate and topographic characteristics, electricity consumption patterns, population, and land-cover characteristics. Through this information, it is possible to analyze patterns by state, climate type, and electricity demand. 

The raw data set contains 1534 rows, where each records a different power outage and relevant information. Columns related to this examination are described below:

| Column     |   Description |
|:------------|--------:|
| 'YEAR'   |       Indicates the year when the outage event occurred |
| 'MONTH' |       Indicates the month when the outage event occurred |
| 'U.S._STATE'	 |       Represents all the states in the continental U.S. |
| 'POSTAL.CODE' |       Represents the postal code of the U.S. states |
| 'NERC.REGION'   |      The North American Electric Reliability Corporation (NERC) regions involved in the outage event |
| 'OUTAGE.START.DATE'   |       This variable indicates the day of the year when the outage event started (as reported by the corresponding Utility in the region) |
| 'OUTAGE.START.TIME' |       This variable indicates the time of the day when the outage event started (as reported by the corresponding Utility in the region) |
| 'OUTAGE.RESTORATION.DATE'	 |       This variable indicates the day of the year when power was restored to all the customers (as reported by the corresponding Utility in the region) |
| 'OUTAGE.RESTORATION.TIME'   |       This variable indicates the time of the day when power was restored to all the customers (as reported by the corresponding Utility in the region) |
| 'CAUSE.CATEGORY' |       Categories of all the events causing the major power outages |
| 'OUTAGE.DURATION'	 |       Duration of outage events (in minutes) |
| 'DEMAND.LOSS.MW	' |       Amount of peak demand lost during an outage event (in Megawatt) [but in many cases, total demand is reported] |
| 'CUSTOMERS.AFFECTED'   |       Number of customers affected by the power outage event |

The data can be accessed here: https://engineering.purdue.edu/LASCI/research-data/outages 

In this project, we focus on the following question:

**How long do power outages last before power is restored?**

These questions could give insight into improvements to infrastructure resilience in different states and electrical grids, and the improvement in technology or restoration time from 2000 to 2016. 

---
## Data Cleaning and Exploratory Data Analysis 

### Cleaning
In the beginning, we were given a .xlsx file that we converted into a .csv file.  This made it easier to use the pd.read_csv() function to read and then clean our data.

#### 1. **Loading the Data**
- The dataset `outage.csv` was loaded using `pandas.read_csv()` with the following configurations:
  - **`usecols`**: Selected columns ranging from index 2 to 55 because these were the only relevant columns to us.
  - **`header`**: The header row was specified at index 0.
  - **`skiprows`**: Skipped the first 5 rows of the file to remove description of dataset.

#### 2. **Column Selection**
- From the loaded dataset, we selected the following subset of columns that are relevant for the analysis:
  - **YEAR**: The year of the outage.
  - **U.S._STATE**: The state where the outage occurred.
  - **POSTAL.CODE**: The postal code of the outage location.
  - **NERC.REGION**: The North American Electric Reliability Corporation region.
  - **CAUSE.CATEGORY**: The category describing the cause of the outage.
  - **OUTAGE.DURATION**: The duration of the outage (in minutes).
  - **DEMAND.LOSS.MW**: The megawatts of electricity lost due to the outage.
  - **CUSTOMERS.AFFECTED**: The number of customers affected by the outage.

#### 3. **Removing Extra Rows**
- The first row of the selected columns was removed because it contained metadata instead of actual data.

#### 4. **Handling Missing Values**
- Missing values in critical columns like **YEAR** and **OUTAGE.DURATION** were dropped to ensure regression models were able to be run.
- For other columns, missing values were imputed using the mean of the dataset if a numeric column or marked as "missing" for categorical.

#### 5. **Data Type Conversion**
- Columns were converted to appropriate numeric data types using `pd.to_numeric()`:
- `YEAR`, `OUTAGE.DURATION`, `DEMAND.LOSS.MW`, and `CUSTOMERS.AFFECTED` were converted to float or int for numerical analysis.
---

#### Cleaned Dataset

|    |   YEAR | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CAUSE.CATEGORY     |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |
|---:|-------:|:-------------|:--------------|:--------------|:-------------------|------------------:|-----------------:|---------------------:|
|  1 |   2011 | Minnesota    | MN            | MRO           | severe weather     |              3060 |              nan |                70000 |
|  2 |   2014 | Minnesota    | MN            | MRO           | intentional attack |                 1 |              nan |                  nan |
|  3 |   2010 | Minnesota    | MN            | MRO           | severe weather     |              3000 |              nan |                70000 |
|  4 |   2012 | Minnesota    | MN            | MRO           | severe weather     |              2550 |              nan |                68200 |
|  5 |   2015 | Minnesota    | MN            | MRO           | severe weather     |              1740 |              250 |               250000 |

### Univariate Analysis
<iframe
  src="assets/univariate1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

*Yearly Frequency Histogram: This plot shows the frequency of outages by year in the USA.  There seem to be more outages towards the later years in our dataset.*

<iframe
  src="assets/univariate2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

*Outage Duration Histogram: This plot shows the distribution of power outage durations.  Many of the power outages are pretty short.*

### Bivariate Analysis
<iframe
  src="assets/bivariate1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

*Choropleth Map: Average Power outage duration by state.  The midwest has long power outages!*
<iframe
  src="assets/bivariate3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

*Demand Loss Scatterplot: This scatter plot shows the relationship between demand loss (MW) and the number of customers affected. The majority of outages involve low demand loss (less than 10,000 MW)*

<iframe
  src="assets/bivariate2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

*NERC Regions Bar Chart: This chart shows the number of outages per North American Electric Reliabillity Coporation(NERC) region.  ECAR and FRCC have the most outages from 2000-2016.*

<iframe
  src="assets/outage_map.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

*Interactive Choropleth Map: This map shows the total minutes in outages per state by year.  This has an interactive feature that has a slider based on year.*


### Interesting Aggregates

Average Outage Duration by Year: 

|   YEAR |   OUTAGE.DURATION |
|-------:|------------------:|
|   2000 |          2843.08  |
|   2001 |          1272.07  |
|   2002 |          4751     |
|   2003 |          4652.43  |
|   2004 |          4368.79  |
|   2005 |          5288.94  |
|   2006 |          3329.53  |
|   2007 |          2336.67  |
|   2008 |          4184.02  |
|   2009 |          3660.52  |
|   2010 |          2937.53  |
|   2011 |          1801.61  |
|   2012 |          1877.98  |
|   2013 |          1369.16  |
|   2014 |          3107.36  |
|   2015 |           935.811 |
|   2016 |          2225.55  |

Explain Significance
Describe which imputation technique you chose to use and why. If you didn’t fill in any missing values, discuss why not.

Average Outage Duration by Day of the Week:
| DAY       |   OUTAGE.DURATION |
|:----------|------------------:|
| Monday    |           2117.49 |
| Tuesday   |           2662.57 |
| Wednesday |           3581.18 |
| Thursday  |           2721.42 |
| Friday    |           2718.82 |
| Saturday  |           2402.37 |
| Sunday    |           2278.82 |

Explain Significance
Describe which imputation technique you chose to use and why. If you didn’t fill in any missing values, discuss why not.

---
## Framing a Prediction Problem

This prediction problem focuses on building a **regression model** to predict the **outage duration** of power outages in the USA, measured in minutes. The response variable, **OUTAGE.DURATION**, is crucial for utility companies as it reflects the severity and recovery time of an outage. 

The prediction model uses features that are known at the **time of prediction**, ensuring its practicality in real-world scenarios. These features include:
- **Cause of the outage**: Provides context for why the outage occurred (e.g., weather, equipment failure).
- **Region**: Captures regional characteristics or historical patterns using the NERC region and U.S. state.
- **Year**: Helps account for increasing critical weather events and improvements in outage management over time.
- **Customers affected**: Reflects the scale of the outage, which can influence restoration efforts.
- **Demand loss (MW)**: Indicates the severity of the disruption in terms of energy demand.

The model is evaluated using the **Root Mean Squared Error (RMSE)** metric. RMSE is chosen because it penalizes large errors more heavily, making it ideal for this problem where large deviations in predictions could lead to inefficient resource allocation or extended downtime. We used RMSE over other metrics like MAE, as it emphasizes minimizing significant prediction errors.

By leveraging this approach, the goal is to develop a robust regression model that minimizes prediction errors and provides actionable insights to utility companies. This ensures that the model not only predicts outage durations accurately but also adheres to the constraints of using information available at the time of prediction, enhancing its applicability in real-world operations.


## Baseline Model

<iframe
  src="assets/simpleLinReg.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We created a simple linear regression as our baseline model.  We selected our predictor variable to be "CUSTOMERS.AFFECTED" because it had the highest correlation with "OUTAGE.DURATION".  We fit a simple linear regression with an 80/20 train/test split.  This model, given its simplicity, didn't perform well on our test set.  It had a RMSE of **8350.87**.  Given that this only takes into account one of the variables, we expected our other models to do better.  

---
## Final Model
Given the high error of the simple linear regression, we decided to experiment with other prediction techniques.  These techniques include multiple linear regression, lasso, ridge, and decision trees.  We will explore each model in this next section:

### Multiple Linear Regression
A baseline approach using all selected features. And the error decreased drastically to **4933.434**  We will see later that this model performed the best.  Marginally better than ridge and lasso regression. 

### Lasso Regression
Lasso regression added L1 regularization to our linear model, helping reduce the impact of less significant features by driving their coefficients to zero. We used `GridSearchCV` to tune the regularization parameter (`alpha`), testing multiple values to find the best fit.

- **Root Mean Squared Error (RMSE)**: **4955.11**
- **Most influential features**: `CAUSE.CATEGORY_fuel supply emergency`, `NERC.REGION_MRO`, and `U.S._STATE_Wisconsin`.

### Ridge Regression
Ridge regression used L2 regularization, penalizing large coefficients to prevent overfitting. Similar to Lasso, we tuned `alpha` using `GridSearchCV`.

- **RMSE**: Slightly lower than Lasso, but still worse than the multiple linear regression: **4944.431**
- **Most influential features**: Similar to Lasso, with some additional weight given to features that didn't have weight before: `CAUSE_CATEGORY`

### Decision Trees
We explored non-linear relationships by fitting a Decision Tree Regressor. Hyperparameters such as `max_depth`, `min_samples_split`, and `min_samples_leaf` were optimized using `GridSearchCV`.
- **RMSE**: The highest of all of the advanced models being: **5480.099**

<iframe
  src="assets/decision_tree.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Chosen Model : Multiple Linear Regression 👑

### Model Performance
- **Baseline Model: Simple Linear Regression**:
  - Used a simple linear regression with limited features.
  - Higher RMSE due to insufficient feature representation.
- **Final Model: Multiple Linear Regression**:
  - Incorporating additional features and interaction terms led to a lower RMSE compared to other models like Lasso, Ridge, and Decision Trees.
  - The improvement highlights the importance of capturing relevant information and relationships in the data.

### Why Linear Regression Performed Best
- The relationships between most predictors and the target variable were largely linear, aligning well with the assumptions of Linear Regression.
- Regularization models like Lasso and Ridge may have over-penalized certain coefficients, while decision trees may have overfit smaller patterns, reducing their performance.
- Linear Regression struck the right balance by explaining the variance in the data without unnecessary complexity.  It is difficult to predict outage duration, thus, a general model such as linear regression worked well.

### Conclusion
The Final Model improved performance over the Baseline by leveraging domain-relevant features, interaction terms, and a simple yet effective linear approach that aligned well with the data's underlying tendancies.  For future work, it would be interesting ti see how this model would perform on a dataset with more datapoints for longer outages.  In that case, ridge regression (with a slightly higher RMSE for this dataset) might perform better.

omit later: State the features you added and why they are good for the data and prediction task. Note that you can’t simply state “these features improved my accuracy”, since you’d need to choose these features and fit a model before noticing that – instead, talk about why you believe these features improved your model’s performance from the perspective of the data generating process.

Describe the modeling algorithm you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model’s performance is an improvement over your Baseline Model’s performance.


<iframe
  src="assets/multLinReg.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>







=======
