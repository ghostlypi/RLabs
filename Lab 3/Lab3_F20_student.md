---
title: 'Lab 3: 2 Numeric EDA & Simple Linear Regression with transformations & Intro to Inference'
date:  Fall 2020"
output: 
  html_document: default
---


### Name: Parth



## Skills


* Given a study, distinguish between explanatory and response variables
* Given a set of raw data, make a scatterplot or regression output using R
* Given a scatterplot, identify patterns such as positive and negative associations
* Given the least squares line and a value of x, calculate the predicted value of y
* Given standard regression output, identify and utilize key parts of the output (estimated slope, intercept, R^2^, etc.)  
* Given a study, interpret the value of the coefficient of determination (R^2^).
* Be able to describe the primary distinction between regression and correlation analysis.  
* If assumptions for linearity fail then use transformations to linearize our data
  
### Optional Skills:  
* State and test the assumptions of inference about the regression model  
* Given a study objective, significance level, and summary statistics, conduct a formal test of significance on a slope based on ANOVA or the t-distribution by conducting the appropriate steps (including stating hypotheses, calculating test statistics, calculating and interpreting p-values and interpreting the conclusion in context).  
* Be able to calculate and interpret the confidence interval for $\beta$ given output from a linear regression analysis.  
* Given standard regression output, interpret the results of the test of hypothesis about the slope.





**Please make sure to show all R code and output after each question so that we can see your work.** Write a sentence for each numerical value produced describing its meaning **in context with the proper units**. If you don't recall how to do something, you should first refer to your textbook, in-class examples, and the primers from Lab #1 and #2, then reach out to your peers and Abhi or me. Of course the internet is a good resource as well.


Here are some symbols that you might find useful:  
$H_0$  $H_1$  $\neq$  $\sigma$  $\mu$  $\mu_0$  $\mu_{word}$  $\rho$  $\beta_0$  $\beta_1$  $\hat{y}$  $\hat{y}_{word}$  

***
START HERE: Beloew are the packages you may need to load to calculate statistics, create graphics, calculate power (optional), etc. in the code chunk below. You should start all labs by loading these in as they are the ones we commonly use.  
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE, comment = "",warning = FALSE, message = FALSE)
require(rmarkdown, quietly=TRUE)
require(ggformula, quietly=TRUE)
require(pwr)
require(mosaic, quietly)



