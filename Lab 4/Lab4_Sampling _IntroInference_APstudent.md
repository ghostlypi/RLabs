---
title: 'Lab #4: Data Collection & More Introduction to Inference '
date: "AP Stats KLS - Fall 2020"
output: html_document
---


### Name: 



## Skills

* Describe and identify sampling techniques and any potential biases from them.  
* Describe the sampling distribution of a statistic and define the standard error of a statistic.  Be able to distinguish the standard deviation from the standard error.  
* Given a study, describe the sampling distribution of $\bar{x}$ as specifically as possible.   
* Explain that in order to determine if there is a relationship or underlying circumstance that explains the observed characteristics of our sample data, we must compare that observation of a perceived difference or relationship to what might occur simply by random chance.  
* Identify and define the null and alternative hypothesis.  
* Evaluate p-values, test statistics and other information to assess the results of a hypothesis test.  
*	Draw specific (AP/Old School way) and general conclusions (New way that most researchers and Universities are teaching) based on the results of the hypothesis test; interpret the information in context.  





 **Please make sure to show all R code and output after each question so that we can see your work.** Write a sentence for each numerical value produced describing its meaning **in context with the proper units**. Be sure to submit your full project as a .zip file that includes your edited, renamed .Rmd file to receive credit. If you don't recall how to do something, you should first refer to your lecture notes, in-class examples, and the primers from Lab #1 and #2. Your lecture notes and readings on these topics are also good resources. This lab may be completed **in groups as always.**


***
 **Reminder**: Before starting this lab, let us load the "ggformula" and "mosaic" packages we need for statistic and graphical functions. **You can install these packages either through the console using install.packages or by using the packages tab on the right side of rstudio.** Input the following two lines in the code chuck below.
 
require(ggformula)  
require(mosaic)

```{r, message=FALSE}


```

***

## Part 1: Data Collection: Southern bull-kelp

