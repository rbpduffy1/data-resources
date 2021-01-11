# *Optional*: Sample size, effect size and statistical power
In our case, our sample size was somewhat governed by how much time the client wanted us to run the test for. However, this isn't always the case. Sometimes, the case is flipped, and you may be asked to determine the minimum necessary sample size for the conclusion to have a specific robustness against a desired output. How do you know if a sample is big enough?

We can use the interesting dynamic between sample size, effect size, and statistical power to answer questions like this.

> **Note 1**:<br>
These are new concepts and were not discussed in the workshop or the introductory reading activity. Please refer to [Part 3](./theory/theory3.md) of the theory activity to get a good grasp of these three concepts relate to each other, before you continue with the coding below. <br><br>
**Note 2**:<br>
This section is _above and beyond_ the Apprenticeship standard, so it's completely optional! It is mentioned here because it answers various practical questions and can be helpful to know about.

## The dynamic
First, let's define those terms.

- <u>**Sample size**</u>: is the number of rows in our sample. <br><br>
- <u>**Effect Size**</u>: is our actual difference between the two sample means. Usually, this is standardised in some way by dividing by a standard deviation. Which standard deviation we should divide and why, is more of a statistics theory question, but prominent research in the space include dividing by the standard deviation of the second sample (see [Glass' Δ](https://en.wikipedia.org/wiki/Effect_size#Glass'_%CE%94)) or by some 'pooled' standard deviation (see [Cohen's *d* measure](https://en.wikipedia.org/wiki/Effect_size#Cohen's_d)) <br><br>
- <u>**Power**</u>: This is the probability of detecting an effect size in our data. 'Detecting' here simply means to correctly reject the Null -- i.e. to correctly say that there is a statistical difference between the two sample means. Power is also equal to *1 - Type II error*.

> The Type II error is the probability of falsely accepting the Null, when we should really reject it. <br><br>
On the other hand, a Type I error, is the probability of falsely rejecting the Null, when really we shouldn't.<br><br>
For more clarity on the distinction between those two errors, check out [Part 3](./theory/theory3.md) of the theory activity.

Those three concepts are also related mathematically -- in other words, given two, we can calculate the third. For instance, given a desired effect size and power, we can calculate the minimum sample size we need in our experiment. Or, for instance, given the sample size that we have and our desired effect size, what would be our power? And from that, what is our estimate for our Type II error?

## Implementation
Power analysis can be complex. Fortunately however, we have tools in Python that do those calculations for us in the background. For this section, we will be using a library called `statsmodels` for its simplicity in doing power analysis calculations. From this library we'll be using the handy `TTestIndPower` object, from which we'll be using the `solve_power()` function to make our estimates.

To import this library run the following:
```python
from statsmodels.stats.power import TTestIndPower
```

> *As before, if you any experience installing this library, please let your mentor know and they will be able to help.*

### Scenario 1. Calculate the power for our results
To do this, we need we will first set the object `TTestIndPower` to a variable, and then call the `solve_power()` function. The function needs two of the three components -- power, effect size and sample size -- to calculate the third. The third variable that we want to calculate will be given a value of _`None`_.

Here are the parameters of this function:
1. `effect_size`: This is our mean difference standardised by dividing by some standard deviation. Default is _`None`_. <br><br>
2. `nobs1`: This is the number of observations in sample 1. We don't need to specify the size of the second sample due to the 'ratio' parameter below. Default is _`None`_. <br><br>
3. `alpha`: This is our significance level. <br><br>
4. `power`: The probability of correctly rejecting the Null, hence, 'detecting' a statistically significant effect size. Default is _`None`_. <br><br>
5. `ratio`: The ratio of the size of sample 2 to that of sample 1. In other words, *ratio = Nobs 2/Nobs 1*. Default is _`1`_, i.e. it assumes we have equal sample sizes. <br><br>
6. `alternative`: Specifies whether our alternate hypothesis is one-tailed or two-tailed. Default is _`two-sided`_. <br><br>

Since we want to calculate power, give the function the sample size, and the effect size you observed, specifying the `alpha` to our SL of 0.05, and setting the `power` parameter to _`None`_.

