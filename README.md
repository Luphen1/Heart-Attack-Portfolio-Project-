# Heart-Attack-Portfolio-Project-

#### Table of Contents
---------------------

-  [Project Overview](#Project_Overview)

-  [Data Sources](#Data_Sources)

-  [Tools](#Tools)

-  [Data Cleaning/Preparation](#Data_Cleaning/Preparation)

-  [Exploration Data Analysis](#Exploration_Data_Analysis)

-  [Data Analysis](#Data_Analysis)

-  [Results/Findings](#Results/Findings)

-  [Recommendation](#Recommendation)



###  Project Overview
The data project aims to provide an insights about trends and patterns of heart attack across the dataset 

![Screenshot (3)](https://github.com/Luphen1/Heart-Attack-Portfolio-Project-/assets/140397207/a8923162-5c38-40ab-a768-e2bfb299c2e9)

###  Data Sources

Heart Attack:The primary database used for analysis is the  "heart_attack.csv" having the following headers age, gender, impulse, pressure_low, pressure_high, glucose,Kcm,troponin and class

###  Tools
- Excel - is used for data cleaning to check of there are missing values and duplicate records across the spreadsheet
- MySQL - is used to change the data type from age numeric value Column to string data type Column which enhances readibility and simplicity for visualization purposes 
- Power Bi - Creating Report 

###  Data Cleaning/Preparing
In the initial data preparation, I performed the following tasks below;

1. Data loading and inspection
2. Handling for missing value
3. Checking for duplicate values
4. Convert each headers to  the right  data type
5. Outlier Detection and Handling
6. Handling Inconsistent Data and Typos

###  Exploration Data Analysis
EDA involved exploring the heart_attack data to answer key questions such as;

1. What is the age_distribution breakdown?
2. What is the gender breakdown?
3. Find age category by gender in the dataset
4. What is the blood pressure range?
5. Find the average glucose level of age category
6. What is the heart class breakdown by age category?
7. Find age category that has impulse more that average
8. What is the average troponin by age category ?
9. Class breakdown of average impulse and glucose in the dataset
10. What is the age category with glucose variation
11. Find the percentage of pressure rate by age category 

###  Data Analysis
Below are some interesting code/features and cleaning I worked with 

```
USE heart_attack;

```

```
SELECT * FROM heart_attack;

```

```
DESCRIBE heart_attack;

```

```
SET sql_safe_updates= 0;

```

```
SET sql_safe_updates = 1;

```

```
ALTER TABLE heart_attack
ADD age_category text;

```

```
ALTER TABLE heart_attack
DROP age;

```

 ```
 UPDATE heart_attack
SET age_category   =
    CASE
        WHEN age BETWEEN 14 AND 19 THEN 'teenager'
        WHEN age BETWEEN 20 AND 29 THEN 'young_adult'
        WHEN age BETWEEN 30 AND 39 THEN 'adult'
        WHEN age BETWEEN 40 AND 49 THEN 'middle_age'
        WHEN age BETWEEN 50 AND 59 THEN 'senior'
        WHEN age BETWEEN 60 AND 69 THEN 'elder'
        WHEN age BETWEEN 70 AND 103 THEN 'old'
        ELSE NULL
    END;

```
    
 ```
SELECT age_category, COUNT(*) AS count_of_age
FROM heart_attack
GROUP BY age_category
ORDER BY COUNT(*)DESC;

```

```
SELECT gender, gender_count
FROM (
    SELECT gender, COUNT(*) AS gender_count
    FROM heart_attack
    GROUP BY gender
) AS gender;

```

```
SELECT 
    age_category,gender,COUNT(*) AS count_gender
FROM
    heart_attack
    GROUP BY age_category,gender
    ORDER BY COUNT(*) DESC;

  ```

```

SELECT age_category, 
 MAX(pressure_high) - MIN(pressure_low) AS blood_pressure_range
FROM heart_attack
GROUP BY age_category;

```

```

SELECT age_category,ROUND (AVG(glucose),2) AS avg_glucose
FROM heart_attack
GROUP BY age_category;

```

```

SELECT age_category,class, COUNT(*) AS count_of_heart_attack
FROM heart_attack
GROUP BY age_category,class
ORDER BY COUNT(*) DESC;

```

```

SELECT age_category,AVG(impulse) AS avg_category_impulse
FROM heart_attack
GROUP BY age_category
HAVING AVG(impulse) > (SELECT AVG(impulse) FROM heart_attack);

```

```

SELECT age_category,ROUND(
AVG(troponin),2) 
AS avg_troponin
FROM heart_attack
GROUP BY age_category
ORDER BY avg_troponin DESC; 

```

```

SELECT 
    class,
    ROUND(AVG(impulse), 2) AS avg_impulse,
    ROUND(AVG(glucose), 2) AS avg_glucose
FROM
    heart_attack
GROUP BY class;

```

```

SELECT age_Category, ROUND(STDDEV(Glucose),2) AS Glucose_Variation
FROM 
     heart_attack
GROUP BY age_category
ORDER BY Glucose_Variation DESC;

```

```

SELECT
    age_Category,
    (SUM(pressure_high) / (SUM(pressure_high) + SUM(pressure_low))) * 100 AS Pressure_high_Percentage,
    (SUM(pressure_low) / (SUM(pressure_high) + SUM(pressure_low))) * 100 AS Pressure_low_Percentage
FROM heart_attack
GROUP BY age_Category;

```

###  Results/Findings
The analysis results are summarized as follow:

1. Gender Distribution: Females are the most prevalent gender in the dataset, especially among the elderly age group.

2. Glucose Variation: Young adults exhibit the highest variation in glucose levels.

3. Age Distribution: The dataset is predominantly composed of elderly individuals.

4. Impulse: Adults demonstrate the highest impulse above average in the dataset.

5. Average Glucose: Seniors have the highest average glucose levels.

6. High Blood Pressure Risk: Seniors are at the highest risk of high blood pressure.

7. Troponin Levels: Elderly individuals have the highest average troponin levels.

8. Heart Attack Risk: There's a significant risk of heart attacks associated with average glucose levels, particularly among the elderly age group.

9. Blood Pressure and Age Groups: Young adults have the highest percentage of high blood pressure attacks, while teenagers have the lowest percentage of low blood pressure


###  Recommendations:

1. Increase Healthcare Access: Provide more frequent health check-ups for young adults to address and prevent high blood pressure.
   
2. Senior Wellness Program: Implement specialized education programs for seniors to mitigate high blood pressure risks through lifestyle changes.
   
3. Promote Heart Health: Encourage heart-healthy habits across all age groups, including balanced diets and regular exercise.
   
4. Raise Awareness: Launch public campaigns to educate about heart attack risks and high blood pressure prevention.
   
5. Improve Healthcare Accessibility: Ensure accessible healthcare services for all, especially in underserved areas.
   
6. Community Support: Foster family and community support to sustain healthy lifestyle changes.






     

