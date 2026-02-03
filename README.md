This repository contains analysis code and information for BIOS6624.
The file structure TBD

File structure:
Project0.rmd: main analysis file containing r code and results
Project0_clean_v2.csv: raw data file provided by the investigator
readme.md: project documentation and cleaning notes

## Data preprocessing notes for Project0.rmd: 
- The initial data cleaning focused on standardizing time variables and removing unnecessary data columns to simplify the analysis.

### Column selection and cleaning:
The following steps were taken to prepare the data based on investigator requirements:
- Removed sample interval columns because the calculation accuracy was unknown
- Removed hormone measures in ug/dl and pg/dl to focus on nmol/l units
- Converted empty strings to proper missing values so time data could be filled
- Renamed the booklet clock time column to fix a typo in the original file

### Technical adjustments:
- used na.strings to ensure empty cells were treated as missing values
- filled wake times for all samples based on the first reported time of the day
- used the lubridate package to convert clock strings into numeric minutes since midnight
- created new variables to measure minutes since waking for both paper and electronic records

### Missing data analysis
- created table to summarize missingness
- reported counts and proportions for each primary variable

## Question 1 Analysis
this section evaluates the agreement between Booklet and MEM times

### analysis steps
- filtered data for samples with both time measures
- calculated bias as the difference between booklet and cap minutes
- measured pearson correlation between the two timing methods
- summarized bias statistics to check for systematic recording errors

### visualizations
- created a histogram to show the distribution of time differences
- produced a scatterplot to visualize agreement
- added a correlation label and legend
- adjusted font sizes and theme

## Research Question 1: Agreement Analysis
This section evaluates whether subject-reported booklet times match electronic monitoring cap times.

### Statistical Modeling & Selection
* **Model 1 (Random Intercept):** Evaluated baseline bias across subjects while accounting for repeated measures. 
  * *Result:* Significant average bias of -6.5 minutes ($p = 0.029$).
* **Model 2 (Random Slope):** Tested if recording accuracy is different for each subject over time. 
  * *Result:* Model had a correlation of 1.00 between intercept and slope, indicating over-parameterization.
* **Comparison:** A Likelihood Ratio Test gave a p-value of **0.058**, suggesting the random slope does not significantly improve the fit.

### Key Conclusions
* **Bias:** Subjects report times roughly 6.5 minutes earlier than cap events.
* **Accuracy:** The agreement slope of **0.995** indicates strong agreement between the two times. 

## Table 1: Comprehensive Study Overview
This table serves as the primary data quality check for the investigator by documenting:
* **Stratified Missingness: Identifies missing data by source. .

* **Biological Validation: Calculates the mean and standard deviation for Cortisol and DHEA at each interval. 

* **Reporting Bias: Calculates the mean difference between booklet and electronic times specifically for each sample. 

## Question 2 Analysis: 
* **Adherence Metrics:** Calculated protocol adherence across two windows (7.5 and 15 mins)
* **Behavioral Trends:** Identified the average magnitude and direction of timing errors
* **Visualization:** Provided boxplots to visualize the distribution of timing deviations relative to the protocol targets

## Question 3 Analysis:
This section prepares the biological data for modeling the diurnal change of Cortisol and DHEA.

### Data Cleaning Steps
* **Cortisol (nmol/L):** * Removed all observations > 80 nmol/L to eliminate likely laboratory errors.
* **DHEA (nmol/L):** * Excluded specific samples at the detection limit (5.205 nmol/L).
    * Conducted subject-level filtering: Participants with more than one sample at the detection limit were excluded from DHEA analysis entirely