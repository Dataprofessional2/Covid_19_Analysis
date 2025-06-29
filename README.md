# Covid_19_Analysis

# This repository contains case studies related to the Covid 19 Data Analysis. It includes data collection, data cleaning, analysis, visualization, and insights using tools like Excel, SQL, Python, and Tableau. The goal is to apply real-world data analytics techniques to solve business problems and derive actionable insights.

### Table Of Contents
- Introduction
- Overview of Covid 19 Data Analysis
- Objective
- Data Cleaning & Preparation
- Data Loading and Inspection
- Exploratory Data Analysis (EDA)
- Data Visualization
- Findings 
- Corona Virus Behaviour all over the world

## Project Overview: Covid 19 spread across the world
- I analyzed global COVID-19 data to explore the spread, impact, and trends of the pandemic across countries and regions. Using publicly available datasets (e.g. WHO data, Kaggle COVID-19 datasets), I applied data cleaning, transformation, and visualization techniques to uncover key insights.

Objective : 
- Analyze cases, deaths, and recovery trends at country and regional levels

- Identify countries/regions with the highest mortality rates

- Compare pandemic progression across WHO regions

- Visualize  trends to highlight peaks and waves
 
Tools Used : Python, Excel, SQL, Tableau



### Data Cleaning/Preparation
In the initial data preparation phase, we performed the following tasks:

- Data loading and inspection.
- Standardizing Data
- Headers Naming Convention
- Handling missing values.
- Data cleaning and formatting.



### Exploratory Data Analysis (EDA) :
- Analyze cases, deaths, and recovery trends at country and regional levels

- Identify countries/regions with the highest mortality rates

- Compare pandemic progression across WHO regions

- Visualized trends to highlight peaks and waves



### Data Analysis using SQL
```sql
-- Simply retrieving data from the table
SELECT * FROM covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest LIMIT 1000;
```
```sql
-- Listing out the countries with most deaths in each WHO Region
SELECT WHO_Region, Country, Deaths
FROM covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest AS main
WHERE Deaths = (
  SELECT MAX(Deaths)
  FROM covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest AS sub
  WHERE sub.WHO_Region = main.WHO_Region
)
ORDER BY Deaths;
```
```sql
-- Listing out the countries with most people recovered in each WHO Region
SELECT WHO_Region, Country, Recovered
FROM covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest AS main
WHERE Recovered = (
  SELECT MAX(Recovered)
  FROM covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest AS sub
  WHERE sub.WHO_Region = main.WHO_Region
)
ORDER BY Recovered;
```
```sql
-- Listing out the WHO Region  with most deaths,recovered and confirmed across the world
SELECT * FROM covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest 
order by Country;
SELECT 
  WHO_Region,
  SUM(Deaths) AS Total_Deaths,
  SUM(Confirmed) AS Total_Confirmed,
  SUM(Recovered) AS Total_Recovered
FROM 
  covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest
GROUP BY 
  WHO_Region
ORDER BY 
  Total_Deaths DESC;
```









```sql
-- Highest recovery rate around the world in different WHO region
SELECT 
  WHO_Region,
  ROUND(SAFE_DIVIDE(SUM(Recovered), SUM(Confirmed)) * 100, 2) AS Recovery_Rate_Percent
FROM 
  covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest
GROUP BY 
  WHO_Region
ORDER BY 
  Recovery_Rate_Percent DESC;
```


```sql
-- Highest Death rate around the world in different WHO region
SELECT 
  WHO_Region,
  SUM(Deaths) AS Total_Deaths,
  SUM(Confirmed) AS Total_Confirmed,
  ROUND(SAFE_DIVIDE(SUM(Deaths), SUM(Confirmed)) * 100, 2) AS Death_Rate_Percent
FROM 
  covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest
GROUP BY 
  WHO_Region
ORDER BY 
  Death_Rate_Percent DESC;
```


```sql
-- Countries which didn't reported any deaths during this timeframe
 SELECT Country, Confirmed, Deaths,WHO_Region
FROM covid-analysis-463108.Covid_19_Analysis.Country_Wise_Latest
WHERE Deaths = 0 AND Confirmed > 0
ORDER BY Confirmed DESC
limit 10;
```











## COVID-19 Data Analysis
🔹 Key Questions Addressed
- How did COVID-19 cases, deaths, and recoveries vary across countries and WHO regions?
- Which countries and regions experienced the highest mortality rates?
- What trends emerged over time in the spread of the virus?

  
🔹 Findings Summary
- The highest death counts were concentrated in specific regions (e.g. Americas, Europe), while mortality rates varied significantly by country.
- The progression of cases and deaths showed distinct waves globally, with peaks at different times across regions.
- Some countries had disproportionately high case fatality rates, highlighting differences in healthcare capacity and response.


 
🔹 Recommendations
- Use regional trends to inform preparedness and resource allocation for future outbreaks.
- Strengthen data reporting consistency to enable more accurate cross-country comparisons.
- Apply similar analytical frameworks for monitoring future pandemics or public health crises.




















