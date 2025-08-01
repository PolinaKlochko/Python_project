# Overview
Welcome to my exploration of the data job market, with a focus on data analyst positions. This project was born from a desire to better understand and navigate career opportunities in this field. It highlights the highest-paying and most sought-after skills to help identify the best roles for aspiring data analysts.

The analysis is based on data from [Luke Barousse’s Python Course](https://youtu.be/wUSDVGivd-8?si=JTG_f3JyfPr6cyU-), which serves as the foundation for this project. The dataset includes comprehensive details on job titles, salaries, locations, and essential skills. Using Python scripts, I examine key insights such as which skills are most in demand, prevailing salary trends, and how skill demand aligns with compensation in the data analytics industry.

# The Questions
Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)
# Tools I Used
To explore the data analyst job market in depth, I utilized a range of essential tools:

- **Python**: The backbone of my analysis, allowing me to analyze the data and find critical insights. I also used
  the following Python libraries:
  - **Pandas Library**: This was used to analyze the data.
  - **Matplotlib Library**: I visualized the data.
  - **Seaborn Library**: Helped me create more advanced visuals.
- **Jupyter Notebooks**: The tool I used to run my Python scripts which let me easily include my notes and analysis.
- **Visual Studio Code**: My go-to for executing my Python scripts.
- **GitHub**: Essential for sharing my Python code and analysis.

# Data Preparation and Cleanup
This section describes the steps taken to clean and prepare the data for accurate and effective analysis.

## Import & Clean Up Data
I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.
```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```
## Filter Indian Jobs
To focus my analysis on Indian job market, I apply filters to the dataset, narrowing down to roles based in India.
```python
df_India = df[df['job_country'] == 'India']
```
# The Analysis
Each Jupyter notebook in this project focuses on exploring a specific aspect of the data job market. Here's how I addressed each question:
## 1. What are the most demanded skills for the top 3 most popular data roles?
To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here: [2_Skill_Demand](https://github.com/PolinaKlochko/Python_project/blob/main/2_Skills_Count.ipynb).
