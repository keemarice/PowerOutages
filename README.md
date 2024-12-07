
---

## Introduction

In this project, we examine a dataset of major power outages in the U.S. from January 2000 to July 2016 from publicly available datasets from the Department of Energy's (DOE) Office of Electricity Delivery and Energy Reliability, the U.S. Energy Information Administration (EIA), the National Oceanic and Atmospheric Administration (NOAA), the National Climatic Data Center (NCDC), the U.S. Department of Labor, Bureau of Labor Statistics, and the U.S. Census Bureau. This data coalesces information on major outage patterns and characteristics of the U.S. states, like climate and topographic characteristics, electricity consumption patterns, population, and land-cover characteristics. Through this information, it is possible to analyze patterns by state, climate type, and electricity demand. 

The raw data set contains 1534 rows, where each records a different power outage and relevant information. Columns related to rhis examination are described below:

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
| 'MONTH' |       Indicates the month when the outage event occurred |


The data can be accessed here: https://engineering.purdue.edu/LASCI/research-data/outages 
In this project, we focus on the following question:

How long do power outages before power is restored? 

These questions could give insight into improvements to infrastructure resilience in different states and electrical grids, and the improvement in technology or restoration time from 2000 to 2016. 


## Data Cleaning and Exploratory Data Analysis 

In the beginning, we were given a .xlsx file that we coverted into a .csv file.  This made it easier to use the pd.read_csv() function to read and then clean our data.

### 1. **Loading the Data**
- The dataset `outage.csv` was loaded using `pandas.read_csv()` with the following configurations:
  - **`usecols`**: Selected columns ranging from index 2 to 55.
  - **`header`**: The header row was specified at index 0.
  - **`skiprows`**: Skipped the first 5 rows of the file to remove metadata.

### 2. **Column Selection**
- From the loaded dataset, we selected the following subset of columns that are relevant for the analysis:
  - **YEAR**: The year of the outage.
  - **U.S._STATE**: The state where the outage occurred.
  - **POSTAL.CODE**: The postal code of the outage location.
  - **NERC.REGION**: The North American Electric Reliability Corporation region.
  - **CAUSE.CATEGORY**: The category describing the cause of the outage.
  - **OUTAGE.DURATION**: The duration of the outage (in minutes).
  - **DEMAND.LOSS.MW**: The megawatts of electricity lost due to the outage.
  - **CUSTOMERS.AFFECTED**: The number of customers affected by the outage.

### 3. **Removing Extra Rows**
- The first row of the selected columns was removed because it contained metadata instead of actual data.

### 4. **Handling Missing Values**
- Missing values in critical columns like **YEAR** and **OUTAGE.DURATION** were dropped to ensure completeness.
- For other columns, missing values were filled where applicable.

### 5. **Data Type Conversion**
- Columns were converted to appropriate numeric data types using `pd.to_numeric()`:
  - **YEAR**, **OUTAGE.DURATION**, **DEMAND.LOSS.MW**, and **CUSTOMERS.AFFECTED** were converted to `float` or `int` for numerical analysis.

---

## Resulting Dataset
The resulting cleaned dataset, stored in the `outageClean` DataFrame, includes the following columns:
- **YEAR**
- **U.S._STATE**
- **POSTAL.CODE**
- **NERC.REGION**
- **CAUSE.CATEGORY**
- **OUTAGE.DURATION**
- **DEMAND.LOSS.MW**
- **CUSTOMERS.AFFECTED**

### Features of the Clean Dataset:
- Contains only relevant data with missing values handled appropriately.
- All numeric columns are ready for analysis and modeling.
- Includes a clean and structured dataset for exploratory data analysis (EDA) and predictive modeling.

---

<iframe
  src="assets/outage_map.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/univariate1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>




## Framing a Prediction Problem

## Baseline Model
<iframe
  src="assets/simpleLinReg.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Final Model




=======
