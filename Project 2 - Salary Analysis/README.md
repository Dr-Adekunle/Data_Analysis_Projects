# Project 2 Data Job Analysis

![Data Science Jobs DashBoard 1](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/38522e273ff43b42fda304fd5c69304c0554437d/Images/Project%202%20-%20Data_Science_Jobs_2023_DashBoard_A.gif)

![Data Science Jobs DashBoard 2](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/38522e273ff43b42fda304fd5c69304c0554437d/Images/Project%202%20-%20Data_Science_Jobs_2023_DashBoard_B.gif)

## Introduction

This analysis was carried out to better understand the data job market and provide insight to job seekers regarding the skills required, the associated renumeration, job schedule and job trends across different countries. It is carried out to know the skills in top demand, correlation between acquired skills and renumeration and the salaries associated with the skills in demand.

### Dashboard File  
Here is the dashboard location [Salary Analysis Dashboard](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Project%202%20-%20Salary%20Analysis/Project%202.xlsm).  

### Questions to Analyze

1. **How did job postings trend?**
2. **Do the skills in high demand command higher salaries?**
3. **Do more skills mean more pay?**
4. **How Does salary compare in Canada with the world?**

### Excel Skills utilized for the Analysis

1. Power Query (ETL)
2. Power Pivot/Power Unpivot
3. Data Analysis Expression (DAX)
4. Data Visualization Techniques with Pivot Charts
5. Table Merging
6. Data Modeling
7. Automation with Visual Basic for Applications (VBA)
8. TEXT Function
9. Slicers


### Data Jobs Dataset

The dataset contains over 32,000 real-world data crawled from job sites over time. Its major columns include the job categories, average yearly and hourly salaries, required skills, countries, work schedule types, and benefits such as health insurance and the flexibility to work from home.

[Jobs Dataset](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Datasets/data_jobs_salary_all.xlsx)


## 1. How did job postings trend?

Two charts were used to answer this question. The monthly trend was straightforward, the pivot table technique in Excel was used to correlate a two-column table of months and count of jobs after the dataset was loaded using Power Query. In the case of the weekly trend, a new column of weekdays was added using Excel's TEXT function while a pivot table was used to correlate these days with the count of job postings. Finally, a line chart with a trendline superimposed was used to check how job postings trended within the year while a column chart was used to visualize the weekly activities.

![Trend computations in the background](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Job%20trend%20computations.gif)

![Trend visualization](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Job%20trend%20visuals.gif)


### Analysis Insights

The job openings at the beginning of the year was a little over 3,000 slots, however, this decreased on the average closing with around 2,000 by the last month of the year. The postings peaked in August and generally on weekdays, with considerable declines on weekends. This suggests job seekers should prepare ahead to take advantage of the job waves at the starting and middle parts of the year.


## 2. Do the skills in high demand command higher salaries?

Due to the way the job_skills column was rendered in the original dataset, data_jobs_salary_fact, e.g. ['sql', 'python', 'aws', 'pyspark', 'tableau', 'power bi', 'git'], the following steps were taken to obtain a separate data_jobs_skills_dim table.
1. A new first column was inserted to the job postings table with unique values from 0 - 32,672 to serve as the primary key for further processing
2. In Excel's Power Query, Text Replace function was used to process the job_skills column to remove the single quotes and square brackets
3. The job_skills column was then split into multiple columns with comma (,) as the delimeter to obtain the skills in different columns
4. Power Query's Unpivot function was then used to recombine the different skills into one column, with the rows retaining the corresponding keys in the job_id column
5. The new skills column was trimmed using Excel's Power Query Trim function to remove leading and trailing blank spaces

Excel's data modeling capability was then used to integrate the data_jobs_salary_fact and data_jobs_skills_dim tables in a one-to-many fashion using the relationship between these two tables with the primary key (job_id) column.


![Skills_dim table creation](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Skills_dim_table_create.gif)

![Skills_dim table modeling](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Skills_dim_table_modeling.gif)

Thereafter, Power Pivot was employed to correlate the job skills with their associated median salaries and a combo visualization was created. With median yearly salary sorted on the primary y-axis in a column chart and the skills demand by a line chart on the secondary y-axis, the visualization told a notable story.

![Skills in demand vs median salary table](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Skills_salary_table.gif)

![Skills in demand vs median salary](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Skills_salary_combo.gif)


### Analysis Insights

