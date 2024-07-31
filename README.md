# Guided Python Data Analysis Project Documentation

## Plot 1: US skill demand
### Goal:
The goal of the provided plot is to visualize the percentage likelihood of various skills appearing in job postings for different data-related roles in the United States. The roles examined are Data Analyst, Data Engineer, and Data Scientist. This plot helps to identify the most demanded skills for these positions, aiding both job seekers in their skill development and employers in aligning their job requirements.

### Plot code and explanation:
```python
# Create subplots for each job title
fig, ax = plt.subplots(len(job_titles), 1, figsize=(10, 8))

# Set the seaborn theme
sns.set_theme(style='ticks')

# Loop through each job title and create a bar plot
for i, job_title in enumerate(job_titles):
    # Filter the dataframe for the current job title and select the top 5 skills
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    
    # Create a horizontal bar plot
    sns.barplot(data=df_plot, x='skill_perc', y='job_skills', hue='skill_count', ax=ax[i], palette='dark:b_r')
    
    # Set the title for each subplot
    ax[i].set_title(job_title)
    
    # Remove x and y labels
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    
    # Invert y-axis to have the highest percentage skill on top
    ax[i].invert_yaxis()
    
    # Remove the legend for each subplot
    ax[i].get_legend().remove()
    
    # Set the x-axis limit
    ax[i].set_xlim(0, 70)
    
    # Remove x-axis ticks for all but the last subplot
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])
    
    # Add text labels for the percentage values
    for x, y in enumerate(df_plot['skill_perc']):
        ax[i].text(y + 1, x, f'{y:.0f}%', va='center')

# Set the overall title for the figure
plt.suptitle('Possibility of required skills appearing in US data job postings')

# Adjust the layout to make room for the titles
plt.tight_layout()

# Display the plot
plt.show()
```

### Plot image:
![image](https://github.com/user-attachments/assets/2f5a1028-51e1-4801-8be0-396da2e8611f)

### Conclusion of the plot:
**Data Analyst:**
Top Skills: SQL (51%), Excel (41%), Tableau (28%), Python (27%), SAS (19%).
Conclusion: SQL and Excel are highly demanded, emphasizing the need for strong data querying and spreadsheet skills.

**Data Engineer:**
Top Skills: SQL (68%), Python (65%), AWS (43%), Azure (32%), Spark (32%).
Conclusion: SQL and Python are critical, along with cloud technologies like AWS and Azure, and big data tools like Spark.

**Data Scientist:**
Top Skills: Python (72%), SQL (51%), R (44%), SAS (24%), Tableau (24%).
Conclusion: Python is the most demanded skill, followed by SQL and R, indicating the importance of programming and data manipulation skills in data science roles.

## Plot 2: Skill trends
### Goal:
The goal of this plot is to visualize the monthly trends in the demand for various skills in Data Analyst job postings throughout 2023. By tracking the skill counts over time, we can identify patterns and shifts in the skills that employers are seeking for Data Analyst roles.

### Plot code and explanation:
```python
# Plot the first five columns of the dataframe as a line plot
df_da_hu_piv.iloc[:, :5].plot(kind='line')

# Remove the top and right spines from plot
sns.despine()

# Get the current axis and make the legend visible
ax = plt.gca()
ax.legend().set_visible(True)

# Adjust the layout to fit everything properly
plt.tight_layout()

# Set the labels for x and y axes
plt.xlabel('Months')
plt.ylabel('Skill counts in Data Analyst job postings')

# Set the title of the plot
plt.title('Data Analyst skill trends throughout 2023')

# Display the plot
plt.show()
```

### Plot image:
![image](https://github.com/user-attachments/assets/a78eef3e-336a-41d3-b2c0-caed960c7fc9)

### Conclusion of the plot:
- SQL and Excel consistently show high demand throughout the year, indicating their critical importance for Data Analyst positions.
- Tableau, Python, and Power BI have relatively lower demand compared to SQL and Excel, but they also show varying trends throughout the year.
- There are noticeable fluctuations in the demand for these skills, suggesting that the requirements for Data Analyst roles can change over time.
- This analysis provides valuable insights for both job seekers and employers in the data analysis field, highlighting the most sought-after skills and how their demand changes over time.

## Plot 3: Salary analysis
### Goal:
The goal of this plot is to visualize the salary distributions for different data-related job titles in the US, providing insights into the salary ranges and median salaries for each job title.

### Plot code and explanation:
```python
# Create a box plot to visualize salary distributions for the top 6 data job titles
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

# Set the seaborn theme
sns.set_theme(style='ticks')

# Remove the top and right spines from the plot
sns.despine()

# Set the title of the plot
plt.title('Salary Distributions of Data Jobs in the US')

# Set the label for the x-axis
plt.xlabel('Yearly Salary (USD)')

# Remove the label for the y-axis
plt.ylabel('')

# Set the limit for the x-axis
plt.xlim(0, 600000)

# Format the x-axis ticks to show salaries in 'K' format
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)

# Display the plot
plt.show()
```

### Plot image:
![image](https://github.com/user-attachments/assets/012b03ce-86ad-41f4-9c09-120622f0b4f2)

### Conclusion of the plot:
- Median Salaries: Senior positions (Senior Data Scientist, Senior Data Engineer, Senior Data Analyst) generally have higher median salaries compared to their non-senior counterparts (Data Scientist, Data Engineer, Data Analyst).
- Salary Ranges: There is a wide range of salaries within each job title, with some outliers indicating very high salaries.
- Consistency: Data Scientist, Data Engineer, and Senior Data Scientist roles show relatively consistent salary distributions with fewer extreme outliers compared to other roles.
- This analysis provides valuable insights into the salary expectations for different data-related job titles in the US job market, helping job seekers and employers make informed decisions.

## Plot 4: Optimal skills:
### Goal:
The goal of this plot is to identify the most optimal skills for Data Analysts in the US by visualizing how the demand for specific skills in job postings correlates with the median salary associated with those skills. This helps in understanding which skills are both in high demand and associated with higher salaries.

### Plot code and explanation:
```python
from adjustText import adjust_text

# Create a scatter plot to visualize the relationship between skill demand and median salary
plt.scatter(df_DA_skills_high_demand['skill_percent'], df_DA_skills_high_demand['median_salary'])

# Set the label for the x-axis
plt.xlabel('Percent of Data Analyst Jobs')

# Set the label for the y-axis
plt.ylabel('Median Salary ($USD)')

# Set the title of the plot
plt.title('Most Optimal Skills for Data Analysts in the US')

# Get the current axis
ax = plt.gca()

# Format the y-axis to show salaries in 'K' format
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))

# Add text labels to each point in the scatter plot
texts = []
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i], df_DA_skills_high_demand['median_salary'].iloc[i], " " + txt))

# Adjust the text labels to avoid overlapping
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))

# Adjust the layout to fit everything properly
plt.tight_layout()

# Display the plot
plt.show()
```

### Plot image:
![image](https://github.com/user-attachments/assets/edde79e2-445c-40a0-9f39-7fe4fa51388a)

### Conclusion:
- Skills that are highly demanded (higher percentage on the x-axis) and associated with higher median salaries (higher value on the y-axis) are considered optimal for Data Analysts.
- This visualization helps job seekers identify which skills to focus on acquiring or improving to maximize their job opportunities and salary potential.
- Employers can also use this information to understand the market value of different skills and adjust their hiring strategies accordingly.
- This analysis provides valuable insights into the skill demand and salary trends for Data Analysts in the US job market.
