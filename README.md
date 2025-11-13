# 🌍 Global Education Data Analysis using BigQuery

This project explores global education statistics using the **World Bank International Education** dataset available in **Google BigQuery**. It demonstrates how SQL can be used to clean, aggregate, and analyze international education data to uncover insights about global learning trends.

---

## 📊 Dataset Overview

**Dataset:** [`bigquery-public-data.world_bank_intl_education`](https://console.cloud.google.com/marketplace/product/world-bank/world-bank-intl-education)

This dataset comes from the World Bank and includes education-related indicators for countries worldwide — such as literacy rates, enrollment ratios, and population by education age group.

**Main Tables Used:**
- `international_education` → contains country-year indicator values  
- `country_summary` → provides metadata such as region, income group, and country code  
- `series_summary` → describes each education indicator  

---

## 🔍 Data Analysis Process
Use **BigQuery SQL** to analyze and visualize education trends across regions of the world.  

1. **Define Question** – Identify the education indicator and year of interest.  
2. **Explore Data** – Inspect dataset tables and understand schema.  
3. **Filter & Join** – Combine `international_education` with `country_summary`.  
4. **Aggregate** – Use SQL functions like `SUM()` to group by region.  
5. **Analyze & Visualize** – Interpret results with charts or summaries.  
6. **Extend** – Form new questions for deeper analysis.

## 📌 Analysis 1 – Population of Official Age for Secondary Education (2015)

### 💡 Research Question
> **"In 2015, how many people were of the official age for secondary education, broken down by region of the world?"**

```sql
SELECT
    summary.region,
    SUM(edu.value) AS secondary_edu_population
FROM
    `bigquery-public-data.world_bank_intl_education.international_education` AS edu
INNER JOIN
    `bigquery-public-data.world_bank_intl_education.country_summary` AS summary
ON edu.country_code = summary.country_code
WHERE
    summary.region IS NOT NULL
    AND edu.indicator_name = 'Population of the official age for secondary education, both sexes (number)'
    AND edu.year = 2015
GROUP BY
    summary.region
ORDER BY
    secondary_edu_population DESC;
```
---

## 🗃️ Output

| Region | Secondary_Edu_Population |
|-------------------------------|--------------------------:|
| South Asia                     | 237,541,684              |
| East Asia & Pacific            | 172,016,129              |
| Sub-Saharan Africa             | 135,639,085              |
| Europe & Central Asia          | 70,181,959               |
| Latin America & Caribbean      | 67,937,467               |
| Middle East & North Africa     | 44,318,682               |
| North America                  | 27,003,321               |

---

## 📈 Insights

1. **East Asia & South Asia** have the largest populations of secondary-school-age children, reflecting high population and education demand.  
2. **Sub-Saharan Africa** shows rapid growth in youth population, indicating a need for expanded educational infrastructure.  
3. **Europe & Central Asia** and **Latin America** have smaller youth populations but high access to education.  
4. **North America** has fewer children in this age group, with high enrollment rates.
   
📚 These results highlight regions where education policies and resources should be prioritized.
