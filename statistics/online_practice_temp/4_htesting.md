# Hypothesis testing
Now that we've cleaned, transformed and explored our data, it's time to answer our research question. We do this by setting up and running a hypothesis test.

> To refresh your knowledge on hypothesis testing and solidify it, we suggest you complete this section in tandem with [Part 2](./theory/theory2.md) of the theory activity.

## Formulating the hypotheses  
The type of hypothesis test we will be focusing on tests the difference between two sample means; therefore, when formulating our Null and Alternative hypotheses, we have to weave this in.

> _There are many types of statistical tests. Some test the significance of correlations between numerical variables, some test whether two distributions are identical or significantly different, and some whether the difference between two sample medians is significant. In other words, this is a whole space! In this module, we will be focusing solely on statistical tests that test the difference between two sample means._

Let's first remind ourselves of our research question - maybe you phrased it something like this:

**_Was there a difference in browsing time between users who were shown homepage design A and those that were shown B?_** <br>


The answer to this question is essentially a 'Yes' or a 'No'. But even if it is a 'Yes', how do we know this difference isn't by chance? This is where hypothesis tests help.

We begin with formulating our Null and Alternate hypotheses, which together should represent all possible outcomes of the experiment:

1. **Null Hypothesis, H<sub>0</sub>**:<br>
This hypothesis states that any difference we observe is due to chance, or is _within the realm of chance_. We come into the experiment assuming that the Null is true.


2. **Alternate Hypothesis, H<sub>1</sub>**<br>
Alternatively we say, the difference we observe is so extreme, it cannot be due to chance, or is _outside the realm of chance_. In other words, we say the difference is statistically significant.


> *We always assume the Null is true, until proven otherwise. This is analogous to assuming innocence until proven guilty, in a courtroom.*

There are two possible outcomes from this test. Either we accept the Null or we accept the Alternative; there is no in-between. Because we start with the assumption of the Null being true, these two outcomes are technically phrased as follows:

1. We reject the Null -- i.e. we 'accept the Alternative', or
2. We fail to reject the Null -- i.e. we don't have enough evidence to reject the initial assumption that the difference is due to random chance.

### One-way vs. Two-way tests
Does it matter which direction the difference goes in, or not? Deciding what matters to you as the experiment designer, will affect whether you end up running a one-way or a two-way test.

If you don't care about which direction the difference goes in -- i.e. Session times for A > Session times for B *or* Session times for B> session times for A -- but you just care *if* there is a difference at all, then you will want a two-way test. This is also called a bi-directional test.

On the other hand, if you're using one design currently (say, A), and you want to see if switching to B is worth it or not, then you only care about testing one direction the difference can go in: session times for B > session times for A. In that case, you would want a one-way, or uni-directional test.

> _Which type of test you choose, will affect the function you will be running in Python, and therefore the p-value you will obtain, and make a decision on the basis of._

## P-values
Recall, we can only really have two outcomes: the difference is due to chance, or it is statistically significant. But how do we know how likely or unlikely our observed difference is?

The p-value answers the following question: *assuming the Null is true -- i.e. what we assume initially -- what is the probability that we get the difference that we ended up getting, or anything more extreme than it?*

In other words, a low p-value means there's a very small chance we would get the difference that we got, if the Null were actually true -- which means, it's quite likely the difference we observed is not due to chance at all!

But how do we know if our p-value is low enough? Is 10% low enough, or do we need it to be 5% or say 0.001%? This is where the significance level comes in.

> The right Python function will give you the p-value in one line. But if you're interested in the maths behind it, and/or you want to delve deeper into the theory, check out the right section in [Part 2](./theory/theory2.md) of the theory activity.

## Statistical Significance
The significance level is simply a probability threshold. Below this threshold, our p-value is deemed 'low enough' and the difference we observed is deemed extreme enough to be called 'statistically significant'. Conversely, if our p-value is above this threshold, then the probability of getting our result, or anything larger or more extreme than it, is not deemed low enough, and we conclude that we don't have enough evidence to reject the Null.

In other words,

- If our **P-value < SL ==> *we reject the Null***
- If our **P-value >= SL ==> *we fail to reject the Null***

> **Important Note**:<br>
You should decide on your SL _before_ you run the experiment. In other words, you should set the goal post before you do anything.

For today, we will assume a SL of **0.05** or 5%.

### Confidence level
Closely related to the SL, is the concept of a confidence level (CL). This value answers the question: *how confident (%) are we in our conclusion?*.

It's related to the SL in that they both add up to 1. I.e. *1 - SL = CL*. For instance, let's say we decide on an SL of 10% (0.1). Then, whatever conclusion we end up with -- to reject or not to reject the Null -- we are making that conclusion with 90% confidence.

Therefore, the lower you set your SL, the more evidence you are requiring from the sample in order to reject the Null, and thus, the more confident you are going to be in your conclusion. It's useful to give your CL as part of your final conclusion to give your audience a sense of how robust your test is.

## Implementation
We will be running a two-sample test, that evaluates the difference between the means of those two samples. The primary test for this situation is called the *two-sample t-test*.

This test comes with a few assumptions:

1. The dependent variable is continuous.
2. The independent variable is categorical and has two categories (two samples).
3. Observations in one sample are independent of those in the other sample.
4. The dependent variable is normally distributed.
5. The samples have identical variances.

Let's see which assumptions we meet:
1. Check. Our dependent variable here is `Session_length`, which is continuous.
2. Check. Our independent variable here is `Group` and has two categories, A and B.
3. We can assume this is the case in our experiment -- i.e. we're assuming no one from our B sample has influenced the opinions of those in the A sampe, and vice versa.
4. We need to check if this is the case.
5. We need to check if this is the case.


> _There are of course many other tests out there, which evaluate for different scenarios. Within the realm of testing for a difference between two means, there is also more than one variation of the t-test, with nuanced differences. Statisticians would of course need to explore those nuances and be able to derive them, but for the Apprenticeship, we won't need to do anything like that. In fact, the only test we need to focus on is the two-sample t-test, explained above. Having said that, [Part 2](theory/theory2.md) of the theory activity delves into more detail and goes further with a few extra tests if you're curious!_

### Libraries
There are a few libraries in Python that have statistical techniques -- `scipy` and `statsmodels` are the prominent ones. For this section, we'll be using the `scipy` package.

After you've installed Scipy, import the `stats` sub-module as so:

```python
from scipy import stats
```

> _Make sure you've installed Scipy correctly using the right command -- usually a 'pip install --' but this might vary depending on any restrictions your organisation has put in place. Please speak to your mentor if installations are causing any headaches!_

### Testing for normality
Referring to assumption 4 above, we need to check if the `Session_length` variable is normally distributed or not. We can do this in two main ways.

The first involves simply visualising the distribution: does it 'look normal'? I.e. does it have one peak, and does it seem symmetrical on both sides? This is a good first check and will quickly let us know if we're on the right track, but we may want to be more confident about this assumption.

To be more confident, we can test this assumption using another statistical test. This is the second method. This statistical test, evaluates how different a dataset is from the normal distribution. Its Null hypothesis states that the variable in question is normally distributed, and the Alternate says that the difference between the data and the normally distribution is statistically significant.

Assuming an SL of 0.05, we can run this test in Python using the handy `normaltest()` function from Scipy, to get a p-value. As before, if the p-value is smaller than our SL, then we reject the Null; if the p-value is greater or equal to the SL, then we fail to reject the Null assumption, and we say the data is normally distributed.

You can run this function as follows:
```python
stats.normaltest(subset_A['Session_length'])

# and running the same check for subset B.
```

Run this test for both subsets, A and B, and make a conclusion on whether the `Session_length` variable is normally distributed in both or not. We need to make sure they're both normally distributed in order to run this test.



### Testing for homogeneity of variances
We also have to test assumption 5, which states that the variances in both samples are identical.

Test this by finding the variances in both samples for the `Session_length` variable.


### Running the test
Within the `stats` sub-library, we'll use the `ttest_ind()` function to run our two-sample t-test. This function takes three main parameters:

1. `a` -- this is our dependent variable from our first sample, A.
2. `b` -- this is our dependent variable from our second sample, B.
3. `equal_var` -- here, we specify whether the two variances are equal or not. Default is *`True`*

```python
stats.ttest_ind(a = , b = , equal_var = )
```


## Making a decision
Once you've tested the assumptions, run the test and get your p-value. Compare this to your predetermined SL, and make your decision!

Write your conclusion up in a `markdown` cell in your Jupyter Notebook, referring back to the research question and the business objectives. Do we use design A or B, or does it matter at all? Specify your level of confidence when making your final recommendation to the leadership at Sense Robotics Ltd.



## Challenges
- [ ] Formulate a two-way Null and Alternate hypothesis for your test. Label those clearly for your audience.
- [ ] Write up a few sentences in a `markdown` cell in your Notebook to explain the methodology of your test, citing the significance level, your confidence level, p-values, what they mean and how you will use them here.
- [ ] Import the `stats` sub-module from the `scipy` library.
- [ ] Write up the two-sample t-test assumptions.
- [ ] Test assumptions 1 and 2, and write up your conclusions.
- [ ] Test the normality assumption (assumption 4) by:
  - [ ] Referring to the distributions visually first (from the EDA section).
  - [ ] Using the `stats.normaltest()` function and comparing to an SL of 0.05.
- [ ] Test the homogeneity of variances of the dependent variables (assumption 5) in both samples.
- [ ] Run the two-sample t-test using the `stats.ttest_ind()` function.
- [ ] Make your conclusion, citing your confidence level, and write up your recommendation to the business.

***
> If you get stuck doing any of the above challenges, then don't you worry! It's part of the learning process. <br><br>
Depending on the nature of the problem, we recommend using the following resources to aid you:<br>
>  1. Your notes from the workshop, where appropriate.
>  2. Google. Especially for debugging.
>  3. Your mentor. Especially for help on the more challenging concepts (e.g. p-values!) and debugging library installation issues.
>  4. The appropriate stage in the [walkthroughs](./walkthroughs/4_htesting.md).
>  5. The completed notebook. Don't jump straight to this one; it should be your final resort!<br><br>

***



  <br />

  ___
  [Previous](3_eda.md) |  [Next](5_power.md)