```

*Markdown tip: putting two spaces after a line forces the next line in your markdown document to also be a new line in your knitted document.*

*Markdown tip: equations in Mardown will ignore any attempt to include spaces, unless you insert at `~` inside the equation where you want the space.* For example, in our BAC-Beers problem from class (hover your mouse over them below to see what it would knit like): $x_{number of beers}$ versus $x_{number~of~beers}$ 

*Markdown tip: If you want to test out two lines of code, such as for a plot (such as with `qqnorm()` and `qqline()`), you have to run them __together__, not one at a time.* 

***

### Scenario 1: Muscle Mass

A person's muscle mass is expected to decrease with age. To explore this relationship in women, a nutritionist randomly selected 60 women between 40 and 79 years old. The research objective is to see if there is the expected muscle mass (in kilograms; kg) **linear decrease** with respect to age (in years) as an approximate trend. The data are found in the file `MuscleMass.csv`. 


1.a State the statistical research question for your analysis. 

> Insert answer here
What linear impact does a woman's age have upon their muscle mass?


1.b Name the response variable of interest and state the type (quantitative or qualitative).  Always include your units!

> Insert answer here
Muscle mass (kg), quantitative

1.c Name the explanatory variable of interest and state the type (quantitative or qualitative). Always include your units!

> Insert answer here
Age (yrs), quantitative

1.d TRUE or FALSE? This is an experimental data collection technique (An experiment is where we have randomly assigned the explanatory variable to the individuals/cases). As opposed to an observational study. **Bold** either the word True or False for your answer.
**FALSE**, this is not an experiment. This is an obeservational study with no treatment.


To answer a researcher's questions in the context of the problem (for a specified explanatory and response variable), we should analyze the data using a linear model. We use the following notation for a linear model: 

$$Y_{muscle~mass} = \beta_0 + \beta_1 \cdot X_{age} + \epsilon$$
Note:  the $\epsilon$ in the formula is the error associated with the variability of our data, sometimes called the **residual error**  

*Statisticians use the above formula but the AP uses and Ti calculators use the formula below*  

Note: The AP exam and your Ti calculators use   $$Y_{muscle~mass} = A + B \cdot X_{age}$$  




1.e **When doing statistical inference it's very important to always check your assumptions/conditions to make sure the model you're using to approximate your data is an appropriate one.**  What assumption are we making about the independent and dependent variables by using this particular linear regression? Hint:  What are we choosing to be our explanatory variable and is this reasonable?

> Insert your answer here


1.f*(optional)* State the null and alternative hypothesis both symbolically and verbally to test the slope of the linear regression, given our expected association (i.e., the research objective). Fill in the blanks below as needed to complete the hypotheses.  

**Hint:** The Null hypothesis $H_0$ can be thought of in various ways:  The "status quo", the hypothesis of no change/no difference    
Whereas as the Alternative Hypothesis $H_1$ can be thought of as the hypothesis we are looking to find evidence to support, the hypothesis of change, something is happening that is different than the status quo (this is why we are going to the trouble to test this hypothesis against what is commonly thought to be true)

> $H_0: \beta_1 = 0$  
> The _____________ of a linear model between __________ and _____________ is zero.  
> $H_1: \beta_1 _____ 0$  
> The _____________ of a linear model between __________ and _____________ is __________ zero


1.g Estimate the population regression line using the data (`MuscleMass.csv`). Then, create a scatterplot of the data, including the estimated linear model on the plot. Modify the code below to perform each action listed in the comments.  

**Hint:**  the function to create a linear model is lm(dataframe$response variable ~ dataframe$explanatory variable)  
The function to create a scatterplot is gf_point(dataframe$response variable ~ dataframe$explanatory variable, arguments to label axes)
*remember your units on the axes labels always!*

to pipe use %>%  
The function to add a linear model to your scatterplot after using the piping command above is:
gf_lm(response variable ~ explanatory variable, data = dataframe)

```{python}
x = muscle.Age
y = muscle.MuscleMass
plt.scatter(x, y)

z = np.polyfit(x, y, 2)
p = np.poly1d(z)
plt.plot(x,p(x),"r--")