Findings show that this is not the case. As seen from the bar-line combo chart, though Python and SQL are top skills, the payments associated with them are in the median range. This fact is further enforced by skills such as Spark, AWS and Java which are about the lowest in demand but commanding the highest salaries. This shows that job seekers can also take advantage of skills in emerging technologies such as AWS for cloud while not yet in high demand. Nonetheless, skills like Python, Oracle, and SQL, suggests their critical importance in high-paying data jobs. This insight guides job seekers on the training and educational programs to focus on for the most pay and impactful technologies.



## 3. Do more skills mean more pay?

Having created the data_jobs_skills_dim and related it with the data_jobs_salary_fact as previously described, Excel's Power Pivot was used to create a table correlating the median yearly salary with the average skills required per job for the respective data jobs.

![Pay of skills per job](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Skills_per_job_table.gif)

The Skills per job was computed using Data Analysis Expression (DAX), first by obtaining the total count of the jobs and that of skills using the COUNT function as measures and finding the average using the DIVIDE function. The codes are shown below:

**DAX measure for job count**
```
Job Count =
COUNTA (
data_jobs_salary_fact[job_title_short]
)
```

**DAX measure for skills count**
```
Skills Count =
COUNTA (
data_jobs_skills_dim[job_skills]
)
```

**DAX measure for skills per job**
```
Job per Skill =
DIVIDE(
    [Job Count],
    [Skills Count]
)
```


For this analysis, a combo visualization was created with the primary y-axis as the median yearly salary in a column chart and a line chart for the average skills count on the secondary y-axis. The column chart was sorted it ascending order and a trend line was incorporated to see if there was a positive correlation in median salary as the job skill increases.

![Does more skills mean more pay?](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Skills_per_job_combo.gif)


### Analysis Insights

This is true in the general sense. The combo chart shows a steady increase in skills from 3 to between 5 and 6, corresponding with a steady increase in median salary from about $80K to around $160K. Further, the incorporated trend line shows a positive correlation between both metrics. This is demonstrated by high-end, multiple-skills roles like Senior Data Engineer and Data Scientist while those requiring fewer skills like in the case of Business Analysts offer lower salaries. This insight portrays the importance of acquiring multiple relevant skills, especially for job hunters aiming for higher-paying roles. The visualization tends to suggest that by doubling the skills in relevant areas one could earn about twice as much.



## 4. How Does salary compare in Canada with the world?

To answer this question, Excel's Power Pivot was used to create a table correlating the job titles with the median salary. Three median salary columns were generated, one was left as default without applying filters. The other two were created by applying DAX measures to filter only for jobs available in Canada in one case and the other for jobs outside Canada. These DAX measures are shown below:

**DAX measure for median salary within Canada**
```
Canada = CALCULATE (
    MEDIAN ( data_jobs_salary_fact[salary_year_avg] ),
    FILTER (
        data_jobs_salary_fact,
        data_jobs_salary_fact[job_country] = "Canada"
    )
)
```

**DAX measure for median salary without Canada**
```
Non Canada = CALCULATE (
    MEDIAN ( data_jobs_salary_fact[salary_year_avg] ),
    FILTER (
        data_jobs_salary_fact,
        data_jobs_salary_fact[job_country] <> "Canada"
    )
)
```

![Pivot Table for Canada vs the world](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Canada_world_table.gif)

A clustered bar chart was used to visualize these cases to understand how Canada faired with the rest of the world regarding renumeration of data jobs.

![Bar chart for Canada vs the world](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/65ef4472587e7fe89a653f7c0a0fd806452b488e/Images/Project%202%20-%20Canada_world_chart.gif)


### Analysis Insights

Data jobs such as Data Analysts, Business Analysts, Machine Learning, software and Cloud Engineers are better paid within Canada compared with the rest of the world. Notwithstanding, job seekers should be aware that much more jobs are available in other parts of the world such as the United States, Kingdom, and Arab Emirates. Job roles like Senior Data Engineer and Data Scientist command higher median salaries both within and without Canada, showcasing the global demand for high-level data expertise. These insights are crucial for negotiations, helping professionals and companies align their offers with market standards while considering geographical variations.


## Conclusion

This data analysis using skills in Excel unravels valuable insights about the data science job market. Employing a real-world dataset of job postings curated from multiple job sites for 2023, the analysis of various data job titles shows their associated median salaries, skills required to do the job, the proportion to which a degree is required, working from home is feasible, health insurance is available or experience is needed amongst others across the world. The analysis using Excel tools such as Power Query (ETL) and Power Pivots Modeling and DAX with Data Visualization Techniques with Pivot Charts, amongst others, reveals the best times to job hunt, countries to target based on the job titles. A positive correlation between acquired skills and renumerations and the main skills to target such as Python, SQL and Azure to compete favorably in the data market.
