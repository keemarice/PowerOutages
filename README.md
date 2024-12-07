
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

<iframe
  src="assets/outage_map.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>




## Framing a Prediction Problem

## Baseline Model

## Final Model
To be made
<iframe
  src="assets/decision_tree.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


=======