plt.show()
```


1.h Before drawing any conclusion, we must evaluate the parametric assumptions of linear regression:  **Must always check assumptions before doing statistical inference!**  

#### Assumptions for Linear Regression Inference  

*The scatterplot show that using a linear model is reasonable for the data  (your data follows a linear pattern)  

*The QQ-Plot shows our values fit the theoretical 1:1 line (the resulting cumulative frequency follows that of the normal distribution), thus our assumption that the errors/residuals are normally distributed is reasonable  

*The Residual plot show no left over pattern and most values are within an even range of the zero line.  Thus our errors/residuals have approximately equal variance and the assumption of independence of residuals seems reasonable (note this diagnostic plot can be used to satisfy two assumptions, equal variance and independence of residuals)


Conduct the appropriate testing for the assumptions of regression analysis. Modify the code below to create the additional plots needed to match each description. For each assumption, list the plot you used to verify each one, bold if you think the statement is met or not, and provide a justification below.  

Hint:  To make a residual plot put a 1 in the argument after the name of the linear model.  This code extracts the tge residual plot for testing independence and constant variance of residuals.  
plot(Linear Model, 1)  

To make a QQ plot put a 2 in the argument after the name of the linear model.  This code extracts the qqplot to test normality of residuals.  
plot(Linear Model, 2)

```{python}
stats.probplot(x, plot=plt)
```

TRUE or FALSE? The assumption of linearity seems reasonable.  
> Plot used: 
> Justification: 

TRUE or FALSE? The assumption of normally distributed error seems reasonable.  
> Plot used: QQ plot
> Justification: The ordered values are very close to the expected values except on both ends.

TRUE or FALSE? The assumption of equal error variance (homoscedacity) seems reasonable.  
> Plot used:  
> Justification: 

TRUE or FALSE? The assumption of the independence of the residuals seems reasonable.  
> Plot used:  
> Justification:  

1.i After checking that we can use a model for the null distribution (i.e.the T-Distributiion to get a t-statistic and p-value calculation), we should also check that our estimates are not unduly influenced by any points (outliers, high leverage or influential points). 

We can use another diagnostic scatterplot of 'Residuals vs Leverage (weight/influence each point holds in the overall linear model)' to help determine if there are any highly influential points (influential outliers).  

**Cooks Distance: a measure of each point's importance in determining the regression result.**  `plot(model, 5)`   
  
When looking at the plot, the red contour lines indicate the critical Cook's Distance, which estimates the importance of each observation to the regression.  
  
Smaller distances from the central cluster of observations means that removing the observations has little effect on the regression results and vis versa.  
  
Distances *larger than one* indicate values that have a high influence on the estimate of the slope and regression analysis.  

Distances between 0.5 and 1 indicate values of concern  

We don't want any values to fall past a Cook's distance of 1 (most commonly used value), note:  Cook's distance of 1 will show up as dotted lines so if you don't see them your values are within the acceptable range. plot(Linear Model, 5) will allow you to check for influential points  


Modify the code below to create the plot to check this guideline. Then bold if you think the statement is met or not, list the plot you used to assess the statement, and provide a justification for your decision. 

```{python}
from statsmodels.formula.api import ols

m = ols('Age ~ MuscleMass',muscle).fit()
infl = m.get_influence()
smfr = infl.summary_frame()
smfr
```

TRUE or FALSE? There are no highly influential points that might alter our analysis and estimate of the slope substantially.

> Plot used:   OLS
> Justification:  True, None of the values for Cooks number exceed 1


1.j Modify the code below to create a summary table (the code is summary(Linear Model)), to assess whether there is a statistically significant relationship between the two variables and use the values from the summary to help answer the question below. Then determine the least squares regression line for your linear model (put the slope and y coordinate of the y intercept into the correct spots in the linear model in green below )  

```{python}
from statsmodels.formula.api import ols

