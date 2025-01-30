# Social-Life-vs.-Math-Performance


## Introduction

In this project, we analyze data from two Portuguese high schools regarding student performance in Mathematics and Portuguese courses as well as social and demographic factors. It contains 34 columns and 395 rows, with the index being “Student ID.” There are 21 categorical variables and 13 numerical variables. In this project, we want to answer two main questions:

* Is having a more active social life associated with a better or worse mathematics grade?
* What kind of socioeconomic and demographic factors have the strongest effect on mathematics grade?

In this project, we use various techniques, including exploratory data analysis, the Wilcoxon Ranked Sum test (nonparametric two-sample t-test), the Krukal-Wallis test (nonparametric ANOVA test), and multiple linear regression to analyze the complex relationships between a student's social life and socioeconomic background, and their mathematics grades. 

## Data

The data used in this project comes from a dataset titled [“High School Student Performance & Demographics”](https://www.kaggle.com/datasets/dillonmyrick/high-school-student-performance-and-demographics) from Kaggle.com.

### Response (Dependent) Variable: Mathematics Final Grade

<img width="600" height="400" src="Plots and Images\grade_hist.png">

For the reponse variable, we use final grade, which is a student's final course grade in their mathematics course where students are graded 0-20.

### Explanatory (Independent) Variables

* **Romantic Relationship** : Whether or not a student is involved in a romantic relationship.  (binary: yes or no)
* **Extracurricular Activities** : Whether or not a student is involved in extracurricular activities. (binary: yes or no)
* **Weekend Alcohol Consumption** : Student’s level of alcohol consumption on weekends.  (scale of 1 to 5, with 1 = very low and 5 = very high)
* **Frequency of Social Outings** : How often a student goes out with friends.  (scale of 1 to 5, with 1 = very infrequently and 5 = very frequently)
* **Address Type** : Type of area that a student resides in. (binary: urban or rural)
* **Family Support**: Whether or not a student’s family provides them with educational support. (binary: yes or no)
* **Health**: Student’s current health status. (scale of 1 to 5, with 1 = very poor and 5 = very good)
* **Internet Access**: Whether or not student has reliable access to the internet at home (binary: yes or no)
* **Mother’s Education**: Student’s mother’s education level.  (5 levels ranging from “none” to “higher education”)
* **Father’s Education**: Student’s father’s education level.  (5 levels ranging from “none” to “higher education”)
* **Extra Paid Classes**: Whether a student participates in extra (paid) mathematics courses outside of school. (binary: yes or no)
* **Parent Status**: Student’s parents’ cohabitation status. (binary: “Living together” or “Living apart”)


## Some Quick Data Visualization

First, we will start with exploratory data analysis. 

<img width="400" height="400" src="Plots and Images\heatmap_1.png">
<img width="400" height="400" src="Plots and Images\heatmap_2.png">
<img width="400" height="400" src="Plots and Images\heatmap_3.png">

As illustrated in the heatmaps above, the only numeric variable that appear to be correlated with the final grade variable is the frequency of social outings.


  
## Wilcoxon Test to Analyze the Relationship Between Math Performance, and Romantic Relationship Status and Involvement in Extracurricular Activities

<img width="300" height="300" src="Plots and Images\wilcox_1.png">
<img width="300" height="300" src="Plots and Images\wilcox_2.png">

Since our data is not normally distributed, we have opted to use Wilcoxon Rank Sum test, as opposed to the standard two sample t-test.  The results of the tests are as follows:
* **Romantic relationship**: At 𝛼 = 0.05, we fail to reject the null hypothesis. However, at 𝛼 = 0.10, we can reject the null hypothesis and conclude that there may be a relationship between involvement in a romantic relationship and mathematics final grade. After further analysis, we conclude that students involved in a romantic relationship tend to achieve higher mathematics grades than those who are not.
* **Extracurricular Activities**: With a very large p-value of 0.6049, we fail to reject the null hypothesis at both  𝛼 = 0.05 and 𝛼 = 0.10. Thus, we can conclude that there is not a significant relationship between involvement in extracurricular activities and mathematics final grade.


## Kruskal Wallis Test to Analyze the Relationship Between Math Performance, and Frequency of Social Outings and Weekend Alcohol Consumption

<img width="300" height="300" src="Plots and Images\kw_1.png">
<img width="300" height="300" src="Plots and Images\kw_2.png">

Since our data is not normally distributed, we have opted to use the Kruskal Wallis test, as opposed to the standard ANOVA test.  The results of the tests are as follows:

* **Weekend Alcohol Consumption**: At 𝛼 = 0.05 and 𝛼 = 0.10, we fail to reject the null hypothesis.Thus, we can conclude that there is insufficient evidence that there is a relationship between mathematics grade and weekend alcohol consumption.
* **Frequency of Social Outings**: With a p-value of 0.005372, we can reject the null hypothesis at 𝛼 = 0.05. Thus, we can conclude that there is a significant relationship between mathematics grade and frequency of social outings. 
Our post-hoc analysis indicates that students who attend social outings more frequently achieve a lower mathematics grade.

## Multiple Linear Regression to Analyze the Relationship Between Math Performance and Socioeconomic Status

<img width="300" height="400" src="Plots and Images\lr_1.png">
<img width="300" height="300" src="Plots and Images\lr_2.png">

* Extra paid classes, mother's education, and family support were the only variables to have a significant relationship with a student's final mathematics grade at a significance level of 0.10.
* The predictive power of this model is very weak, with an adjusted R-squared value of 0.0508.
Unfortunately, this model is not entirely valid or reliable, as two of the linear regression assumptions have been violated. To address this, we will apply a Box-Cox transformation to our response variable and repeat this model.

## Modified Multiple Linear Regression

<img width="300" height="400" src="Plots and Images\lr_5.png">
<img width="300" height="300" src="Plots and Images\lr_6.png">

* The mathematics final grade variable has many values of '0'. Since a final grade of 0 in a course generally means that a student did not complete the course or had their score voided, these scores are most likely irrelevant. Thus, we will remove all rows where final grade is equal to 0, and repeat the linear regression model.
* With zero values removed, the results slightly differ. The independent variables that have a statistically significant relationship with final mathematics grade at the 0.10 significance level are family support and father's education level.
* Fortunately, this model passes all three of the linear regression assumptions, and can be considered to be a valid and reliable model. 


## Final Thoughts

**Social Factors and Math Performance**
*Not much impact from individual factors (e.g., extracurricular activities, alcohol consumption, etc.). However, a few factors are significant:
**Social Life**: 
*Students involved in a romantic relationship are predicted to achieve higher mathematics grades compared to their peers. 
*Students who attend social outings very frequently are predicted to achieve lower mathematics grades compared to their peers.
**Socioeconomic Status**:
*Students whose father has completed a Bachelor’s degree or higher are predicted to achieve higher mathematics grades  compared to their peers.
*Students who receive more family support in the field of mathematics are predicted to achieve lower mathematics grades compared to their peers.
*Significant collective impact of social factors on math performance (p-value = 0.002352).
**Conclusion and Future Directions**
*Social factors as a whole affect math performance.
*Future research should consider geographical and cultural factors.
*Limited to Portuguese data; findings may not generalize globally.






