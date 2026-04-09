# The Analysis

## 1.What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting. 

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](2_Skill_Demand.ipynb)


### Visualize Data

```python

fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

    plt.show()
    ```

    ## Results 

    ![Visualization of Top Skills for Data Nerds](Images/skill_demand_all_data_roles.png)

### Insights

- R is 44% Important for statistical computing and graphics. 

- Data Analyst focus more on tools for data manipulation and visualization (Excel,Tableu)

- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analyst and Data Scientist who are expected to be proficient in more general data management and analysis tools(Excel, Tableu).

## 2. How are in demand skills trending for data analyst?
### visualize data

``` python 

from matplotlib.ticker import PercentFormatter 
df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False,
legend='full' , palette='tab10)

plt.gca().yaxist.set_major_formatter
(PercentFormatter(decimals=0))

plt.show()

```
![Trending Top Skills for Data Analysts in the US](Images/skill_trend_DA.png) 
*Bar graph visualizing the trending top skills for data analyst in the US in 2023.*

### Insights:

- Tools like Tableau/Power BI show varying demand, suggesting companies cycle through hiring needs for data visualization specialists.

- Python & R programming languages appear in top 5 but with lower percentages than SQL/Excel, indicating many DA roles don't require heavy programming.

- The relatively flat trends (no dramatic drops) suggest consistent, stable demand for data analyst skills in 2023.

# The Analysis 

## How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds

#### Visualize Data

``` Python

sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style="ticks")
plt.title('Salary Distribution for Top 6 Job Titles in the United States')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 600000)
ticks_x = plt.FuncFormatter(lambda x, pos: f'{int(x/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

```

#### Results 

1[Salary Distribution of Data Jobs in the US](4_Salary_Analysis.ipynb)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

#### Insights

- Many roles have right-skewed outliers, meaning exceptional candidates (with rare skills) can earn 2–3x the median.

-  Salaries align with industry demand—technical roles (Engineer, Scientist) outpace Analyst roles. Consider location for accurate expectations.

- Moving from Analyst to Senior Analyst/Engineer can double salary potential. Focus on skills like Python, SQL, and cloud tools to climb the ladder.

# The Analysis

## How well do jobs and skills pay for data?

### Highest Paid and most demanded skills for data

### Visual

``` python
fig, axes = plt.subplots(2, 1, figsize=(12, 10), sharex=True)
sns.set_theme(style='ticks')

df_top_pay = df_da_top_pay.reset_index()
sns.barplot(
    data=df_top_pay,
    x='median',
    y='job_skills',
    ax=axes[0],
    palette='dark:b_r'
)
axes[0].set_title('Top 10 Highest Paid Skills for Data Analysts')
axes[0].set_ylabel('')
axes[0].set_xlabel('')
axes[0].xaxis.set_major_formatter(
    plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K')
)
axes[0].set_xlim(0, 200000)
if axes[0].get_legend():
    axes[0].get_legend().remove()

df_skill_demand = df_da_skill_demand.reset_index().sort_values('count', ascending=False).head(10)
sns.barplot(
    data=df_skill_demand,
    x='median',
    y='job_skills',
    ax=axes[1],
    palette='light:b'
)
axes[1].set_title('Top 10 Most In-Demand Skills for Data Analysts')
axes[1].set_ylabel('')
axes[1].set_xlabel('Median Salary (USD)')
axes[1].xaxis.set_major_formatter(
    plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K')
)
axes[1].set_xlim(0, 200000)
if axes[1].get_legend():
    axes[1].get_legend().remove()

plt.tight_layout()
plt.show()
```
![Visuals of the Top 10 Most In-Demand Skills and the Top 10 Highest paid skills for Data Analyst](4_Salary_Analysis.ipynb)
#### Insights: 

- The top graph shows specialized technical skills like "dplyr, 'Bitbucket', and 'Gitlab'are associated with higher salaries, some reaching up to $200K, suggesting that advanced technical proficiency can increase earning potential.
- There's a clear distinction between the skills that are
highest pald and those that are most in-demand. Data analysts aiming to maximize their career potential should consider developing a diverse skill set that includes both high-paying specialized
Lskills and widely demanded
foundational skills.

- The bottom graph highlights that foundational skills like 'Excel', 'PowerPoint', and 'SQL' are the most in-demand, even though they may not offer the highest salaries.

# The Analysis 

## 4. What is the most Optimal Skill for Data Analysts?

#### Visualize the Data
``` Python
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${(int(y/1000)):}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))
plt.legend()
plt.show()
```
### The Results

![Most Optimal Skills for Data Analysts in the USA](5_Optimal_Skills.ipynb)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

#### Insights 
- SQL is the most in-demand skill—but not the highest paid
SQL appears in ~58% of job postings, making it the most requested skill.
However, its median salary (~$91K) is not the highest, suggesting it’s a baseline requirement rather than a premium differentiator.
- Python has the highest salaries among common skills
Python stands out with the highest median salary (~$97–98K) while still being highly demanded (~33%).
This indicates strong value in combining programming with data analysis—Python is a key “premium” skill.
-  Specialized or enterprise tools boost pay despite lower demand
Skills like Oracle, R, and Tableau show high salaries ($92K–$97K) but are mentioned in fewer job postings.
This suggests that specialization (databases, statistical tools, visualization platforms) can lead to higher compensation even if demand is narrower.

**Overview**


Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.
The data sourced from Luke Barousse's Python Course which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.
***The Questions***
Below are the questions I want to answer in my project:
1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)
Tools I Used

**** Challenges I Faced**
- Data Inconsistencies: Getting the data in the right order.
- Complex Data Visualization: multiple aspects of the code are involved (seaborn)

** Conclusion ** 
 - This project reinforced the importance of sticking to fundamental principles when working with complex or convoluted data.