m = ols('Age ~ MuscleMass',muscle).fit()
infl = m.get_influence()
smfr = infl.summary_frame()
smfr
```

1.k Interpret the slope of the linear model, in context.

> As Age increases by 1 year, Muscle Mass is expected to decrease by 1.19.


1.l Interpret the intercept of the linear model, in context. (Provide the mathematical interpretation, whether it makes sense or not practically.)

> When Age is zero, we would expect Muscle Mass to be 156.3 kg.


1.m State and then interpret the coefficient of determination.

> R^2^ = 0.750058330358794
> 0.750058330358794 of the variation in the muscle mass is explained by the linear model with age. 


1.n Assess the strength of the relationship using the coefficient of determination. Is age a good predictor of muscle mass?
> The strength of this relationship is very strong since the r^2 value is verhy high.


1.o Determine the 95% confidence interval for the slope of the regression line. Modify the code below to determine the interval, then interpret it in context below.  

Note:  General Confidence Interval Formula is:  Remember you can hover your cursor over the things within the dollar signs to see the equations in math type form  
$point estimate \pm standard error$
where $standard error = (critical value) \cdot (margin of error) $  

Note: Formula for confidence level using the T-distribution is confint(Linear Model, level = Confidence level in decimal form)  

Note:  Our general confidence interval interpretation is this:
**Based on our sample, we are *insert confidence level* confident that the true *insert parameter of interest* is between *insert lower bound* and *insert upper bound*.  **  

Note:  A general version specific for Linear Regression is:  **Based on our sample, we are *insert confidence level* confident that the true slope of the linear regression between *insert Response variable* and *insert Explanatory variable* is between  *insert lower bound* and *insert upper bound*.  **  
 


```{python}
print(-1.19+57*1.677)
print(-1.19-57*1.677)
```

> Fill in the blanks below for our general confidence interval interpretation for linear regression.  

Based on our sample, we are 95% confident that the true value of the linear regression between 40 and 90 is between -96.779 and 94.399. 


1.p Modify the code below to perform a power analysis for your regression model, using an effect size of 0.15 (medium effect size, see below for more info) and significance level of 0.05 (This means your Confidence Level is 95% because they both must sum to 1).  

# Interpret your power analysis below.  

Note:  Power is a good thing, we want as much of it as we can get (because the more power we have the lower our chance of committing a type 2 error)!  The usual minimum threshold we want is 0.80 or 80% Power which in turn gives us a 20% chance we're making a type 2 error ($\beta$ = type 2 error), ($\alpha$ = type 1 error = significance level ) 

Note:  in the code below leave the blank empty after the 'power=' this tells R to find the power (the thing we're interested in knowing here), f2 = (f-squared) is the effect size given by the formula $f^2 = R^2/(1-R^2)$, Commonly it's suggested to use $f^2$ values of $0.02, 0.015, 0.35$ to represent small, medium, and large effect sizes  

$u = 1$ for simple linear regression  

v = residual/error degrees of freedom = sample size n - 2 since we have 2 variables in this case 


```{python}
ftest_power(avg/stdev(muscle.MuscleMass.tolist()), 57, 57, 0.05)
```

> Fill in the blanks below for interpretation of power.


1.q Which of the following statements are true? **Bold** all statements (but not the list-letter) that are true. 

a. The individuals were sampled randomly (i.e., a random sample), so it implies an observational study (i.e., cannot determine causality).  
**b. The individuals were not randomly assigned to their value of the explanatory variable, so this is not an experiment but an observational study instead, so we can't determine causality.** 
c. The individuals were randomly assigned to the explanatory variable, so this is an experiment, so we can say any changes we observed is due to the explanatory variable.
d. The individuals were randomly assigned to the explanatory variable, so this is an experiment, but we can only determine an association, not causality.
e. The individuals were randomly assigned to their value of the explanatory variable, but we cannot generalize to all individuals in the population since there was not also a random selection. 
**f. The individuals were randomly selected, so we can generalize to the population.**


1.r Can we trust the results of your conclusion? Explain your answer, statistically.  

Note:  In order to trust our results we must show we've satisfied the conditions so the model (T-distribution in this case) was appropriate to use to calculate our p-value and our power ananlysis was at least 80%  

Note:(power analysis not needed (unless using it to determine appropriate sample size) if you reject the null hypothesis since there's only a chance you're making a type 1 error). 

> Yes, it looks like our Power analysis yielded a value very close to 1 showing that we can reject the null hypothesis.


***

### Scenario 2: Digoxin 

Digoxin is a commonly used medication for treating domestic cats suffering from congestive heart failure. Its primary benefit is to help the heart muscles contract. While digoxin can be an extremely useful medication, the difference between a therapeutic dosage and a toxic dosage can be negligible, and overdoses frequently occur as it is difficult to estimate the muscle mass of a living cat’s heart accurately. 

Researchers conducted a postmortem study of 144 adult domestic cats (over 2kg in weight) that died from symptoms of congestive heart failure (47 female, 97 male). The goal of the historic study was to better understand the association between an adult cat’s body weight (kg) and heart weight (g), with the ultimate goal to develop a linear model that veterinarians could use to better predict an adult cat’s heart weight (g) given their observed body weight (kg).  The data are in `cats.csv`. 

*Data Source: R. A. Fisher (1947) The analysis of covariance method for the relation between a part and the whole, Biometrics 3, 65–68.*


2.a State the statistical research question of this analysis.

> Is there a linear relationship between body weigh and heart weight?


2.b Identify the variable type by completing the table below by filling in the blanks

Variable | Description                  | Type (Categorical (Cat) or Numeric (Num))
---------|------------------------------|-------------------------------
Bwt      | Body Weight (kg)             |  **Num**
Hwt      | Heart Weight (g)             |  **Num**
Sex      | Sex (F, M)                   |  **Cat**




The researchers start by completing a linear regression analysis for the heart weight (g) against body weight (kg) in all adult cats; they expect that heart weight will increase with body weight, like it does in other mammals.  

**2.c State the alternative hypotheses for a regression hypothesis test of body and heart weight, both symbolically and verbally.  I gave the null as an example so fill in the alternative and tell me why the null hypothesis $H_0$ is what it is.  Note the details like units that I put in $H_0$!**

> $H_0: \beta_1 = 0$  
> The true slope of a linear relationship between body (kg) and heart (g) weight in adult cats is zero.   
> $H_1: \beta_1 > 0$  
> The true slope of a linear relatiobship between body (kg) and heart (g) weight in adult cats is greater than zero.


2.d Modify the code below to perform a power analysis for your regression model, using an effect size of 0.25 (equivalent to an R^2^ of 0.20) and significance level of 0.05. Interpret your power analysis below by bolding the correct decision.  In the future you'll be expected to write this sentence on your own so take note!  

See the power analysis above we did for more guidance if needed.

```{python}
avg = mean(cats.Hwt.tolist())

