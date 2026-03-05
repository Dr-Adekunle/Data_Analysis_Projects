# Excel Salary Dashboard

![Salary Dashboard 2023](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/741d03c4b98e79ce1fc22196e16e56b787d1624a/Images/Project%201%20-%20Data%20Science%20Information%20Dashboard.gif)  

## Introduction  

This dashboard provides a one-stop shop for job seekers in data science for the positions and number of vacancies available, what to expect for renumeration, the parts of the world these jobs are located, the proportion of entry-level positions and the degree to which certain benefits exists.  

### Dashboard File  
Here is the dashboard location [Salary_Dashboard]("C:\Users\Adekunle\Desktop\Data Projects\Excel\Data_Analysis_Projects\Project 1 - Salary Dashboard\Project 1.xlsx").  

### Excel Skills Utilized  
The following Excel skills were employed in the creation of the dashboard:  

1. Advanced formulas, logical operations, statistical, and dynamic array functions  
2. VLOOKUP, HLOOKUP, XLOOKUP, INDEX, MATCH  
3. Data validation, manipulation, automation, and visualization techniques  
4. Automation using Visual Basic for Applications (VBA)  
5. Storytelling, drawing insights from derived data visualizations    

### Data Jobs Dataset  

The data site contains over 32,000 real-world data crawled from job sites over time. Its major columns include the job categories, average yearly and hourly salaries, required skills, countries, and benefits such as health insurance and the flexibility to work from home.  

[Dataset]("C:\Users\Adekunle\Desktop\Data Projects\Excel\Data_Analysis_Projects\Datasets\data_jobs_salary_all.xlsx")  


## Dashboard Build  

![Computations in the background](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/741d03c4b98e79ce1fc22196e16e56b787d1624a/Images/Project%201%20-%20Computations%20behind%20the%20scene.gif)

Behind the scene, a UNIQUE array of the job titles was created, LOGICAL operations were used to FILTER and AGGREGATE the desired metrics against each job while the XLOOKUP function was used to isolate the specific information to appear on the dashboard. Statistical functions such as MEDIAN and ARITHMETIC computations, nested IF statements were used in other worksheets to obtain the information on the dashboard and make them interact dynamically.  

![Data validation](https://github.com/Dr-Adekunle/Data_Analysis_Projects/blob/741d03c4b98e79ce1fc22196e16e56b787d1624a/Images/Project%201%20-%20Data%20validation.gif)  
  
Bar and Map charts were used to visualize the median salaries of the job titles in monochromatic color scheme for easier readability allowing the immediate understanding of the disparities in global salaries across countries at a glance. Dough nut charts were employed to provide insights into the proportion to which job seekers may apply without a degree, work from home, have access to health insurance or to hourly pay. The information were linked in a way to make all the dashboard charts interactive based on the job title and country selected using data validation which prevent users from entering invalid inputs. Some sample codes used in the build are highlighted below: 


**Sample codes employed**  

**Calculate MEDIAN based on Job title and selected country where yearly salary is available**  
```
=MEDIAN(
IF(
(jobs[job_title_short]=$A15)*(jobs[job_country]=country)*(jobs[salary_hour_avg] <> 0),
jobs[salary_hour_avg]
)
)
```  

**Lookup job count based on the job title selected**
```
=XLOOKUP(title, $A$15:$A$24, $C$15:$C$24)
```  

**Compute the count of jobs based on Job title and selected country in the chart restricted by data validation where the work from home column is TRUE**
```
=COUNTIFS(jobs[job_title_short], $A28, jobs[job_country], country, jobs[job_work_from_home], "TRUE")
```  

## Conclusion

The dashboard was built to provide insights into salary trends across 10 data-related IT jobs based on real-life data crawled from multiple job sites to demonstrate my skills in Excel for Data Analysis. It serves as a guide to job explorers hunting for jobs and provides insights to career paths in the field of data. Data jobs offers between a median yearly salary of $90,000 and $155,000. The high-end salaries typically go to the senior roles. The Data Analyst positions are the most in demand but offering the least renumeration while the Cloud Engineering roles are very scarce. The top countries where these jobs are in-demand includes the United States, United Kingdom and the United Arab Emirates. A larger proportion of the senior-level roles required working from office, having a degree and work experience