***
**A note on standardising effect size**:<br>
For simplicity we may want to simply divide the observed difference by the total standard deviation of the dataset, or perhaps by the average standard deviation of both samples. Whilst the difference may not be massive, it's best in these cases to refer to the research. We can assume that measures such as Cohen's _d_ and Glass' Δ were derived, and are justified reasonably (if we don't want to read the original research [1](https://books.google.co.uk/books?id=2v9zDAsLvA0C&pg=PP1&redir_esc=y#v=onepage&q&f=false), [2](https://digitalcommons.wayne.edu/jmasm/vol8/iss2/26/))

Whichever measure we decide on using, we should make sure we mention it in our experiment. For today, we'll be using Cohen's *d* measure, as it's quite popular and there has been quite a bit of work on it. It seems accepted for instance that an effect size, d, of 0.01 or smaller is considered 'very small' whereas if d is 2 or greater, then the effect size is considered 'huge'.

|*d*|Considered|
| --- | --- |
|0.01| Very small |
|0.2| Small |
|0.5|Medium|
|0.8|Large|
|2.0|Huge|
**Table 1** -- *Various measures of Cohen's 'd' value.*

To calculate Cohen's *d* from our observed difference, we divide it by the pooled standard deviation as expressed in the following equation:


![Cohen d](images/cohen.JPG)<br>
**Equation 1** -- *Calculating Cohen's 'd' measure*.

Where,
- `μ`<sub>1</sub> is the mean of our first sample;
- `μ`<sub>2</sub> is the mean of our second sample;
- `S`<sub>p</sub> is the pooled standard deviation.

According to the original research, 'pooled standard deviation' is calculated using the following equation:

![Cohen d- spooled](images/cohen_pooled.JPG)<br>
**Equation 2** -- *Calculating pooled standard deviation according Cohen's work*.

Where,
- n<sub>1</sub> is the size of sample 1.
- n<sub>2</sub> is the size of sample 2.
- s<sub>1</sub> is the standard deviation of sample 1.
- s<sub>2</sub> is the standard deviation of sample 2.


Now that we have the equations, we can convert our observed difference to a Cohen's 'd' value.

> **Note**:<br>
You can use `np.sqrt()` function from the `numpy` package to do a square root. <br>
For squaring, you can use the asterisk syntax. I.e. x<sup>2</sup> can be denoted in Python by `x**2`.

***

Once you have your effect size, you can now plug in the appropriate values -- `effect size`, `nobs1`, `ratio`, `alpha` and `alternative` -- in the `solve_power()` function to get your power value. Make sure you specify the `power` parameter as _`None`_.

Once you've calculated the power, you can now easily calculate the Type II error of your experiment.


### Scenario 2. Given a desired effect size, and power, what should our sample size be?
We can use the same equation to flip the problem. If we were to start over, with limited resources, or with a need to minimise the time needed to run the experiment, we would need to think about the minimum sample size we'd need for the experiment to succeed.

1. **Effect Size**: We can use Cohen's d measure as our standard. Say, we were only interested in at least a 'large' effect between the two homepage designs, A and B. From Table 1, that means we would be eyeing a 'd' value of at least 0.8.
<br><br>
2. **Power**: This can be arbitrary, but it will depend on how tolerant we are of making Type II errors. How costly is it to assume that the difference is random, when it is actually statistically significant? There's potentially an opportunity cost of not moving from one design to the other, but it may not be too impactful. In light of this, we may say we're tolerant of no more than a 5% Type II error -- hence, a power of 95%.
<br><br>
3. **Ratio**: For now, let's assume equal sizes for both samples, which gives us a ratio of 1.
<br><br>

Assuming an SL of 0.05, we can input the values into our function, whilst setting the `nobs1` parameter to _`None`_, to get our minimum sample size.

## Exploring the dynamic
Try experimenting with those parameters to get a better grasp of the dynamic.

For example:
- Try changing effect size, whilst keeping everything else constant.
- Try changing the significance level, whilst keeping everything else constant.
- Try changing the power requirement, whilst keeping everything else constant.

And this is just for when we're trying to estimate sample size (Scenario 2). You can try different combinations for Scenario 1 as well! Note down the effects you observe.

### Further: Visualising the dynamic
In addition to manual inputs, you can also see the dynamic between the parameters visually using the handy `plot_power()` function.

Similarly to `solve_power()` this function comes from the `TTestIndPower` object from statsmodels. It takes the following parameters:

- `dep_var` -- this is the parameter you're choosing to vary. On the plot, it will be on your X-axis. This can either be your sample size, _`nobs`_ or effect size, _`es`_.
- `nobs` -- The sample size values that will be experimented with.
- `effect_size` -- The effect size values that will be experimented with.

Your X-axis will take whatever parameter you specify in the `dep_var`, and your Y-axis will be your power.

For example, using the following code to plot the power output when varying the sample size between 2 and 200, for 5 different effect size values.

```python
tp.plot_power(dep_var= 'nobs',
              nobs = np.arange(2,200),
              effect_size = np.array([0.01,0.2, 0.5, 0.8, 2.0]))
```

Experiment with the parameters and make a note of any interesting observations!


## Challenges
- [ ] Explain the terms sample size, effect size, and statistical power in your own words, in your notebook.
- [ ] Import the `TTestIndPower` object and assign it to a variable, called `tp`.
- [ ] Use the `solve_power()` function from `tp` to calculate the power from your experiment.
  - [ ] Calculate Cohen's *d* measure from your observed difference.
  - [ ] Fill in the parameters appropriately, making sure you set the right one to `None`.
  - [ ] Calculate the Type II error.
- [ ] Use the `solve_power()` function to get the minimum sample size required to detect a 'large' effect size with a Type II error of 5%.
- [ ] Experiment with this function, noting down what happens when you change:
  - [ ] The effect size,
  - [ ] The SL, and
  - [ ] The power requirement, when keeping everything else constant.
- [ ] *Optional*: Visualise the dynamic using the `plot_power()` function.


***
> If you get stuck doing any of the above challenges, then don't you worry! It's part of the learning process. <br><br>
Depending on the nature of the problem, we recommend using the following resources to aid you:<br>
>  1. Your notes from the workshop, where appropriate.
>  2. Google. Especially for debugging.
>  3. Your mentor. Especially for help on the more challenging concepts (e.g. p-values!) and debugging library installation issues.
>  4. The appropriate stage in the [walkthroughs](./walkthroughs/5_power.md).
>  5. The completed notebook. Don't jump straight to this one; it should be your final resort!<br><br>

***



  <br />

  ___
  [Previous](4_htesting.md) |  [Back to outline](0_brief.md) |
