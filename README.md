# Guided Python Data Analysis Project Documentation

## Plot 1: US skill demand
### Goal:
The goal of the provided plot is to visualize the percentage likelihood of various skills appearing in job postings for different data-related roles in the United States. The roles examined are Data Analyst, Data Engineer, and Data Scientist. This plot helps to identify the most demanded skills for these positions, aiding both job seekers in their skill development and employers in aligning their job requirements.

### Plot code:
'''python
fig, ax = plt.subplots(len(job_titles),1)
sns.set_theme(style='ticks')
for i, job_title in enumerate(job_titles):
    df_plot=df_skills_perc[df_skills_perc['job_title_short']==job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_perc', y='job_skills', hue='skill_count', ax=ax[i], palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].invert_yaxis()
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 70)
    if i != len(job_titles)-1:
        ax[i].set_xticks([])
    for x, y in enumerate(df_plot['skill_perc']):
        ax[i].text(y+1, x, f'{y:.0f}%', va='center')
plt.suptitle('Possibility of required skills appearing in US data job postings')
plt.tight_layout()
'''