FTestPower().power(effect_size = 0.15, df_num = 1, df_denom = 139, alpha = 0.05)
```

> We have enough power (over 80%) to detect a true alternative with an effect size of 0.15.  

> We do not have enough power (<80%) to detect a true alternative with an effect size of 0.15.



2.e A useful summary statistic for the relationship between body and heart weight in adult cats would be the correlation, so calculate it by filling in the blanks below.  

Note: use this code to calculate correlation coefficient (r),  `cor(dataframe$Response , dataframe$explanatory)`

```{python}
cats = pd.read_csv("cats.csv")
```


2.f Suppose the parametric conditions are met for this analysis (usually we will check all these like we did in the first example but so this lab doesn't take a year to complete we'll assume they've been on this one).  

Conduct a linear regression analysis on these data. Modify the code below (fill in the blanks/replace) so it will make the scatterplot with a line, create a linear model, and display the summary table for your linear model. 

```{python}
x = cats.Bwt
y = cats.Hwt
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 1)
except:
    z = np.polyfit(x, y, 1)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
m = ols('Bwt ~ Hwt',cats).fit()
m = ols('Bwt ~ Hwt',cats).fit()
infl = m.get_influence()
smfr = infl.summary_frame()
smfr
```

2.g Does the linear model with body weight explain much of the variability in heart weight for adult domestic cats?  
How much variability does it explain? Does that seem like a good model to use for predictions?  Hint:  I'm asking you about the coefficient of determination $R^2$

> r^2 = 0.646620905709151


The researchers notice that the strength of linear relationship may depend on sex of the cat, male and female. To this end, the researchers considered two separate linear models, one for female adult cats and the other for male adult cats: 


```{python}
mcats = list()
fcats = list()
for v in cats.values.tolist():
    if v[1] == "F":
        fcats.append(v)
    else:
        mcats.append(v)
mcats = pd.DataFrame(mcats,columns = ["ID","Sex","Bwt","Hwt"])
fcats = pd.DataFrame(mcats,columns = ["ID","Sex","Bwt","Hwt"])
# Male Cats
print("Male Cats")
x = mcats.Bwt
y = mcats.Hwt
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 1)
except:
    z = np.polyfit(x, y, 1)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
#Female Cats
print("Female Cats:")
x = fcats.Bwt
y = fcats.Hwt
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 1)
except:
    z = np.polyfit(x, y, 1)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
