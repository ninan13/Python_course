# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here: [2_Skills_Count.ipynb](3_Project/2_Skills_Count.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style = 'ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data = df_plot, x = 'skill_percent', y = 'job_skills', ax = ax[i], hue = 'skill_count', palette = 'dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].set_xlim(0,65)
    ax[i].get_legend().remove()

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va = 'center')
    
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in Germany Job Postings', fontsize = 15)
fig.tight_layout(h_pad = 0.5)
plt.show()
```

### Results

![Visualisation of Top Skills for Data Jobs in Germany](3_Project/images/skill_demand_data_roles.png)

### Insights

- Across Data Analyst, Data Engineer, and Data Scientist roles in Germany, SQL and Python consistently appear as the most in-demand skills. 
- Data Analysts rely heavily on business intelligence tools such as Tableau, Excel, and Power BI, reflecting a stronger focus on reporting and data visualization. 
- Data Engineers show the widest technical spread, with high demand for cloud platforms (Azure, AWS) and big-data technologies like Spark, indicating more infrastructure-oriented responsibilities. 
- Data Scientists emphasize programming and statistical analysis, with strong requirements for Python, SQL, and R. Overall, the chart highlights a clear pattern: while all roles share a foundation in SQL and Python, each job type branches into distinct toolsets aligned with its core tasks.

