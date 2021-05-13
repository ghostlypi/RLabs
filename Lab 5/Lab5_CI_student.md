---
title: 'Lab #5 - Confidence Intervals for One Population Mean'
date: "KLS Stats - Spring 2021"
output: 
  html_document: default
---


### Name/s: 



## Skills

*  To recognize and pull out key information from a research scenario  
*  Given a study objective, determine whether significance testing is appropriate
*  Identify potential types of error given a significance test  
*  Construct a confidence interval for a population mean  
*  Given a confidence level ($1-\alpha$), determine the critical value (t*) needed to construct the confidence interval   
*  Construct and interpret a one sample interval for the mean based on the t-distribution  


**Please make sure to show all R code and output after each question so that Abhi can see your work.** Write a sentence for each numerical value produced describing its meaning **in context with the proper units**.
 
You may work on this lab individually or in groups, but each person turn in their own completed lab to Canvas.


Here are some symbols that you might find useful:  
$H_0$ $H_1$ $\sigma$ $\mu$ $\mu_0$ $\mu_{word}$ $\neq$

***

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE, comment = "", warning = FALSE, message = FALSE)
require(rmarkdown, quietly=TRUE)
```


<span style='color:#000000;background:#ffc0cb;'>
<b>2 points.</b>  Rmd file knits  </span>






## Scenario 1: The Advertising Campaign

A non-profit that delivers clean water devices world-wide generally averages 11 thousand dollars in donations daily. In hopes of expanding, the non-profit recently ran a print campaign to raise awareness and drive traffic to their website, hopefully resulting in an increase in **donations**. The ads ran each Sunday. Suppose you work for the company, and *you have been asked to see if the campaign has resulted in an increase in the true mean daily donation*. Suppose you randomly sample 40 days from the six months following the campaign started. From the sample, you calculated a mean daily donation of 11.4 thousand dollars with a sample standard deviation of 1.57 thousand dollars. 


1.a. In the scenario above, bold the parameter of interest and italicize the research question. You may need to use a combination of `**` and `_` if they overlap -- check the RMarkdown resources if you don't recall how to use either `*` or `_`.  Hint:  `**` can be used for bold and `_` can be used for italicize or `*` if they don't overlap.

1.b. Recall that a confidence interval gives an estimate for our parameter of interest `true mean daily donation` by computing our point estimate (sample mean in this case), and adding/subtracting the margin of error (which is the product of our critical value and standard error), so we end up with an interval (a lower bound and upper bound) that may contain the true value of our parameter of interest.

From the formula sheet (including in your project directory with this lab, click to open it from the file menu in the bottom right), this is the same formula sheet you get with your AP exam, you can see the formulas used to calculate the standard error, note we find the critical values using our calculators.  You'll be asked to do these by hand on the exam so make sure you can do that too but in the real world we use R to calculate these things, so we'll practice both.

Let's go over the assumptions to see if we can use the t-distribution in the first place:  

-$\sigma$ is unkown ($\sigma$ = population standard deviation) which commonly the case in the real world
- random sample
- sample size is 30 or larger or the sample comes from a roughly symmetric distribution without major outliers (aka approximately Normal)


General Formula for a Confidence interval $statistic ± (critical value)(standard error of statistic)$ or written more compactely as $point estimate ± M.O.E$   
Note: MOE = Margin of Error

Calculate the 95% confidence interval (CI) for the true mean daily donation levels after the campaign started by modifying the code chunk below to enter the appropriate values or object names for the blanks. I've included the summary stats for the data set (not included). Add comments to the code, using `#`s to describe what each line of code is doing.
Note:  confidence intervals are always two tailed so we need to split our significance level $\alpha$ into two by dividing it by 2 as seen in the formula below.



```{python}
xbar=11.4 # sample mean
s=1.57 # standard deviation
n=40 # sample size
se=s/sqrt(n) # stderr
#(tcrit<-qt(1-(se)/2, (n)-1)) # t-interval

(lower<-______-______*______) # describe here
(upper<-______+______*______) # describe here
```
*T interval calculated by Abhi due to Tech diffs*
1.c. Write your final confidence interval below.

> (10.898, 11.902)


1.d. Based on the confidence interval, are you confident to claim the true mean daily donation after the campaign could be the **same** as the value it was before the campaign stated, 11 thousand dollars? Why or why not? Fill in the brackets in the sentence below. Possible words/ values to insert include: \$11.4k, 1.57, 40, $11k, 5%, 95%, true mean, sample mean, population, sample. **Bold** your inserted/selected words/phrases. 

> Our interval [DID] capture the null value (before-campaign mean of [11]). Assuming our sample is one of the [95%] that would contain the [profit], then the mean daily donation after the ad campaign [WOULD BE THE SAME] as the mean daily donation before the campaign started. 


Recall: Suppose you decided to take a second sample to revisit and revise your question. This time, instead of selecting *any* day in the six months of the campaign, you randomly select *only* from days that the print campaign ran (i.e., a random selection of Sundays from the six months). You randomly selected 10 Sundays, and you calculated a sample mean daily donation of 11.94 dollars (in thousands) and a sample deviation of 1.57 thousand dollars. 

