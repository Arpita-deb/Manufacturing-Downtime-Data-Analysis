# Manufacturing Downtime Exploratory Data Analysis

This repository contains the files related to the data analysis of Production Line Downtime of a Soda producing company. This project was done as a part of Maven Analytics monthly data challenge for September 2024. The dataset was provided by Maven Analytics.

### What is included in this repository:

1. Problem Statement
2. Original and Working Copy of the datasets
3. Associated data visualizations
4. A project report which contained detailed analysis results

A Medium article is also available [here](https://medium.com/@arpita_deb/manufacturing-downtime-54c409ad24f7).

*********************************************************************************

## Problem:
The primary challenge faced by a soda production line is frequent and prolonged downtime, which negatively impacts operational efficiency. Production line downtime refers to the period during which a manufacturing line is non-operational due to various factors, such as equipment failures, maintenance, or operator errors.

The root causes behind downtime, whether operator-related or mechanical, are not well understood, leading to inconsistent productivity and efficiency across different batches.

## Goals:
The goal of this analysis is to figure out —

* How efficient is the current production line?
* Which operators are underperforming?
* What are the leading causes for line downtime?
* Are certain operators struggling with specific errors? If yes, identify these factors.

## Tools used:

* **Excel** - for data analysis and visualization
* **Canva** - to create the report

## About the dataset:

The dataset covers 38 production batches for 6 soda products from August 29 to September 3, 2024. It includes 4 sheets that give information about batch numbers, product details, operators, production start/end times, and downtime information. Each product has a minimum production time, with 4 operators managing the batches. There are 12 downtime factors, each linked to either operator or machinery errors, and multiple factors may affect a single batch.

**Data Description:**

1. **Line productivity**: Fact table containing details for each batch produced
   | Column | Data Type | Description |
   | :--- | :--- | :--- |
   | Date | Date |	Date the batch was produced |
   |  Product	ID | String | The product produced in the batch |
   |  Batch | String |	Unique ID for the batch produced |
   |  Operator  | String |	Production line operator in charge of the batch |
   |  Start Time | Time |	Time the batch production started |
   |  End Time | Time | Time the batch production ended |

2. **Products**:	Dimension table with details on each product
   | Column | Data Type | Description |
   | :--- | :--- | :--- |
   |  Product | String |	Unique product ID |
   |  Flavor | string |	Soda flavor for the product |
   |  Size | Integer |	Product size (volume) |
   |  Min batch time | Integer |	Minimum time required to produce a batch (with no downtime) |

3. **Line downtime**: Fact table containing downtime (in minutes) by factor for each batch
   | Column | Data Type | Description |
   | :--- | :--- | :--- |
   |  Batch | String |	Unique ID for the batch produced |
   |  Downtime factor | Integer |	Downtime minutes for each factor ID (across columns) |

4. **Downtime factors**:	Dimension table with details on each downtime factor
   | Column | Data Type | Description |
   | :--- | :--- | :--- |
   | Factor | Integer | Unique ID for each downtime factor |
   | Description | String | Downtime factor description |
   | Operator Error | Boolean |	Is this due to operator error? (Yes/No) |

## Analysis Results:

### 1. Current Line Efficiency Patterns:

![0](https://github.com/user-attachments/assets/b30db629-c456-4205-9c56-dae5b474383a)

The table above gives an overview of the performance of 38 batches of productions.

Efficiency is calculated as a ratio of Minimum Batch Time and Actual Batch Time. A higher efficiency means the actual time is close to the minimum. However, the current line efficiency is 67% ranging from 44% to 100%. It reveals potential for improvement in the overall line efficiency.

![1](https://github.com/user-attachments/assets/b4a2756f-fb2e-46c8-bdf2-c78e7a4eaca8)

28 out of 38 batches are performing at a medium level of efficiency between 51 to 80%. Only 5 batches have an efficiency score below 50%, signaling potential problems in the production process.

Identifying the least efficient batches may reveal more insights into the underlying causes for low productivity and efficiency of this production line.

![2](https://github.com/user-attachments/assets/fb3254e7-1fcf-4e76-83ab-b718855857ea)

Upon plotting the efficiency and line downtime data, I got a scatterplot where each dot represents a batch with corresponding efficiency score and downtime minutes. Clearly as downtime increases, efficiency decreases. The correlation score between line efficiency and downtime is about -0.9053 suggesting a strong negative correlation. However, correlation doesn’t always mean causation. Line Downtime could be one of the many reasons for low batch efficiency, but not the sole one.

Nonetheless, line downtime is visibly a culprit in reducing efficiency of the production line.

### 2. Identifying Underperforming Operators:

![4](https://github.com/user-attachments/assets/e65aba62-2118-47cc-9a31-53d9e8b9bace)

Charlie has the highest downtime (384 mins) but a mid-range average downtime (35 mins per batch). Mac has the highest average downtime per batch (42 mins), suggesting Mac’s batches have higher downtime per unit of production.

Mac’s high average downtime (42 minutes) and low efficiency points to potential inefficiency across the batches handled. Even though Charlie has the highest total downtime, his batches are relatively more efficient on average compared to Mac’s. This pattern indicates that Mac might be facing more severe production interruptions per batch, which could be linked to specific downtime factors.

![3](https://github.com/user-attachments/assets/28c01c6a-8db0-4424-a0b0-ff4f6ac33034)

The breakdown of total batch time into downtime and working time reveals that the downtime is roughly proportional to total batch time. In general, as an operator runs a production line longer, he/she will most likely face longer downtime.

The operators in this particular production line spend about 36.24% of their total time in production delays. Identifying the factors responsible for long downtime will help us reduce the percentage of downtime and increase overall productivity.

### 3. Leading Factors for Downtime:
   
![5](https://github.com/user-attachments/assets/5b818f60-b60d-4f6d-bdd4-cb043422caec)

Five out of twelve downtime factors account for the 80.4% of the lost production time, with each causing over 2 hours of delays.

This chart highlights where interventions will have the biggest impact on improving efficiency, namely in machine adjustment, machine failure, inventory shortage, batch change and coding error.

![6](https://github.com/user-attachments/assets/ed676c9b-9580-4d9d-adc3-d49b1e10ded2)

Among the 12 leading downtime factors 6 are associated with operator error which accounts for 56% of total downtime. The rest 44% are related to machine-related error.

This shows that human factors are a bigger source of downtime for this production line. Understanding which operators are struggling with which specific error can help them identify their pain points and suggest ways to address their problems.

### 4. Operators Struggling with Specific Errors:
   
![7](https://github.com/user-attachments/assets/491a14e6-1fd2-49c8-b984-eb8cecff0c82)

Charlie struggles with a wide range of factors (10 out of 12), particularly with Machine Adjustment and Machine Failure. Dee faces downtime across 11 factors, similar to Charlie, with Machine Adjustment and Inventory Shortage as being primary issues. Dennis’s primary issues are Machine Adjustment and Machine Failure, but his downtime is spread across fewer factors (6 of 12). Mac struggles with Batch Change (130 mins), and Inventory Shortage (80 mins).

This chart highlights a clear pattern where the majority of operators are consistently affected by the same three key downtime factors: machine adjustments, machine failures, and inventory shortages.

## Summary:

* The current line efficiency is 67%.
* Downtime has a strong negative correlation with efficiency (-0.9053).
* An average one-hour batch faces 36 minutes of downtime.
* Charlie has the highest total downtime (384 mins) but moderate average downtime (35 mins/batch).
* Mac is the least efficient operator (63%) with an average downtime of 42 mins per batch.
* Operators spend 36.24% of their total time in production delays.
* Batch changes and machine adjustments are frequent operator-related issues causing major downtime.
* Machine failures and inventory shortages contribute significantly to downtime but are not operator errors.
* Most operators are affected by machine adjustments, failures, and inventory shortages.

## Recommendations:

* Focus on minimizing Machine Adjustments, Failures, and Inventory Shortages, as these factors significantly contribute to downtime.
* Provide targeted training for operators, especially for Mac and Charlie, to reduce downtime associated with operator errors like Batch Change and Machine Adjustment.
* Consider adjusting batch schedules to balance workloads and minimize downtime for operators like Mac, who experience high average downtime, and improve overall efficiency across the line.
* Introduce preventive maintenance strategies and proactive interventions for frequent machine-related issues to reduce unexpected downtimes and improve line efficiency.

By addressing these core areas, especially operator-related downtime factors, the company can expect to see higher efficiencies and reduced production interruptions.

## Limitations of the analysis:

1. Since the dataset is smaller, we cannot generalize the findings.
2. I haven't taken account of the affect of various products on production downtime and operator efficiency.

## Appendix:

* A Medium article is also available [here](https://medium.com/@arpita_deb/manufacturing-downtime-54c409ad24f7).

