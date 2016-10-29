---
layout: post
title: Project 4 - Fantastic 4 Consultancy - Predicting Data Scientist Salaries via Web Scraping
date: 2016-10-19 02:30:00
summary: Overview and description of my introductory Data Science Immersive project
categories: project dsi python eda web scraping LogisticRegression salary glassdoor
---

Week 4 Project Overview
-----------------------

This week's assignment was a group effort with 3 other classmates, Amish, Jesse and Kristen.

The project was designed to determine the factors which contribute to salaries of Data Scientists being either above the median of all salaries or below. Utilizing web scraping techniques and Logistic Regression (Classification).

Specifically the project required us to:

-	identify public web sources for job listings with Salary data.
-	obtain, via Web Scraping, enough data and features to perform statistical tests
-	clean the data, as necessary
-	develop a reproducible method supported by sound practices for making statements about what features are most influential in position salaries
-	utilize visual and statistical tools to present our recommendations
-	use new statistical tools and functions such as KNeighborsClassifier, GridSearchCV, selenium/phantomJS web tools, LogisticRegression

[Project 4 Jupyter Notebook - Group Submission](https://github.com/jpfreeley/GA-DSI/blob/master/DSI_IMAGE/curriculum/week-04/4.1-lab-webscraping/scraping-project-4-starter_JPF-Jesse.ipynb)

**Note:** The methodology below is drawn from the "Data Science Workflow" document provided by General Assembly

IDENTIFY THE PROBLEM
====================

*We've been asked to determine which parts of a job description are most influential in determining the salary of a Data Science "flavored" position. Because it is known that several job titles overlap in the Data Science industry, we must be wary of these subtleties*

**Risks and Assumptions**

It was clear that obtaining a large dataset which contained salary information was going to be a challenge. By 1st scraping the indeed.com website, we got a sense that about 4% of job descriptions contained some indicator of salary.

We were also at the mercy of the indeed.com search algorithm to present us relevant search results. We also needed to assume that there were no gross typographical errors. We dd not have significant outliers.

To supplement the indeed.com data, we also scraped historical salary information from glassdoor.com. This allowed us a baseline of Location and Title information along with salaries.

### ACQUIRE THE DATA
We were successful in scraping job postings from indeed.com. We scraped up to 1000 listings for each of 39 cities. In the end we compiled nearly 27,000 listings, about 1000 of which contained salary data. With the following data for each:

+ Location of Job - string
+ Title of Job - string
+ Summary of Job description - string
+ Job Posting Company - string
+ JKID - unique indeed.com job identifier - string
+ Number of "stars" for that Company - float 0-5 (0.5 increments)
+ Number of reviews for the company - integer
+ How many days ago the posting was created - float
+ Date that the posting was scraped - datetime
+ City that was used for the search - string

From Glassdoor we obtained the following data for nearly 1400 records:

salary
Location
title
company

Lastly, we obtained a Cost of Living index for cities in our scraped dataset from expatistan.com.

### PARSE THE DATA
Much of our efforts was spent cleaning the various columns. We developed functions for cleaning the reviews, the salary, the post_date, the title, and various other fields which we felt needed standardization.

One process that required a manual inspection and tagging of the data was the "binning" of the title data into 3 separate bins named ENTRY-LEVEL, MID-LEVEL, SENIOR-LEVEL experience level. We wrote code to programmatically bin the data, however the initial work to determine which title keywords should be assigned to which bin was a process that required some manual decisions.

This binning step was very important because these bins were directly used as features in our model. Decisions to assign a particular job listing as ENTRY/MID/SENIOR were subjective and could have significantly influenced our results. It would have perhaps been better to use countvectorizer to tokenize the titles and assign weights such as word occurrence. Further work would be required to investigate this more fully.

Likewise, glassdoor data was prepared, and titles binned by experience level as above.

### MINE THE DATA

Our overall goal was to attempt to make recommendations regarding which parts of a job listing might be used to determine if the positions salary would be above or below the median. I think we may have missed the mark slightly in this task. Because of the shortcomings of the glassdoor dataset, we were ultimately only able to use City and the binned Experience Level as the features of our model.

Due to this constrained feature-set, the analysis which was performed was more academic than enlightening. What we did was use the glassdoor data to train our model and compared that to the test set of the indeed data. The results and predictions below are a results of this train-test methodology.

#############

In conclusion, we can surmise that our model can, with reasonable accuracy, make a prediction about whether a salary would be above or below the median salary in the genre of "Data Scientist" jobs.

### REFINE THE DATA

### BUILD A DATA MODEL

### FURTHER WORK

Future work in this area could include focusing solely on the scraped indeed.com data and using more of the features in the indeed.com data for our model.

In addition, we could utilize frequency methods such as countvectorizer to parse the Position Summary and Position Title to determine which keywords have more weight in influencing keywords than others.

### POSTSCRIPT

Data acquisition is sometimes a very difficult process. Obtaining a significantly sized sample to perform reasonable analysis can be resource intensive. However, equally important is understanding that not every dataset will be useful in a particular project. Data shouldn't be included by force simply because it is available. It needs to make sense to include it.

Understanding when a project is departing from the initial questions posed is often difficult when you are focused on completing specific micro-tasks.
