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

## 2. How are in-demand skills trending for Data Analysts?

To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

View my notebook with detailed steps here: [3_Skills_Trend](3_Project/3_Skills_Trend.ipynb).

### Visualize Data

```python

sns.lineplot(data = df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter())

plt.show()

```

### Results

![Trending Top Skills for Data Analysts in Germany](3_Project/images/Trending_Top_Skills_for_Data_Analysts_in_Germany.png)  


### Insights:
1. SQL stays on top all year.
It’s consistently the most requested skill for Data Analysts in Germany, even though it dips a bit late summer.

2. Python is strong but more volatile.
It rises in spring/early summer, drops sharply in September, then picks up again toward the end of the year. Still clearly the second-most important skill.

3. Tableau trends downward.
It starts fairly high but gradually declines through the year. This might signal a shift toward other visualization tools or more emphasis on coding-based skills.

4. R keeps a moderate but steady presence.
It has ups and downs, but stays mid-range. Some companies still want it, but it’s far less central than SQL/Python.

5. Power BI stays low and stable.
It’s the least requested of the five but remains consistent. Likely more dependent on specific company ecosystems than industry-wide demand.