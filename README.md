# Sports-Analysis-
Data Visualization for base football player metrics

"""
Created on Mon Sep 22 15:23:43 2025

@author: Sudhanva
"""

import pandas as pd 
import matplotlib.pyplot as plt
import seaborn as sns 
import numpy as np


df1 = pd.read_excel("Y7.xlsx")

df1 = df1.dropna()


cols_to_drop = ['Name', 'Pupil ID', 'Date of Measure \n(dd-mm-yy)', 'Age @ PHV',
       'Maturity Offset \n(years)', 'Date of Birth \n(dd-mm-yy)',
       'Age \n(years)', 'Gender \n(M=1, F=2)']

df1.drop(columns=cols_to_drop, inplace=True)

#(169, 35)


"""
#~~~~~~~~~~~~~~~~~~~~~Descriptive Statistics~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


# Count gender
gender_counts = df1['Gender \n(M=1, F=2)'].value_counts()

# Map numbers to labels
gender_counts.index = gender_counts.index.map({1: 'Male', 2: 'Female'})


print(gender_counts)

# Bar chart
gender_counts.plot(kind='bar', color=['skyblue', 'lightpink'])
plt.title("Gender Split of Students")
plt.ylabel("Number of Students")
plt.show()

# Pie chart (alternative)
gender_counts.plot(kind='pie', autopct='%1.1f%%', colors=['skyblue', 'lightpink'])
plt.title("Gender Split of Students")
plt.ylabel("")  # remove y-label
plt.show()
"""

"""
sns.regplot(
    data=df1,
    x="Age \n(years)",
    y="Standing Height \n(cm)"
)

plt.title("Age vs Standing Height")
plt.show()
"""

#~~~~~~~~~~~~~~~~~~~~~~~~~ Radar Charts ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

"""
# Example: pick one athlete

for x in range(0, 169):
    athlete = df1.iloc[x]   # first row, you can change to a specific player

    # Select performance metrics
    metrics = ["CMJ \n(cm)", "20m Sprint \n(sec)", "Mid Thigh Pull (N/kg)", "Sit & Reach (cm)"]
    values = athlete[metrics].values

    # Radar charts need to "loop back" to the first value
    values = np.append(values, values[0])
    angles = np.linspace(0, 2*np.pi, len(metrics)+1)

    # Plot
    fig, ax = plt.subplots(figsize=(6,6), subplot_kw=dict(polar=True))
    ax.plot(angles, values, marker='o')
    ax.fill(angles, values, alpha=0.25)

    # Axis labels
    ax.set_xticks(angles[:-1])
    ax.set_xticklabels(metrics)

    #plt.title(f"Athletic Profile: {athlete['Name']}")
    plt.show()
""" 
#~~~~~~~~~~~~~~~~~~~~~~~~~Correlation Plots ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

corr = df1.corr()
cmap = sns.diverging_palette(230, 20, as_cmap=True)
f, ax = plt.subplots(figsize=(11, 9))
sns.heatmap(corr, cmap=cmap, vmax=.3, center=0,
            square=True, linewidths=.5, cbar_kws={"shrink": .5})

plt.show()
plt.close()
