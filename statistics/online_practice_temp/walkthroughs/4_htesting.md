# Walkthrough: Hypothesis testing
This section walks through the coding challenges given in the [_Hypothesis testing_](../4_htesting.md) section of the activity.

## Challenge 1: Null and Alternative
- [ ] Formulate a two-way Null and Alternate hypothesis for your test. Label those clearly for your audience.

Let's recall our research question:

>_Did changing homepage designs between A and B, significantly affect average browsing session time?_

To answer this question conclusively, we need to design a hypothesis test. And for that, we need to formulate Null and Alternate hypotheses:

**Null, H<sub>0</sub>**: There is no difference in average session time spent by users who saw design A and that of those who saw design B. If there is one, it's due to random chance, and is not _statistically significant_.

In other words, μ<sub>A</sub> = μ<sub>B</sub>.

Where μ<sub>A</sub> represents the mean session length for sample A, and μ<sub>B</sub> represents the mean session length for sample B.


**Alternative, H<sub>1</sub>**: There is a statistically significant difference between the time spent on our website by users who saw design A and by users who saw design B.

In other words, μ<sub>A</sub> ≠ μ<sub>B</sub>.

## Challenge 2: Methodology
- [ ] Write up a few sentences in a `markdown` cell in your Notebook to explain the methodology of your test, citing the significance level, your confidence level, p-values, what they mean and how you will use them here.


Formulating the hypothesis as we did here means in essence, we can make one of two conclusions:
1. We **reject the Null**. We say the observed difference is statistically significant, and _is due to_ changing the design variable (A or B).

2. We **fail to reject the Null**. We say the observed difference is not extreme enough to be considered statistically significant (by our standards). Therefore, we cannot reject the Null and we conclude that our observed difference between the two groups is simply due to chance.

We decide on what 'statistically significant' means by setting a threshold called the __significance level__. When we get our p-value later on, this is what we compare it to.

- If our p-value >= SL then we fail to reject the Null (or we accept the Null).
- If our p-value < SL then we reject the Null, and we say the result is statistically significant.

For this experiment, we will go with a significance level of **0.05**.

Our **confidence level** for this experiment relates inversely to our significance level. In fact, our _Cl = 1 - SL_. By virtue of setting our SL to 0.05, we're saying we assume a confidence level of 0.95, or **95%**.

Therefore, whatever conclusion we make in the end -- be it to accept or reject the H<sub>0</sub> -- we make it with 95% confidence that we're right.

## Challenge 3: Set-up
- [ ] Import the `stats` sub-module from the `scipy` library.

For the statistical functions in this section, we'll be using the `scipy` module -- and specifically, the `stas` sub-module within scipy.

After you've installed Scipy, import the `stats` sub-module as so:

```python
from scipy import stats
```

> _Make sure you've installed Scipy correctly using the right command -- usually a 'pip install --' but this might vary depending on any restrictions your organisation has put in place. Please speak to your mentor if installations are causing any headaches!_



## Challenge 4: Student's T-test assumptions
- [ ] Write up the two-sample t-test assumptions.
- [ ] Test assumptions 1 and 2, and write up your conclusions.
- [ ] Test the normality assumption (assumption 4) by:
  - [ ] Referring to the distributions visually first (from the EDA section).
  - [ ] Using the `stats.normaltest()` function and comparing to an SL of 0.05.
- [ ] Test the homogeneity of variances of the dependent variables (assumption 5) in both samples.

The assumptions of our two-sample t-test -- called the Student's T-test -- are:

1. The dependent variable is continuous.<br><br>

We can test this easily by looking at our `Session_length` variable and checking its type in Python, using the `.dtype` attribute.

```python
# If it's continous, this should give us a float
df['Session_length'].dtype
```

Once we've verified the output is a float -- i.e. a _dtype('float64')_ -- then we can tick this assumption and go to the next one.


2. The independent variable is categorical and has two categories (two samples).<br><br>

This again can be confirmed easily by investigating the number of values/categories our `Group` variable takes. We can do this with the `.unique()` function.

```python
# Unique values in the Group column
df['Group'].unique()
```

Once we've confirmed that we only have two values, 'A' and 'B', we can tick this assumption and move to the next one.

3. Observations in one sample are independent of those in the other sample.<br><br>

Although in real life we may want to do some more investigating, for now we can assume that our users were not interacting with each other, and/or influencing each other's opinions. Let's tick this one and move on to the next assumption!

4. The dependent variable is normally distributed.<br><br>

We can do this in two ways. The first is to eyeball the distribution plots from the [EDA stage](3_eda.md). From those plots, both samples 'look' normally distributed -- i.e. they have one peak each, about which the data seem symmetrical.

