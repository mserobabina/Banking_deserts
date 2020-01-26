# ETL Project

## Summary
The main objective of this analysis is to determine where bank deserts are located in the United States and populations affected by the lack of financial services in their area. Exploring who borrows, where they borrow and why. This analysis will be covering demographics and bank metrics for year 2017 (partial analysis of 2019 is presented as well) in 3,142 U.S. counties, excluding Puerto Rico.

### Data Extraction
Three data sources were utilized to compile database:
* **For bank metrics**, quarterly data from the FDIC Financial Data was utilized . CSV files can be extracted [here](https://www5.fdic.gov/idasp/advSearch_warp_download_all.asp?intTab=1)
* **For demographics**, data from the 2017 estimates American Community Survey (2010 U.S. Census) was utilized. CSV files can be extracted [here](https://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml)
* **For unemployment and median household income**, data from the Bureau of Labor Statistics - LAUS data was utilized. Excel files can be extracted [here](https://www.bls.gov/lau/)
 
### Data Transformation 
 For each source: 
 * Selected the variables of interest for the analysis
 * Eliminated any duplicates or null values
 * Summed quartely values to obtain annual observations for bank metrics
 
 _Note: For details on data transformation, please refer to the \"Data_Transformation.ipynb\"_
 
 ### Data Loading
 Financial Deserts database were created in SQL, containing:
 * Demographics data information, using FIPS as primary key
 * Income and unemployment, using FIPS and State as primary keys
 * Bank metrics
 
 ## Statistical Summary
 ![Test Image 3](https://github.com/mserobabina/Banking_deserts/blob/master/ETL%20Project/jupyter.PNG)
