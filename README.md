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
