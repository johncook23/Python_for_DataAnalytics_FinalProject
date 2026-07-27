# Read Me


## Importing the csv file

``` python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('~/Python for Data Analytics/GitHub Repository/Python-for-Data-Analytics/StudentPerformanceFactors.csv')
```

## Creating Visualizations

Scatterplot of Hours Studied vs. Exam Score

``` python
plt.figure(figsize=(8, 5))
sns.scatterplot(
    data=df, 
    x='Hours_Studied', 
    y='Exam_Score', 
    hue='Motivation_Level',
    palette='viridis', 
    alpha=0.7
)
plt.title('Hours Studied vs. Final Exam Score', fontsize=14, fontweight='bold')
plt.xlabel('Hours Studied per Week', fontsize=12)
plt.ylabel('Exam Score', fontsize=12)
plt.tight_layout()
plt.show()
```

![](final_project_code_files/figure-commonmark/cell-3-output-1.png)

Exam Score Distribution by Parental Involvement

``` python
plt.figure(figsize=(8, 5))
sns.boxplot(
    data=df, 
    x='Parental_Involvement', 
    y='Exam_Score', 
    order=['Low', 'Medium', 'High'],
    palette='Set2'
)
plt.title('Exam Performance by Parental Involvement', fontweight='bold')
plt.xlabel('Parental Involvement Level')
plt.ylabel('Exam Score')
plt.show()
```

    /var/folders/jg/230rwzm55m9dsd9y8zwd3cxr0000gn/T/ipykernel_39771/441736833.py:2: FutureWarning: 

    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.

      sns.boxplot(

![](final_project_code_files/figure-commonmark/cell-4-output-2.png)

Habits Correlation Heatmap

``` python
plt.figure(figsize=(8, 6))
numeric_cols = ['Hours_Studied', 'Attendance', 'Sleep_Hours', 'Previous_Scores', 'Exam_Score']
sns.heatmap(df[numeric_cols].corr(), annot=True, cmap='Blues', fmt=".2f")
plt.title('Correlation Matrix of Student Factors', fontsize=14, fontweight='bold')
plt.tight_layout()
plt.show()
```

![](final_project_code_files/figure-commonmark/cell-5-output-1.png)

Attendance Barplot

``` python
df['Attendance_Tier'] = pd.cut(
    df['Attendance'], 
    bins=[59, 70, 80, 90, 100], 
    labels=['60–70%', '71–80%', '81–90%', '91–100%']
)

# Plot average exam score by attendance group
plt.figure(figsize=(9, 5.5))
ax = sns.barplot(
    data=df, 
    x='Attendance_Tier', 
    y='Exam_Score', 
    palette='Blues_d',
    errorbar=None
)
plt.title('Average Exam Score by Attendance Tier', fontsize=14, fontweight='bold')
plt.xlabel('Attendance Rate', fontsize=12)
plt.ylabel('Average Exam Score', fontsize=12)
plt.ylim(50, 80)

for p in ax.patches:
    ax.annotate(
        f'{p.get_height():.2f}', 
        (p.get_x() + p.get_width() / 2., p.get_height()), 
        ha='center', va='center', 
        xytext=(0, 8), 
        textcoords='offset points', 
        fontsize=11, fontweight='bold')

plt.tight_layout()
plt.savefig('attendance_barplot.png')
plt.show()
```

    /var/folders/jg/230rwzm55m9dsd9y8zwd3cxr0000gn/T/ipykernel_39771/3172496374.py:9: FutureWarning: 

    Passing `palette` without assigning `hue` is deprecated and will be removed in v0.14.0. Assign the `x` variable to `hue` and set `legend=False` for the same effect.

      ax = sns.barplot(

![](final_project_code_files/figure-commonmark/cell-6-output-2.png)