1.e. Should you calculate a confidence interval for this sample, given that $\sigma$ is unknown and your sample size is small? What additional information would you need to know to meet the conditions for calculating a confidence interval?  

> Insert answer here
We need to know if the data is normal.

1.f. Assuming your sample is roughly symmetric, calculate the 95% confidence interval for this new sample. Compute each part seperately below for practice but you can use theuse the `t.test()` function which we would normally do to check your work.  See #2c for help with t.test function or use the help menu.

**Modify the Code below**


```{r}
xbar<-11.4     # stores sample mean value
s<-1.57       # stores sample sd value
n<-40         # stores sample size
se<-s/sqrt(n)  # calculates sample standard error and stores as object se
(tcrit<-qt(1-0.05/2, n-1))   # calculates t critical for two tailed test with C=95%, stores as object tcrit and prints to screen
(lb<-xbar-tcrit*se)   # calculates, prints and stores 95% CI lower bound
(ub<-xbar+tcrit*se)   # calculates, prints & stores 95% CI upper bound
```

1.g. Interpret your confidence interval from #1.6 in the context of the scenario. Edit the [placeholder]s to add in the specific values/context from this question, using in-line code where possible. The placeholders may stand in for a word, phrase, value, values, or mathematical notation. Bold your inserted answers. 

> Based on our [assumption], we are [95%] confident that the [profit] is between [10.81689] and [13.0631] [thousands of dollars].


1.h. Based on the **confidence interval**, are you confident to claim that the non-profit has increased their mean daily donation rate by running the ad campaign? Why or why not?

> Insert answer here
No, we are not confident since the original mean stays within the 95% confidence interval of the old mean.

1.i. Let's say we ran a one tailed hypothesis using our same data set and concluded to reject the null in favor of the alternative that the true mean Sunday donation rate was greater than 11k. Does this conclusion agree with your confidence interval? What about the tests for confidence intervals and hypothesis tests might differ that could give us different results?

> Insert answer here
This conclusion disagrees with our confidence interval. The hypothesis test may differe because it is one sided and therefore does not have an expansive alternative hypothesis.

***
## Scenario 2: Run differential in Baseball

Baseball is a game for statistics lovers. One particular statistic is the mean run differential, or the mean number of runs between the winning and losing teams' scores -- in other words, by how many points a particular team wins or loses games, on average. You'd like to know if your favorite team is, on average, winning games (having a run differential greater than zero). You recorded the run differential for your favorite team for a random sample of games through the season. We can read them into R as follows:

```{python}
rd=[3, 1, -1, -4, -2, 5, 2, 1, 1, -1, 3, -4, 4, 2, 1, 1, -1, 6, 10, 2, -1, -2, 3, 2, 1, -1, 3, 2, -1, -2, 1, -3, -1, 1, -4]
```

In the above sample, a positive value implies your favorite team won the game by that many points. In this scenario, our objective is to perform the hypothesis testing and estimate the parameter of interest (i.e. the true mean run differential).


2.a. Explain why it is okay or not to use a t-test. Check your conditions!

> Insert answer here
Random: "random sample of games"
Normal: We don't know if it's normal, skip to next param
Large Number: There are 35 samples > 30
10%: 35 games is less than 10% of all the games played by favorite baseball team.

2.b. Calculate the appropriate statistics for `run.diff` which are needed for the t-test. Hint:  We will need to know: length/# entries of our data set, mean, standard deviation (sd), aka $n, \bar{x}, sd$

>Insert code chunk here to find the stats mentioned above
\bar{x} = 0.7714285714285715
n = 35
sd = 2.951427513890168

2.c. Conduct a hypothesis test, using the `t.test()` function. Modify the code below by replacing the blanks. Now that you know how to compute all the pieces of our tests individually we'll just use the simpler t.test function that does all the work for us! 

```{r}
t.test(______, mu=______, alternative="______")
```
p = 0.5
 
2.d. Calculate the 95% confidence interval, using the `t.test()` function. Modify the code below by replacing the blanks.  Note 1: confidence intervals are always two-sided or tailed.  Note 2:  we just add the $conf.int at the end of the t.test function to make it compute a CI instead of a hyp test.
```{r}
t.test(______, alternative="______", conf.level = ______)$conf.int
```
*Note: your confidence interval should be two values (not "Inf"). If you are seeing something else*

[-0.24242265, 1.78527865]
2.e. What can you conclude from your hypothesis test and confidence interval about the true mean run differential for your favorite team?  Write out the conclusions to both and compare.  Do they complement or contrast each other?

> Insert answer here
They do complement each other. Our P of 0.5 is within our interval from [-0.2424, 1.7853].


***

## Scenario 3: Koala Mate Preference

