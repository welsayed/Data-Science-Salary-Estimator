# Data Science Salary Estimator: Overview
* Developed a salary estimation tool (with an MAE of approximately $11,000) to assist data scientists in optimizing their income negotiations upon securing a job position.
* Conducted web scraping of more than 1000 job descriptions from Glassdoor, employing Python and Selenium.
* Engineered key features extracted from the textual content of each job description, enabling the quantification of the importance companies place on skills such as Python, Excel, AWS, and Spark.
* Employed GridsearchCV to fine-tune and optimize Linear, Lasso, and Random Forest Regressors, ultimately achieving the best-performing model.
* Constructed a user-friendly client-facing API utilizing Flask for seamless accessibility.

## Code and Resources Used 
**Python Version:** 3.7  
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, selenium, flask, json, pickle  
**For Web Framework Requirements:**  ```pip install -r requirements.txt```  
**Scraper Github:** https://github.com/arapfaik/scraping-glassdoor-selenium  
**Scraper Article:** https://towardsdatascience.com/selenium-tutorial-scraping-glassdoor-com-in-10-minutes-3d0915c6d905  
**Flask Productionization:** https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2

## Web Scraping
Enhanced the web scraper GitHub repository (mentioned earlier) to extract data from 1000 job listings on Glassdoor.com. For each job posting, the following information was collected:
* Job Title
* Salary Estimate
* Job Description
* Rating
* Company
* Location
* Company Headquarters
* Company Size
* Company Founded Date
* Type of Ownership
* Industry
* Sector
* Revenue
* Competitors

## Data Cleaning
Following the data scraping, a series of data cleaning and transformation steps were undertaken, resulting in the creation of the following variables and changes:
* Extracted numeric data from the salary information.
* Introduced new columns to distinguish between employer-provided salaries and hourly wages.
* Removed rows lacking salary information.
* Extracted and parsed the company's rating from the company text.
* Added a new column to identify the state where the company is located.
* Included a column indicating if the job was located at the company's headquarters.
* Transformed the company's founding date into the age of the company.
* Introduced separate columns for different skills mentioned in the job description:
   * Python
   * R
   * Excel
   * AWS
   * Spark
* Created columns for a simplified job title and seniority level.
* Added a column to represent the length of the job description.

## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the pivot tables. 

![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/salary_by_job_title.PNG "Salary by Position")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/positions_by_state.png "Job Opportunities by State")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/correlation_visual.png "Correlations")

## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 20%.   

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.   

I tried three different models:
*	**Multiple Linear Regression** – Baseline for the model
*	**Lasso Regression** – Because of the sparse data from the many categorical variables, I thought a normalized regression like lasso would be effective.
*	**Random Forest** – Again, with the sparsity associated with the data, I thought that this would be a good fit. 

## Model performance
The Random Forest model far outperformed the other approaches on the test and validation sets. 
*	**Random Forest** : MAE = 11.22
*	**Linear Regression**: MAE = 18.86
*	**Ridge Regression**: MAE = 19.67

## Productionization 
In this step, I built a flask API endpoint that was hosted on a local webserver by following along with the TDS tutorial in the reference section above. The API endpoint takes in a request with a list of values from a job listing and returns an estimated salary. 