However, looks can be deceiving. To be more confident, we can test this assumption using another statistical test. This is the second method. This statistical test, evaluates how different a dataset is from the normal distribution. Its Null hypothesis states that the variable in question is normally distributed, and the Alternate says that the difference between the data and the normally distribution is statistically significant.

Assuming an SL of 0.05, we can run this test in Python using the handy `normaltest()` function from Scipy, to get a p-value.

```python
# For sample A
stats.normaltest(A['Session_length'])
```

We get a p-value of **0.326**. Since this is bigger than our SL of 0.05, we say that we don't have enough evidence to reject the Null, and thus, we accept it. We conclude with 95% confidence that there is no statistically significant difference between `Session_length` for sample A and a normal distribution, and we say it is normally distributed.

Now let's see if B is also normally distributed.

```python
# For sample B
stats.normaltest(B['Session_length'])
```

We have ourselves an even higher p-value this time of **0.51**, which means again, since 0.51 > 0.05, we fail to reject the Null, and conclude that the session times for sample B are also normally distributed.

Now that we know both our samples are normally distributed, we can move on to testing the last assumption - homogeneity of variances.


5. The samples have identical variances.<br><br>

We can test this easily by running the `.var()` function on both samples.

```python
# Variance for sample A
A['Session_length'].var()
```

This returns a variance of 647.20. Let's check that of sample B:

```python
# Variance for sample B
B['Session_length'].var()
```

This returns a variance of 604.75.

Since the variances are not identical, we fail this assumption. When running our test, we should make sure it takes this into account.


## Challenge 5: Running the t-test
- [ ] Run the two-sample t-test using the `stats.ttest_ind()` function.

The `ttest_ind()` function takes a few essential parameters:

- `a` - this is our dependent variable from our first sample.
- `b` - this is our dependent variable from our second sample.
- `equal_var` - we specify if our variances are equal or not. Take either a _True_ or a _False_. Default is True.

We will be setting the last parameter to False, as our variances are not equal.

In statistics this variation of a two-sample t-test, when the variances are unequal, is called _Welch's t-test_. If we were doing this by hand, this might be quite a radical change as we would have had to use various other equations to get the right p-value. Fortunately however, we're doing this in Python, where all we're really concerned with is changing a parameter from the default _True_ to _False_.

> If you're interested in the mathematical nuances of the different variations of two-sample t-tests -- e.g. equal, similar, or unequal variances -- refer to the theory section of the online practice, or check out this excellent [Wikipedia article](https://en.wikipedia.org/wiki/Student%27s_t-test#Equal_sample_sizes_and_variance) on the topic.

Let's run the test!

```python
# Running the two-sample t-test, ensuring the equal_var = False
stats.ttest_ind(a = A['Session_length'],
               b = B['Session_length'],
               equal_var= False)
```

The test returns two values: a _t-statistic_ and a _p-value_. If we were doing this by hand we would have used the former to calculate the latter. Thankfully, we're using Python, and this function gives us the p-value straight away.

It returns a p-value of **0.000429**.


## Challenge 6: Making a conclusion
- [ ] Make your conclusion, citing your confidence level, and write up your recommendation to the business.

Based on our test, our p-value is **0.000429**. Recall that our pre-determined SL was **0.05**.

Since our p-value is smaller than our SL, we can now with 95% confidence **reject the Null hypothesis** that there is no difference between the average time spent on the two homepage designs.

Therefore, the difference we observed, of just **2.12 seconds** between page A and page B, is actually _statistically significant_. Varying our designs actually had a meaningful impact on the amount of time our users spent on the site!

> Going with just an observed difference of 2.12 seconds without any statistical testing, we might have crudely said that that was due to random chance. By formulating and running a proper statistical test however, we now say the opposite -- that the difference of 2 seconds is meaningful based on the data -- and we can quantify how confident we are in this decision (95%). This is why we do hypothesis tests!

Based on this, we can with 95% confidence say that homepage design did have a statistically significant impact on average user browsing time. Of the two designs, design A (see below) brought in longer browsing sessions in Q1, and we recommend that Sense Robotics Ltd deploy it across its entire userbase.

![](../images/A.JPG)<br>
**Design A**: The winning design.


In future, we can try:
- Experimenting with new designs. This time, we could run one-way t-tests, where we would only change the design if we have a significant difference in one direction: B > A.
- If non-urgent, we can keep the test running for 6 months, changing the duration. It could be that over a period that long, we ending up accept the Null.
- We could run regional experiments - could it be possible that different parts of the worlds react differently to different designs?
- We could experiment with various other website features, not just homepage design, to answer questions aimed at optimising ad revenue, or getting users to complete their purchases for example.



  <br />

  ___
  [Previous](3_eda.md) |  [Next](5_power.md)