Male koalas bellow during the breeding season, and researchers wanted to know if females display a preference for larger males from only hearing the bellows, or if she displays no preference for male size based on bellows. Charlton et al. (2012) measured responses of estrous female koalas (i.e., females ready to mate) to playbacks of bellows that had been modified on the computer to simulate male callers of different body size. Randomly selected females were placed one at a time into an enclosure while hidden loudspeakers played bellows simulating a larger male on one side (randomly chosen) and a smaller male on the other side. Male bellows were played repeatedly, alternating between sides, over 10 minutes. Females often turned to look in the direction of the loudspeaker (invisible to her) during the trial. The researchers measured preference for the larger male as the number of looks towards the larger-male side minus the number of looks towards the smaller-male side. Thus, a positive value is interpreted as a **female looked most often toward the larger male** (i.e., preference for the larger male), and a negative value is interpreted as she looked most often in the direction of the smaller male. Higher magnitudes of the score (the absolute value of an individual's score) is interpreted as a stronger preference. A score of 5 would mean the female looked towards the larger male 5 times more than she looked towards the smaller male; a score of -12 would mean the female looked toward the smaller male 12 times more than she looked toward the larger male. No preference would have a score of 0. The following data measure the mate preference for the larger male of each of 35 females: 

5, 7, 10, -3, -4, 5, 6, 3, 2, 3, 7, 4, 6, -4, 2, 2, 14, 2, 
3 ,-1, 9, 3, -3, 8, 2, -3, 2, -5, 7, -2, 12, 5, -9, 9, 4



3.a. In the text above, bold the research objective.

3.b. Calculate the relevant summary statistics for the t-test and confidence interval (same as we did in #2).
n = 35
\bar{x} = 3.0857
sd = 5.1127
< Insert code chunk here; annotate/comment your code to describe what descriptive statistic each line calculates >
```{python
arr=[5, 7, 10, -3, -4, 5, 6, 3, 2, 3, 7, 4, 6, -4, 2, 2, 14, 2, 3 ,-1, 9, 3, -3, 8, 2, -3, 2, -5, 7, -2, 12, 5, -9, 9, 4]
print(len(arr)) # sample size
print(mean(arr)) #sampe mean
print(stdev(arr)) #sample stdev
```

Now we will want to conduct a hypothesis test. 

3.c. Have the conditions been met to perform a hypothesis test? 

> Insert answer, and run the code chunk below to help see if they are satisifed. Remember how we do boxplots because they come up a lot!

```{r}
darr = pd.DataFrame(arr,columns=["looks"])
darr.boxplot("looks")
```

3.d. State the population of interest and the parameter of interest.

> Insert answer here
All Koala Females & number of looks at a large male


3.e. State the null and alternative hypotheses (verbal and symbolic).  You might want to use some of symbols from the beginning of lab

> Insert answer here.
H_0 = 0 looks at the larger male
H_a = more than 0 looks at the larger male


3.f. Execute your hypothesis test and then fill in the appropriate values below. 


> $\alpha = 0.05
> $s/\sqrt{n} = 0.864200634745681$  
> $t_{statistic} = 3.5706
> $p$-value $= 0.001087$  
> [Reject] $H_0$  

<Inserted code chunk to compute standard error (se) and t.test>


3.g. Interpret your p-value in the context of the question.

> Insert answer here
Since there is a 0.001087 probability of getting a result this extreme.


3.h. Calculate a 95% confidence interval for the mean mate preference, then write your interval below, using in-line code.

calculated by Abhi

> Insert answer here
(1.33, 4.84)


3.i. Interpret your confidence interval in the context of the problem. 

> Insert answer here 
The mean number of looks towards the larger male are between 1.33 and 4.84 looks.


3.j. Why would we want to calculate a confidence interval? (What does a hypothesis test tell us? What can a confidence interval tell us that a hypothesis test cannot?) Explain.

> Insert answer here
So we can have extra evidence to support that larger males are more favored.


3.k. Based on the confidence interval and your one-sample t-test result, do you think the mean mate preference from bellows is for larger males (greater than 0)? Explain.

> Insert answer here.
Yes, the entire confidence interval is greater than 0 indicating that it is likely that the average female prefers a larger male.




3.l. For each of the following, indicate if it is a correct or incorrect interpretation of the confidence interval you calculated. Provide an explanation for each.

1. 95% of the sample preferences will be between the upper and lower bounds of the confidence interval. 

> Correct or Incorrect?  
> Explain.
Incorrect, because 95% of the confidence intervals capture the sample mean.

2. There is a 95% chance that the true mean preference is between the upper and lower bounds of the confidence interval.

> Correct or Incorrect?  
> Explain.
Correct, because 95% of the confidence intervals capture the sample mean.

3. Suppose we repeat this experiment many times. 95% of the time, when we calculate a confidence interval, the true mean preference will actually be between the upper and lower bounds of the confidence interval. 5% of the time, it will not. 

> Correct or incorrect?  
> Explain. 
Correct, see explanation for 1 & 2


3.m. All else being equal, how would the following changes to the koala experiment influence a confidence interval? (Choose one answer, and **bold** it.)

1. Increased confidence level (1-$\alpha$): [Wider]  

2. Smaller sample size (n): [Wider] 

3. Larger standard deviation: [Wider]    



**Want to hear a koala [bellow](https://soundcloud.com/new-scientist/male-koala-bellow)?**























