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

- SQL and Excel consistently show high demand throughout the year, indicating their critical importance for Data Analyst positions.
- Tableau, Python, and Power BI have relatively lower demand compared to SQL and Excel, but they also show varying trends throughout the year.
- There are noticeable fluctuations in the demand for these skills, suggesting that the requirements for Data Analyst roles can change over time.
This analysis provides valuable insights for both job seekers and employers in the data analysis field, highlighting the most sought-after skills and how their demand changes over time.
