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

View my notebook with detailed steps here: [2_Skills_Demand](https://github.com/PolinaKlochko/Python_project/blob/main/2_Skills_Demand.ipynb).

### Visualize Data
```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_count[df_skills_count['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_count', y='job_skills', ax=ax[i], hue='skill_count', palette='crest')

plt.show()
```
### Results
![](https://github.com/PolinaKlochko/Python_project/blob/main/images/Likelihood%20of%20Skills%20Requested%20in%20Indian%20Job%20Postings.png)

*Bar graph visualizing the salary for the top 3 data roles and their top 5 skills associated with each.*
### Insights:
- SQL is the most requested skill for Data Analysts and Data Engineers, with it in over half the job postings for both roles. For Data Scientists, Python is the most sought-after skill, appearing in 70% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).
- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (70%) and Data Engineers (61%).
## 2. How are in-demand skills trending for Data Analysts?
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

View my notebook with detailed steps here: [3_Skills_Trend](https://github.com/PolinaKlochko/Python_project/blob/main/3_Skills_Trend.ipynb).
### Visualize Data
```python
from matplotlib.ticker import PercentFormatter

df_plot = df_DA_India_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()
```
### Results
![](https://github.com/PolinaKlochko/Python_project/blob/main/images/Trending%20Top%20Skills%20for%20Data%20Analysts%20in%20India.png)

*Bar graph visualizing the trending top skills for data analysts in India in 2023.*
### Insights:
- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experiences a sharp spike in May, reaching its peak (~58%), but then declines and stabilizes toward the end of the year.
- Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.
## 3. How well do jobs and skills pay for Data Analysts?
To identify the highest-paying roles and skills, I only got jobs in India and looked at their median salary. But first I looked at the salary distributions of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most.

View my notebook with detailed steps here: [4_Salary_Analysis](https://github.com/PolinaKlochko/Python_project/blob/main/4_Salary_Analysis.ipynb).
### Visualize Data
```python
sns.boxplot(data=df_India_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
### Results
![](https://github.com/PolinaKlochko/Python_project/blob/main/images/Salary%20Distributions%20of%20Data%20Jobs.png)

*Box plot visualizing the salary distributions for the top 6 data job titles.*
### Insights
- Machine Learning Engineers and Data Scientists have the widest salary ranges among all roles, indicating high earning potential as well as variability depending on experience, company, or skill level. Both roles have upper ranges extending well beyond $200K.
- Data Engineers show a relatively high and consistent salary distribution, with a strong median compared to Data Analysts and Software Engineers, suggesting solid demand and compensation for infrastructure-focused data roles.
- Software Engineers and Data Analysts have narrower and lower salary ranges compared to more specialized roles. Their median salaries are also among the lowest, reflecting entry- to mid-level compensation and potentially fewer domain-specific requirements.
## Highest Paid & Most Demanded Skills for Data Analysts
Next, I narrowed my analysis and focused only on data analyst roles. I looked at the highest-paid skills and the most in-demand skills. I used two bar charts to showcase these.
### Visualize Data
```python
fig, ax = plt.subplots(2, 1)  

# Top 15 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='crest')

# Top 15 Most In-Demand Skills for Data Analysts')
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='crest')

plt.show()
```
### Results
Here's the breakdown of the highest-paid & most in-demand skills for data analysts in India:
![](https://github.com/PolinaKlochko/Python_project/blob/main/images/Highest%20Paid%20Skills%20and%20Most%20In-demand%20Skills%20for%20Data%20Analyst%20in%20India.png)

*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in India.*
### Insights:
- High-paying skills for data analysts in India include technical tools like pyspark, Linux, GitLab, MySQL, PostgreSQL, and MongoDB, all associated with median salaries above $140K. Mastery of backend and engineering-related tools appears to strongly boost earning potential.
- Most in-demand skills, such as MongoDB, Power BI, Tableau, Excel, and SQL, are centered around data visualization, reporting, and database management. These are essential for day-to-day analysis work, even if they don’t command the highest salaries.
- There’s a clear gap between what pays the most and what’s most in demand — suggesting that data analysts should balance their skillset by learning foundational tools for employability and niche or technical tools for salary growth.
## 4. What are the most optimal skills to learn for Data Analysts?
To identify the most optimal skills to learn ( the ones that are the highest paid and highest in demand) I calculated the percent of skill demand and the median salary of these skills. To easily identify which are the most optimal skills to learn.

View my notebook with detailed steps here: [5_Optimal_Skills](https://github.com/PolinaKlochko/Python_project/blob/main/5_Optimal_Skills.ipynb).
### Visualize Data
```python
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])
plt.show()
```
### Results
![](https://github.com/PolinaKlochko/Python_project/blob/main/images/Most%20Optimal%20Skills%20for%20Data%20Analyst%20in%20India.png)

*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in India.*
### Insights:
- Specialized skills like MongoDB, Looker, and Spark command the highest salaries (over $110K), despite appearing in less than 20% of job listings, highlighting their high value and scarcity.
- Essential skills like SQL, Excel, and Python are prevalent in 40–50% of job postings but offer moderate salaries (~$96K–$98K), indicating they are foundational yet not highly lucrative on their own.
- Tools such as Power BI and Tableau strike an optimal balance, with 20–30% job demand and robust median salaries (~$108K–$112K), making them ideal for career advancement.
## Visualizing Different Techonologies
Let's visualize the different technologies as well in the graph. We'll add color labels based on the technology (e.g., {Programming: Python})
### Visualize Data
```python
from matplotlib.ticker import PercentFormatter

# Create a scatter plot
scatter = sns.scatterplot(
    data=df_DA_skills_tech_high_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology',  # Color by technology
    palette='bright',  # Use a bright palette for distinct colors
    legend='full'  # Ensure the legend is shown
)
plt.show()
```
### Results
![](https://github.com/PolinaKlochko/Python_project/blob/main/images/Most%20Optimal%20Skills%20for%20Data%20Analyst%20in%20India%20with%20coloring.png)

*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in India with color labels for technology.*
### Insights:
- Programming skills like Python and R offer elevated salary potential (up to ~$98K for Python), even with lower demand (<20%), underscoring the value of strong coding skills in data analytics roles.
- Database technologies, including MongoDB (~ $160K) and SQL Server (~ $90K–$100K), exhibit a broad salary range, with MongoDB providing niche, high-paying opportunities despite minimal demand (<10%).
- Analyst tools such as Power BI, Tableau, and Excel balance demand (20–40%) with salaries exceeding $100K, positioning them as critical and market-relevant skills for professional growth.
# What I Learned
Throughout this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in Python, especially in data manipulation and visualization. Here are a few specific things I learned:
- **Advanced Python Usage**: Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.
- **Data Cleaning Importance**: I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.
- **Strategic Skill Analysis**: The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.
# Insights
This project provided several general insights into the data job market for analysts:
- **Skill Demand and Salary Correlation**: There is a clear correlation between the demand for specific skills and the salaries these skills command. Advanced and specialized skills like Python and MongoDB often lead to higher salaries.
- **Market Trends**: There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
- **Economic Value of Skills**: Understanding which skills are both in-demand and well-compensated can guide data analysts in prioritizing learning to maximize their economic returns.
# Challenges I Faced
This project was not without its challenges, but it provided good learning opportunities:
- **Data Inconsistencies**: Handling missing or inconsistent data entries requires careful consideration and thorough data-cleaning techniques to ensure the integrity of the analysis.
- **Complex Data Visualization**: Designing effective visual representations of complex datasets was challenging but critical for conveying insights clearly and compellingly.
- **Balancing Breadth and Depth**: Deciding how deeply to dive into each analysis while maintaining a broad overview of the data landscape required constant balancing to ensure comprehensive coverage without getting lost in details.
# Conclusion
This deep dive into the data analyst job market has been highly insightful, shedding light on the key skills and emerging trends that define this dynamic profession. The insights gained not only deepen my understanding but also offer practical direction for anyone aiming to grow in the field of data analytics. As the landscape continues to evolve, staying informed through ongoing analysis will be crucial. This project lays a strong foundation for future research and highlights the value of continuous learning and adaptability in the world of data.