A study was interested in examining long-distance dispersal of southern bull-kelp (*Durvillaea antarctica*, google it to see a picture of what the kelp looks like!) adults in coastal New Zealand to understand connectivity between coastal populations. (Invertebrates can 'raft' on the detached kelp, which also remains alive until beach-cast (spilled up onto the beach).  
Given part of their written methods below, answer the questions that follow. 

*Methods* (excerpt)
Collection of beach-cast *D. antarctica* samples from seven field sites spanning the Canterbury Bight region was performed in March 2009 and again in April/May 2010. At individual field sites, we typically sampled across approximately 0.5-2.0 km of coastline. Where possible, we sampled only the beach-cast specimens that included a holdfast and/or primary stipe to ensure that individuals were not samples more than once. In the cases (primarily in 2010) where relatively low numbers of intact specimens were found at some sites, we collected tissue from large pieces of *D. antarctica* that were clearly separated (e.g. >20 m) from other such pieces, again to avoid repeated sampling of individual specimens. We generally targeted specimens stranded at or above the high tide mark and sampled the dried tips of their fronds to maximize success with DNA extraction. Typically, between 20 and 30 samples were collected per site per year, with a small piece (a few cm) of frond tissue preserved in 95% ethanol before being transferred to silica gel.

For all multiple choice questions, **bold** (or __bold__) your answers but do not include the beginning letter or ending double spaces. For example: a. **this answer**. 

1a: What is the population of interest in this study?

  a. all drifting *D. antarctica* in the Canterbury Bight  
  b. all beach-cast *D. antarctica* in New Zealand 
  **c. all beach-cast *D. antarctica* in the Canterbury Bight**  
  d. all *D. antartctica* in the Canterbury Bight


1b: What is one case in this study?

  a. one *D. antarctica*  
  b. one month
  c. one coastline  
  **d. one field site**  


1c: What type of sample design did the researchers employ?

  a. Stratified Random Sample  
  b. Simple Random Sample  
  **c. Convenience Sample**  
  d. Volunteer Sample


1d: Biological studies can't always use a SRS like other fields, as they often don't have a sampling frame. How could the researchers introduce randomization into their study (what could they physically do while collecting the kelp on the beach to collect it in a random way)?

> They can sample on different days to 



1e: If the researchers assumed that the kelp on the beach was already a random sample of the kelp drifting in the ocean, would that satisfy you that they could generalize their sample to the population? Why or why not?

> No, the kelp that drift to land might have been affected by an external factor such as proximity to land and cannot be compared with ocean kelp.



***

## Part 2: Sampling Distribution Properties

2a: Define the following terms in *general* (not just for this kelp study):

> Population distribution:  The distribution of the entire population of individuals.


> Sample distribution: The distribution of the sample collected


> Sampling distribution:  The diversity of the sample collected.


2b: Describe the following characteristics for the sampling distribution, being as specific as you can for a *general* sampling distribution (not just for this kelp study), use the appropriate greek letters and subscripts:

Hint: Here are the symbols and words you should use (remember you can hover over them): $\mu_{\bar{x}}=\mu$, $\sigma_{\bar{x}}=\sigma/\sqrt{n}$, symmetric, unimodal, bell-shaped; normal 

> Center: $\mu_{\bar{x}}=\mu$ The center is a measure of the average of the individuals within a 


> Spread: $\sigma_{\bar{x}}=\sigma/\sqrt{n}$ The spread is a measure of how far data is from the center.


> Shape:  Is the distribution of data points. Things ot consider include:"Is the graph symetrical?", "Is the graph unimodal(1 peak), bimodal(2 peaks) or polymodal(multiple peaks)", "What is the shape? is it bell shaped, skewed left, or skewed right?", and "Is it normal, binomial?"


2c: Why is there variation around the center of the sampling distribution in *general*?  Think about how samples vary, and what this means for the sample means that make up the sampling distribution of the sample means and how the size of our sample effects the variability and how well our sample will represent the true population and how different samples make our estimates (statistics) of the population (parameters) better or worse.

> Insert your answer below.



2d: How Does/Doesn't the underlying population (the population from which you are taking samples) distribution affect the sampling distribution center? Explain why this is so.

> Insert your answer below.



2e: In the table below fill in the values in the last column to get practice calculating the standard error for a sampling distribution and to see how the sample size effects the standard error (spread/variability). The population standard deviations is given below. 

*Play around with the applet at the link below to see visually what's going on between the difference between the TRUE sampling distribution of ALL POSSIBLE samples which is what this calculation is for.*

*Note: if you want to see the standard error change visually, go to the [applet](www.rossmanchance.com/ISIapplets.html), click on "Sampling Words" and then the check box for "Show Sampling Options) and run your simulations of a sampling distribution at different sample sizes, check the circle next to 'fixed' for "scale" under the sampling distribution options. This will keep your axis from rescaling as you run different sampling distributions. (Be sure to start with n=10 if you do this!)*

Population standard deviation: $\sigma_{1}=1.51$; Goal here is to see how the theoretical Standard error calculation (last column) compares to those of actual values from specific samples of different sizes (middle column) and how by increasing the sample size we can get closer to the TRUE Population Spread


|     n     |   $\mu_{\bar{x}}$  |  $\sigma_{\bar{x}}$  |  $\sigma/\sqrt{n}$  |
|:---------:|:------------------:|:--------------------:|:-------------------:|
|  10       |        7.978       |     0.481            |                     |
|  50       |        7.997       |     0.215            |                     |
|  100      |        7.998       |     0.152            |                     |
|  1000     |        7.999       |     0.047            |                     |
  


2f: How does the calculation of standard error compare to your estimated standard error from the graph? Why is there a difference, if any?

> Insert your answer below.



***

## Part 3: Data Collection - Penny Age

3a: Collect your own sample (try to figure out how to do it randomly if possible) from *at least* 30 pennies (or coins of any kind you can find, check the couch!) for the variable: what is the age (in years) of the penny/coin? Calculate the age of the penny/coin from 2019 (we are going to assume no 2020 pennies/coins are in circulation yet). 

Describe your sampling design below.  Make sure to describe your sampling design so I can tell if it's random, convienence, volunteer, etc.  

*Note* I know we're in a coin shortage now so if you can't find 30 pennies/coins then think of something else around your house you can get at least 30 individuals for or else use this applet to simulate randomly selecting 30 or more pennies *Note* it will be more fun if you actaully collect them on your own!  

Go to http://www.rossmanchance.com/ISIapplets.html  
- Click 'one mean', then select 'pennies', select at least a sample size of 30

> Insert your answer below.



3b: Make a vector of your data and store it as `age` in the code chunk below. If you don't recall how to use the function `c()`.  *Note* change the name of the vector from 'age' to something appropriate if you aren't using coins.  Example:  Your vector below shoud look something like age<-c(0,0,1,2,2,13,14,14,21, ...,41) if using coins where 0 represents a coin from 2019, 1 represents a coin from 2018, etc.

```{r}
age<-c(_____)
```

3c: What type of sample did you take?

> Insert your answer below.



3d: What is the population of interest in this scenario?

> Insert your answer below.



3e: Create a histogram and then a boxplot of your sample distribution, making sure to label it appropriately.

**Add code chunk here, and use the gf_histogram() and gf_boxplot() function we've used before, make sure to label axes appropriately and specifically always!**



3f: Describe your distribution, discussing the four characteristics of shape, center, spread, and outliers. 

> Insert your answer below.



3g: Calculate the descriptive numerical summaries to best quantify your distribution's center and spread (will depend on if your distribution is approx. symmetric or skewed on what stats you use) . Write the values below using symbolic notation (e.g.: symbol = value). 

**Add code chunk here**

> Insert your answer below.



3h: Regardless of what you calculated in 3g, calculate the mean $\bar{x}$, standard deviation $s$, and sample size $n$ of your data, using R code for all three. Write the values below in the green section after you plug your varible name into the functions in the code chunk below to calculate the values. 

**insert into code chunk below**
```{r}
mean(~_______)  
sd(~_______)  
length(______)  

```


> Insert your answer below.



3i: Fill in the blank, bolding the words you enter in the blanks. 

*Note*
The mean and standard deviation above are **statistics** (numeric summaries from a sample) because they were measured on a **sample**.  This is also why we aren't using greek letters to represent them since those are reserved for parameters (numeric summaries from a population).





***

## Part 4: Inference

In 1999, the population mean age of pennies in circulation was $\mu = 12.264$ years, with a population standard deviation of $\sigma = 9.608$ years. Let's see if your sample mean age of pennies in circulation in 2019 differs from the the mean from 1999. If you didn't use pennies or some coins of some kind then I guess compare what you did find to this data.

4a: What is the general research question?

> Insert your answer below.



4b: What is the population of interest in this study?

> Insert your answer below.



4c: What is the parameter of interest in this study?

> [insert appropriate symbol here] = [state parameter of interest in words]
> (Insert your answer below).



4d: State your null and alternative hypotheses, both symbolically and verbally. Use these symbols and also write out in words your null and alternative hypothesis: $<, >, \neq$,  $H_0$, $H_1$
Hint:  the symbol part of the null hyp. will be $H_0: \mu = 12.264$  

> Insert your answer below.



4e: Fill in the table describing what each symbol represents, whether it represents a parameter or a statistic, and the values of each in this context.

Symbol    | Description        | parameter or statistic? | Value (with units)
--------- | ------------------ | ----------------------- | ------------------
$\mu_0$   |                    |                         |          
$\bar{x}$ |                    |                         |           
$s$       |                    |                         |           
$n$       |                    |                         |            



4f: Check the conditions for completing a hypothesis test for a single mean on your data. 

> 1. Random sample: [Met?]; [Justification]  
  2a. Population is normally distributed: No. Move on to 2b.  
  2b. $n \geq 30$: [Met?]; [Justification]  
    Conditions for hypothesis test [failed / satisfied]


4g: Evaluate the likelihood of getting your sample of pennies/coins/whatever if the null hypothesis is true. Use the applet to simulate a null model and determine the likelihood of getting a sample as extreme as your sample mean.  aka find the p-value!
- Go to http://www.rossmanchance.com/ISIapplets.html  
- Click 'one mean', then select 'pennies' and change the variable to 'age'  
- Click 'show sampling options', then simulate a sampling distribution with 10000 samples of the same size as the one you took in part 3.  
- Under the sampling distribution, you want to 'count samples "[chose the option that matches your alternative hypothesis (beyond matches not equal to)]" and then fill in the field with your sample mean. Click "count."  
- The count in red will display the number of samples out of the samples you simulated which had sample means that were as or more extreme than the sample mean from your sample.  

> Record that proportion below.



4h: Draw another sampling distribution and calculate the likelihood of getting a sample mean as or more extreme than yours. 

> Record that proportion below.



4i: Were the proportions the same? If they were not, explain why. If they were the same, try it a few more times and then explain why  some varied. 

> Insert your answer below.



4j: Let's use a model to find our likelihood, instead of an estimated sampling distribution, even though this is fun and using simulations it's quicker/more efficient if we can use our theoretical probability distributions to do our inference (which we can as long as we've checked our conditions to make sure they're satisified to use these to model our data)!  
- Click in the top green bar 'theory-based inference'  
- Change the scenario to 'one mean'  
- Enter your $n$, $\bar{x}$, and $s$ into the fields, then 'calculate'  
- Click "Test of Inference".  
- Enter the correct null value and click the inequality until it matches your null and alternative hypotheses.  
- Click 'Calculate.'  

> Record the standardized test statistic and p-value that is returned.



4k: Interpret your p-value in the context of the question.

> There is a **[insert p-value]** probability of getting our test statistic of **[insert test statistic]** or more extreme, if the **[write parameter of interest]** is **[insert null value]**. 


4l: Was your p-value the same as the value you got from your simulation? Why or why not?

> Insert your answer below.



4m: Write a specific (using the reject or fail to reject language) and general conclusion (using the p-value and other pieces of evidence from our EDA (descriptive statistics like, graph of your data, one or more of the summary stats form your data, CI's, etc, that back up your conclusion)) about your population citing two pieces of evidence; your hypothesis test/p-value can only be one. 

> Insert your answer below.
Specific Conclusion (AP):
General Conclusion:


4n: What can you say, in general, about the age of pennies in your population? *(Hint: think both about your hypothesis test, and about the sample you took. Can you generalize?)*

> Insert your answer below.



4o: To use the model, our conditions from 4f needed to be satisfied. What if you hadn't met those conditions? What would that mean for your conclusion?

> Insert your answer below. 



Before you finish -- check your knitted document. Is it easy to read? Do you need to add spaces anywhere to create line breaks? Did you accidentally delete any of the answer formatting, etc?  Get in the habit of always doing this and to remind yourself that you're creating an easy to read awesome Markdown doc when all said and done!
