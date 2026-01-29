This repository contains analysis code and information for BIOS6624.
The file structure TBD

File structure:
Project0.rmd: main analysis file containing r code and results
Project0_clean_v2.csv: raw data file provided by the investigator
readme.md: project documentation and cleaning notes

Data preprocessing notes for Project0.rmd: 
-The initial data cleaning focused on standardizing time variables and removing unnecessary data columns to simplify the analysis.

Column selection and cleaning:
The following steps were taken to prepare the data based on investigator requirements:
-Removed sample interval columns because the calculation accuracy was unknown
-Removed hormone measures in ug/dl and pg/dl to focus on nmol/l units
-Converted empty strings to proper missing values so time data could be filled
-Renamed the booklet clock time column to fix a typo in the original file

Technical adjustments:
-used na.strings to ensure empty cells were treated as missing values
-filled wake times for all samples based on the first reported time of the day
-used the lubridate package to convert clock strings into numeric minutes since midnight
-created new variables to measure minutes since waking for both paper and electronic records


