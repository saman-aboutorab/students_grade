# students_grade

## Introduction

Do students who report higher amounts of studying tend to get better
final grades? does the quality of the student\'s family relationship
influence the number of absences the student has in school?
:::

::: {.cell .code execution_count="27" id="caoxEn8ju3Oy"}
``` python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Import median function from numpy
from numpy import median

```
:::

::: {.cell .markdown}
![students](vertopal_5cb6d8a1ed7e4fba8e578c2d00770b1b/4b23ae0ec4d3a4d7dae2a524502ed749a43c7e6c.jpg)
:::

::: {.cell .markdown id="wgiNvKaNv08n"}
## Dataset
:::

::: {.cell .code execution_count="2" id="kf3Gn-eDvtKA"}
``` python
student_data = pd.read_csv('student-alcohol-consumption.csv')
```
:::

::: {.cell .code execution_count="3" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="bUkISTJYvxUq" outputId="1d393bc5-b12d-492b-d7d1-4c3591a6cabf"}
``` python
print(student_data.head())
```

::: {.output .stream .stdout}
       Unnamed: 0 school sex  age famsize Pstatus  Medu  Fedu  traveltime  \
    0           0     GP   F   18     GT3       A     4     4           2   
    1           1     GP   F   17     GT3       T     1     1           1   
    2           2     GP   F   15     LE3       T     1     1           1   
    3           3     GP   F   15     GT3       T     4     2           1   
    4           4     GP   F   16     GT3       T     3     3           1   

       failures  ... goout Dalc Walc health absences  G1  G2  G3  location  \
    0         0  ...     4    1    1      3        6   5   6   6     Urban   
    1         0  ...     3    1    1      3        4   5   5   6     Urban   
    2         3  ...     2    2    3      3       10   7   8  10     Urban   
    3         0  ...     2    1    1      5        2  15  14  15     Urban   
    4         0  ...     2    1    2      5        4   6  10  10     Urban   

          study_time  
    0   2 to 5 hours  
    1   2 to 5 hours  
    2   2 to 5 hours  
    3  5 to 10 hours  
    4   2 to 5 hours  

    [5 rows x 30 columns]
:::
:::

::: {.cell .markdown id="xlOv2Vp-1pIu"}
## Plot style
:::

::: {.cell .code execution_count="65" id="gIaGeMTIwc7u"}
``` python
sns.set_style("whitegrid")
sns.set_palette("RdBu")
```
:::

::: {.cell .markdown id="-MzOZVvmv9p9"}
## Study time vs. grade {#study-time-vs-grade}
:::

::: {.cell .code execution_count="72" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":601}" id="SAPJg7wlvzH6" outputId="c8da4a30-fa0c-4eb4-bc8a-c11246e835db"}
``` python
# List of categories from lowest to highest
category_order = ["<2 hours",
                  "2 to 5 hours",
                  "5 to 10 hours",
                  ">10 hours"]

# Turn off the confidence intervals
g = sns.catplot(x="study_time", y="G3",
            data=student_data,
            kind="bar",
            order=category_order, ci=None)

# Add a title
g.fig.suptitle("Study time vs. Grade")

# Show plot
plt.show()
```

::: {.output .stream .stderr}
    <ipython-input-72-a9304d37df5c>:8: FutureWarning: 

    The `ci` parameter is deprecated. Use `errorbar=None` for the same effect.

      g = sns.catplot(x="study_time", y="G3",
:::

::: {.output .display_data}
![](vertopal_5cb6d8a1ed7e4fba8e578c2d00770b1b/78cbd0e9106f35383044f421f7a6513b2952945c.png)
:::
:::

::: {.cell .markdown id="oFtnW6w6x8qh"}
## Internet access
:::

::: {.cell .code execution_count="73" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":512}" id="avKFN0CiwIQV" outputId="817221fc-4165-407a-960a-be33c95df164"}
``` python
# Create a box plot with subgroups and omit the outliers
g = sns.catplot(x='internet', y='G3', data=student_data, kind='box', hue='location', sym='')

# Add a title
g.fig.suptitle("Internet access vs. Grade")

# Show plot
plt.show()
```

::: {.output .display_data}
![](vertopal_5cb6d8a1ed7e4fba8e578c2d00770b1b/377abc4365ffc0b09aaceaabb1c5df936151fc56.png)
:::
:::

::: {.cell .markdown id="Gr6xlqQfyNai"}
## Romantic relationships
:::

::: {.cell .code execution_count="75" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":512}" id="mVT0czegxkax" outputId="ce806ab1-0bdb-4fe0-c25a-99e7d4eafe87"}
``` python
# Set the whiskers to 0.5 * IQR
g = sns.catplot(x="romantic", y="G3",
            data=student_data,
            kind="box", whis=0.5)

# Add a title
g.fig.suptitle("Romantic Relationships vs. Grade")

# Show plot
plt.show()
```

::: {.output .display_data}
![](vertopal_5cb6d8a1ed7e4fba8e578c2d00770b1b/f2b360b52b7d44638bdb57b6205146834d40716a.png)
:::
:::

::: {.cell .markdown id="gHDBlP9vzLG7"}
## Absence vs. Relationship {#absence-vs-relationship}
:::

::: {.cell .code execution_count="76" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":601}" id="SckTKWowy2m7" outputId="97c65020-1d2a-46ad-a375-779d6e62dc68"}
``` python
# Plot the median number of absences instead of the mean
g = sns.catplot(x="romantic", y="absences",
			data=student_data,
            kind="point",
            hue="school",
            ci=None, estimator=median)

# Add a title
g.fig.suptitle("Absence vs. Relationship")


# Show plot
plt.show()
```

::: {.output .stream .stderr}
    <ipython-input-76-b09a7e7f14f2>:2: FutureWarning: 

    The `ci` parameter is deprecated. Use `errorbar=None` for the same effect.

      g = sns.catplot(x="romantic", y="absences",
:::

::: {.output .display_data}
![](vertopal_5cb6d8a1ed7e4fba8e578c2d00770b1b/b4fb32924a57b26334da420c0ad627483ccc861f.png)
:::
:::

::: {.cell .markdown id="Fm-Ho1mSys5c"}
## Family relationships vs. Absence {#family-relationships-vs-absence}
:::

::: {.cell .code execution_count="78" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":512}" id="_xBSILFuyL4M" outputId="65238f40-2111-4048-bf09-45d50e0765d5"}
``` python
# Remove the lines joining the points
g = sns.catplot(x="famrel", y="absences",
			data=student_data,
            kind="point",
            capsize=0.2, join=False)

# Add a title
g.fig.suptitle("Family relationships vs. Absence")

# Show plot
plt.show()
```

::: {.output .display_data}
![](vertopal_5cb6d8a1ed7e4fba8e578c2d00770b1b/344ce7d65b826947e2d3d85c8eb3cffa1563962c.png)
:::
:::

::: {.cell .code id="JSHn0L6F0SEk"}
``` python
```
:::