mcats
```


2.h Write the null and alternative hypotheses for a regression hypothesis on heart weight (g) against body weight (kg) for adult domestic cats for each sex (males, females), both symbolically and verbally.  I gave you the first one again as an example to help with the rest

> $H_{0,~males}$: $\beta_{1,~males} = 0$  
> The true slope of a linear relationship between heart weight (g) and body weight for adult male domestic cats is zero.
> $H_{1,~male}$:  $\beta_{1,~males} != 0$
> The true slope of a linear relationship between heart weight (g) and body weight for adult male domesitc cats i not zero.

> $H_{0,~females}$: $\beta_{1,~females} = 0$  
> The true slope of a linear relationship between heart weight (g) and body weight for adult female domestic cats is zero.
> $H_{1,~female}$:  $\beta_{1,~females} != 0$
> The true slope of a linear relationship between heart weight (g) and body weight for adult female domesitc cats i not zero.


2.i Assess whether the parametric conditions of linear regression have been satisfied, for sex group (males, females); include any guidelines we should also check for our analyses. Modify the code to create the appropriate graphics. **For each group**, state the condition, the plot you used as evidence, then whether it has been satisfied. Give a **brief** justification of your decision.  Note in the code below how to subset your data set into Males and Females.

```{python}
mcats = list()
fcats = list()
for v in cats.values.tolist():
    if v[1] == "F":
        fcats.append(v)
    else:
        mcats.append(v)
mcats = pd.DataFrame(mcats,columns = ["ID","Sex","Bwt","Hwt"])
fcats = pd.DataFrame(fcats,columns = ["ID","Sex","Bwt","Hwt"])
# Male Cats
print("Male Cats")
x = mcats.Bwt
y = mcats.Hwt
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 1)
except:
    z = np.polyfit(x, y, 1)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
stats.probplot(x, plot=plt)
m = ols('Bwt ~ Hwt',mcats).fit()
m = ols('Bwt ~ Hwt',mcats).fit()
infl = m.get_influence()
smfr = infl.summary_frame()
smfr
x = list()
for i in range(len(smfr.values.tolist())):
    x.append(4.313*mcats.Bwt.tolist()[i]-1.184)
y = smfr.standard_resid
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 4)
except:
    z = np.polyfit(x, y, 4)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
plt.scatter(smfr.standard_resid, smfr.hat_diag)
plt.show()

#Female Cats
print("Female Cats:")
x = fcats.Bwt
y = fcats.Hwt
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 1)
except:
    z = np.polyfit(x, y, 1)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
stats.probplot(x, plot=plt)
m = ols('Bwt ~ Hwt',fcats).fit()
m = ols('Bwt ~ Hwt',fcats).fit()
infl = m.get_influence()
xmfr = infl.summary_frame()
xmfr
x = list()
for i in range(len(xmfr.values.tolist())):
    x.append(4.313*mcats.Bwt.tolist()[i]-1.184)
y = xmfr.standard_resid
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 1)
except:
    z = np.polyfit(x, y, 1)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
plt.scatter(xmfr.standard_resid, xmfr.hat_diag)
plt.show()

