# ETL Project

## Summary
The main objective of this analysis is to determine where bank deserts are located in the United States and populations affected by the lack of financial services in their area. Exploring who borrows, where they borrow and why. This analysis will be covering demographics and bank metrics for year 2017 (partial analysis of 2019 is presented as well) in 3,142 U.S. counties, excluding Puerto Rico.

### Data Extraction
Three data sources were utilized to compile database:
* **For bank metrics**, quartely data from the FDIC Financial Data was utilized . CSV files can be extracted [here](https://www5.fdic.gov/idasp/advSearch_warp_download_all.asp?intTab=1) \,
* **For demographics**, data from the 2017 estimates American Community Survey (2010 U.S. Census) was utilized. CSV files can be extracted [here](https://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml)\n",
* **For unemployment and median household income**, data from the Bureau of Labor Statistics - LAUS data was utilized. Excel files can be extracted [here](https://www.bls.gov/lau/)"
 
### Data Transformation
 For each source:
 * Selected the variables of interest for the analysis
 * Eliminated any duplicates or null values
 * Summed quartely values to obtain annual observations for bank metrics
 * Note: For details on data transformation, please refer to the \"Data_Transformation.ipynb\" file*
 
 ### Data Loading
 Financial Deserts database were created in SQL, containing:
 * Demographics data information, using FIPS as primary key
 * Income and unemployment, using FIPS and State as primary keys
 * Bank metrics
 
 ## Statistical Summary
 
 #Set dependencies
import pandas as pd
import numpy as np
import warnings
warnings.filterwarnings('ignore')
#Load the transformed files
population="Population.csv"
education="Eductation.csv"
hh_income="HouseholdIncome.csv"
income_unemployment="Income_Unemployment_2017.csv"
internet_access = "InternetAccess.csv"

#Read the files
df_population = pd.read_csv(population)
df_education = pd.read_csv(education)
df_hh_income = pd.read_csv(hh_income)
df_income_unemployment= pd.read_csv(income_unemployment)
df_internet_access= pd.read_csv(internet_access)
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [],
   "source": [
    "#Set dependencies\n",
    "import pandas as pd\n",
    "import numpy as np\n",
    "import warnings\n",
    "warnings.filterwarnings('ignore')\n",
    "#Load the transformed files\n",
    "population=\"Population.csv\"\n",
    "education=\"Eductation.csv\"\n",
    "hh_income=\"HouseholdIncome.csv\"\n",
    "income_unemployment=\"Income_Unemployment_2017.csv\"\n",
    "internet_access = \"InternetAccess.csv\"\n",
    "\n",
    "#Read the files\n",
    "df_population = pd.read_csv(population)\n",
    "df_education = pd.read_csv(education)\n",
    "df_hh_income = pd.read_csv(hh_income)\n",
    "df_income_unemployment= pd.read_csv(income_unemployment)\n",
    "df_internet_access= pd.read_csv(internet_access)\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [],
   "source": [
    "count_counties = df_income_unemployment[\"County\"].count()\n",
    "total_population= df_population[\"pop_total\"].sum()\n",
    "female_pop = df_population[\"pop_female\"].sum()\n",
    "male_pop = df_population[\"pop_male\"].sum()\n",
    "summary=pd.DataFrame([{\"Total Number of Counties\": count_counties, \"Total Population\": total_population, \n",
    "                       \"Female Population\":female_pop, \"Male Population\":male_pop}])\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th>Summary_Table</th>\n",
       "      <th>0</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Female Population</th>\n",
       "      <td>126852354</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Male Population</th>\n",
       "      <td>119526965</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Total Number of Counties</th>\n",
       "      <td>3141</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Total Population</th>\n",
       "      <td>321004407</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "Summary_Table                     0\n",
       "Female Population         126852354\n",
       "Male Population           119526965\n",
       "Total Number of Counties       3141\n",
       "Total Population          321004407"
      ]
     },
     "execution_count": 26,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "summary=summary.rename_axis('Summary_Table')\n",
    "\n",
    "summary_T= summary.T\n",
    "summary_T\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