```

*Male Cats Regression*
Condition/Guideline             | Plot              | Satisfied or Violated?  | Justification
--------------------------------|-------------------|-------------------------|-------------------
 Linearity                      |Normal Linear Reg  |Satisfied                |There appearse to be a strong linear association between bodymass and heart weight.
 Normality of Residuals         |Residual V Fitted  |Satisfied                |The residuals and the fitted values seeme to have a strong linear association.
 Constant variance of residuals |Residual V Fitted  |Violated                 |The rediduals do not rest a constant distance from 0 meaning that they are not of constant variance.
 Independence of residuals      |Residual V Leverage|Violated                 |The correlation is approximatly linear so the residua;s are not independent.
 No Influential Points with Cooks Distabce beyond CD=1 |Redidual V Fitted  |Satisfied | There were no points that had a cooks distance greater than one.
  
Note:  In the future you will need to remember/be able to look up all the conditions (like the five conditions above) for each kind of significance test   

*Female Cats Regression*
Condition/Guideline             | Plot              | Satisfied or Violated?  | Justification
--------------------------------|-------------------|-------------------------|-------------------
 Linearity                      |Normal Linear Reg  |Satisfied                |There appearse to be a strong linear association between bodymass and heart weight.
 Normality of Residuals         |Residual V Fitted  |Satisfied                |The residuals and the fitted values seeme to have a strong linear association.
 Constant variance of residuals |Residual V Fitted  |Violated                 |The rediduals do not rest a constant distance from 0 meaning that they are not of constant variance.
 Independence of residuals      |Residual V Leverage|Violated                 |The correlation is approximatly linear so the residua;s are not independent.
 No Influential Points with Cooks Distabce beyond CD=1 |Redidual V Fitted  |Satisfied | There were no points that had a cooks distance greater than one.



2.j Create a summary table for the linear regression for each sex (one summary for males and one sumary for females). Using the tables, determine the least squares regression lines for your linear models of each species group.
See how we did this in earlier example if needed.  

```{python}
m = ols('Bwt ~ Hwt',cats).fit()
m = ols('Bwt ~ Hwt',cats).fit()
infl = m.get_influence()
smfr = infl.summary_frame()
smfr
```

> Write linear regression lines here for male and female cats in using math notation $'s!  See earlier problem for example if needed



2.k Based on our fitted linear model, if we observe a male cat with a body weight of 3.1 kg, what is the cat’s estimated heart weight (g)? Show your calculations. and fill in the blank for your interpretation below.


> If a male adult cat's body weight is 3.1 kg, we would expect (or predict) it to have a heart weight of 12.1863 g.

in the future and on the AP you'll be expected to write this sentence out on your own and remember to use the word predict or expect (your choice)!


2.l Which sex has a linear regression with stronger prediction power? Provide and compare relevant statistics (compare the $R^2$ values for males and females) then justify your answer by saying which line has a stronger prediction power using the interpretation of $R^2$ in context.

> Insert answer here

THe R^2 value for the male cats is higer than for the female cats indicating a stronger predictive power

2.m **TRUE** or FALSE? (Bold your answer).  Based on the results of the t-test (specific type of hypothesis test that uses the student T-distribution), we have strong evidence agaist the null hypothesis that $\beta_{1,~male} = 0$ in favor of the alternative hypothesis that $\beta_{1,~male} > 0$. There is a positive linear relationship between between an adult male cat's body weight (kg) and heart weight (g). 


2.n TRUE or **FALSE**? (Bold your answer). (Bold your answer). If there is no association between heart and body weight in female adult cats (i.e. $H_{0,~female}: \beta_{1,~female} = 0$) is true), the probability of observing a t-test statistic of 4.215 or greater is 0.00119.


2.o Do you trust your results of your regressions? Justify your answer. 

> Insert your answer here
I would not trust the results because the r^2 values are relativly low.

2.p Can we determine if body weight **caused** the heart weight in a cat? Explain why or why not with statistical reasoning. 

> Insert your answer here.
The T-test establishes a value less than 0.05 allowing us to reject the null ghypothesis, however our r^2 values are rather low.

2.q Can we **generalize** our results to all adult cats with congestive heart failure? Explain why or why not with statistical reasoning. 

> Insert your answer here.

It seems likely since we had a random sample we can generalize the results to all adult cats.


***

### Scenario 3: Suspended Sediment

Runoff from agricultural fields, urban areas, and construction sites can carry away soil, producing cloudy or muddy water. During periods of increased runoff (i.e. storms) the discharge (flow) of water in rivers, creeks, and streams, increase and this increase flow is known to carry away more soil from the terrestrial environment. Soil in the water, called suspended sediment, blocks out the sunlight that bottom-dwelling plants in lakes and rivers need to survive. If these bottom-dwelling plants, called submerged aquatic vegetation (SAV), are deprived of sunlight for extended periods, they will die.

You are working as a hydrologist to characterize the relationship between suspended sediment concentrations (mg/L) and water discharge (ft^3/s /mi^2) at the confluence of a tributary to the Salinas River, CA. You carefully monitor rain events and discharge at the confluence and collect 100 random water samples from the same bridge location. For each sampling event you note the discharge rate and return to the lab where you measure the concentration of suspended sediment (mg/L).  You know that previous studies of discharge and suspended sediment concentrations on coastal streams of North America suggest a variety of log-linear based relationships.
 The data are found in `salinas.csv`.

3.a Test the parametric assumptions and guidelines of linear regression for the simple linear regression of `sediment` as a function of `discharge`. Insert the necessary code and then assess the conditions below. 

```{pythons}
salinas = pd.read_csv("salinas.csv")
x = salinas.discharge
y = salinas.sediment
plt.scatter(x, y)
try:
    z = np.polyfit(x, y, 1)
except:
    z = np.polyfit(x, y, 1)
p = np.poly1d(z)
print(p)
plt.plot(x,p(x),"r--")
plt.show()
m = ols('Bwt ~ Hwt',cats).fit()
m = ols('Bwt ~ Hwt',cats).fit()
infl = m.get_influence()
smfr = infl.summary_frame()
smfr
```

Condition                | Plot            | Satisfied or Violated?  | Justification
-------------------------|-----------------|-------------------------|-------------------
Linearity                |Linear Regression|Satisfied                |
                         |                 |                         |
                         |                 |                         |
                         |                 |                         |
                         |                 |                         |

Hint: one or two or the above conditions should not be satisfied (you should be able to tell from your diagnostic plots)    

Sometimes, the linear model assumptions are satisfied after taking an appropriate transformation of the explanatory variable and/or the response variable.  

We will try the most common transformation (Logs) to see if we can transform our data closer to linearity.  More specifically let's try taking the log-base-10-transformation on the explanatory variable and see if that leads us to satisfying our linear model assumptions.  


3.b Now assess the parametric assumptions and guidelines of linear regression for the transformed linear regression of `lm(sediment~log10(discharge))`. Most of the code has been provided for you, fill in any blanks and replace general words like dataframe, transformation (log10, ln, x^2, etc), piping symbol (%>%), and response/explanatory with the appropriate terms for this problem.  

List each assumption, the graph used to assess it, and whether you think the assumption has been satisfied or violated, justifying your answer.  
Note: I'm calling the transformed linear model sed.log.lm but you could call it whatever you want (it's nice to get a pattern going like first three letters of variable/dataframe then the transformation your using, then what model, or something similar)  

Note: Also remember we have to always label the transformed variable on our graphs

```{r}
sed.log.lm<-lm(dataframe$response~log10(dataframe$explanatory)) # this is our newly transformed linear model

gf_point(dataframe$response~transformation(dataframe$explanatory), xlab=expression("Log of Discharge (ft"^2~"/s / mi"^2~")"), ylab="Sediment Concentrations (mg/L)", title = "Salinas River") %>%
  gf_lm(salinas$sediment~log10(salinas$discharge), col=1)
plot(transformed model, ___)
plot(transformed model, ___)
plot(transformed model, ___)
```

Condition                       | Plot            | Satisfied or Violated?  | Justification
--------------------------------|-----------------|-------------------------|-------------------
 Linearity                      |                 |                         |
 Normality of Residuals         |                 |                         |
 Constant variance of residuals |                 |                         |
 Independence of residuals      |                 |                         |
 No Influential Points          |                 |                         |
 no value beyond CD=1


Take-home message: Sometimes, the linear model assumptions are satisfied after taking an appropriate transformation of the explanatory variable and/or the response variable. In the data (salinas.csv), the log-base-10-transformation on the explanatory variable led to satisfying linear model assumptions.  If you want you could now proceed with your statistical inference using the t-distribution as our probability distribution (density curve) to calculate a p-value



