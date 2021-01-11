# Exploratory Data Analysis (EDA)
A big part of any project is the exploration phase. This is where you deep dive into the variables of interest - or indeed all the variables - to extract and visualise useful patterns.

> In our case, we started with a clear problem statement and a research question that addresses it, based on what we were told by Sense Robotics, but in many situations we might not have a clear and concise goal. In those cases, exploration plays an even more significant role. It would serve as a guide for the directions we decide to take our project in, and perhaps the hypotheses we might wish to test.

For now, we will be focusing on the two variables of interest, `Group` and `Session_length`. Since the latter is numerical, we can rely on descriptive statistics concepts to help us.

We can begin of course, by running the `.describe()` function from `pandas` on the entire dataframe to remind ourselves of the various key parameters of the `Session_length` column. We can also create subsets for all rows with group `A` and all those with group `B`, and run the function again to read any differences between the two samples.

| Parameter | Meaning |
| --- | --- |
| `count`| Number of rows in this variable (excluding NA rows) |
| `mean` | Mean of the variable |
| `std` | Standard deviation of the variable |
| `min` | Minimum value in the variable |
| `25` | Value at which we cover 25% of the data; the 25th percentile |
| `50` | Value at which we cover 50% of the data; the 50th percentile, or the median|
| `75` | Value at which we cover 75% of the data; the 75th percentile |
| `max` | Maximum value in the variable |
**Table 1** -- Output of the _describe()_ function.


Whilst the `.describe()` function is great, it does not give us everything -- and we may not be interested in all its outputs either. We can instead choose to output specific measures using the appropriate functions.

### Measures of centrality
Whilst this already given in the output above, if we only cared about the mean of a variable we can simply run the `.mean()` function on the column in question. Similarly, if we only cared about the median, we could use the `.median()` function on the column we want.

At this stage, it's useful to remember our objective: to find if there was at all a difference between the two designs in terms of their effect on browsing time. In other words, we are looking at the average difference in `Session_length` for the two samples -- was there one? We can investigate this by subtracting the mean session time for subset A, from the mean of subset B (or vice versa).

> Make a note of this value, as we will come back to it when we're running our test.


### Measures of spread
The `.describe()` function gives us the standard deviation and various percentiles, but we may want to know more.

For instance, if we wanted to find the variance of a variable, we could use the `.var()` function. Likewise, if we wanted any one of the parameters specifically, we can use the appropriate function -- e.g `.std()` for standard deviation, `.min()` for minimum, and `.max()` for maximum. If we wanted, we could also choose to find the _range_ of the sessions by subtracting the minimum value from the maximum value.

The output above gives us three percentiles -- 25, 50, and 75 -- but we may want to get a more granular description of the distribution of session times. One approach would be to call the specific percentiles of interest, which we can do using the `percentile()` function from the `numpy` package. We could run the following for instance to get the 60th percentile:

```python
np.percentile(a = df['Session_length'], q = 60)
```

It could be useful to run various percentile values for each of your subsets to get a better feel of how similar or different their distributions are.

> <u>Note:</u> The 25th percentile is also called the first _quartile_. Likewise, the 50th percentile (the median) is also referred to as the second quartile, and the 75th percentile as the third quartile.


### Visualisation
Manually outputting various percentile values might get tedious, and may still not give us a very clear picture. What if we could get all this from a graph? There are two main ways to get a visual understanding of a distribution: histograms and boxplots (or box-and-whisker plots).

There are many ways to build those plots in Python -- including some functionality within `pandas`! However, for today, we'll be trying out another library, purpose-built for data visualisation, called `seaborn`, because it's user-friendly and its aesthetically pleasing graphs.

> *Today, we'll only be getting a flavour of Seaborn functionality, but we won't be delving into it (nor is it a requirement for this module), so please don't feel overwhelmed by this! There's a whole module on visualisation, in which you will have plenty of time to explore the nuances of this package and some others.*

To import seaborn, run the following line of code, back under the Libraries heading:

```python
import seaborn as sns
```

Seaborn is great for many high-level functions, but for more nuanced manipulations like adding a legend, changing titles, and rotating axis labels, we'll use an older and more flexible library called `matplotlib`. Run the following code to import the _pyplot_ sub-module from matplotlib:

```python
import matplotlib.pyplot as plt
```

Finally, in the Libraries heading as well, run the following line:

```python
%matplotlib inline
```
> This last line might seem a little strange, or magical. In fact, it's actually called a 'magic function'. Its purpose is to allow Seaborn to display its plots in a Jupyter Notebook environment -- by default, they don't and we would have had to add extra lines of code to display them. To make our lives easier, we run this magic function.



**1. Histograms**:<br>
A histogram is a great way to tell us the shape of a distribution. The data is divided into bins, or bars, of equal size, and their heights represent how frequently that range of values (represented by the width of the bin) occurs in our data.

In seaborn, we use the `.distplot()` function, passing only one parameter: the variable itself. The following should produce a histogram -- or a distribution plot in seaborn lingo:

```python
sns.distplot(a = df['Session_length'])
```

What do you notice about the shape of the distribution? We can take this further, by plotting the distributions of `Session_length` for each sample on the same graph, to visualise how similar or different they are. This can easily be done by running the same line of code above for the two samples, both in the same Jupyter Notebook cell. Once you've run this, you can also add a legend for clarity using the following from `matplotlib`:

```python
plt.legend('Group A', 'Group B')
```
> _Make sure the order of the legend categories is correct. In the above example, we ran the .distplot() function for sample A first, then that for sample B -- in which case, 'Group A' should be listed first in the legend labels._

What do you see? When thinking of our research question, what does this plot suggest?


**2. Boxplots**:<br>
Another great way to visualise a distribution, is through using boxplots, or box-and-whisker plots.


![Boxplot](./images/bxplot.JPG)<br>
**Fig. 1** -- *An example boxplot*

A boxplot gives a few things about the distribution beyond the simply what it looks like.

1. It gives us the **_median_**. This is represented by the line in the middle of the box.<br><br>
2. It gives us the **_25th percentile_**. This represented by the left edge of the box.<br><br>
3. It gives us the **_75th percentile_**. This represented by the right edge of the box.<br><br>
4. It gives the **_Interquartile range (IQR)_**. This is the difference between the 75th and 25th percentiles -- i.e. the width of the box.<br><br>
5. It gives us the **_whiskers_**, which are calculated by adding/subtracting the IQR from either edge of the box, usually scaled to a factor of 1.5. I.e.
    - Right whisker = 75th percentile + 1.5*IQR
    - Left whisker = 25th percentile - 1.5*IQR
<br><br>
6. It gives us the **_outliers_**. These are defined arbitrarily as any data points beyond the whiskers.

> Note that scaling to a factor of 1.5 is the just 'typically' what we do, but this can be changed depending on how tolerant you want to be of extreme values. I.e. if those values shouldn't be considered 'extreme' then you can increase the scaling factor to say, 2, or more. It would depend on context and your judgement as the analyst.

To produce a boxplot in seaborn, we use the nice `.boxplot()` function, passing in the variable, `Session_length` to the `x` parameter:

```python
sns.boxplot(x = df['Session_length'])
```

We can compare the boxplots for each sample, simply by assigning the `y` parameter to our `Group` variable.

> **A few notes things to try:**<br>
1. Check out the `whis` parameter in the function. <br>
2. Try swapping the `x` and `y` parameters around!


## [*OPTIONAL*] Further exploration  
So far, we only really explored the two main variables, `Group` and `Session_length`. But the data we collected allows for more interesting exploration, if we want to keep going! To name a few:

- We can look at distributions of `Session_length` by `Gender` -- did the user's gender affect how long they browsed our site for on average?
- We can explore distributions by `Continent` -- did location matter?
- We can extract month information from the `Date` column and/or weekday/weekend information for example to explore distributions. Use the [documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Timestamp.html) to see the various other attributes a Pandas _datetime_ object can take. *Note: you have to convert the `Date` column from a string to a datetime object first.*
- We can combine any of the above! Hint: try passing another variable to the `hue` parameter in seaborn.


## Challenges
- [ ] Print the summary statistics for:
  - [ ] The entire dataframe, and
  - [ ] The two samples separately.
- [ ] Print the following measures of centrality for each of the samples session lengths:
  - [ ] The mean,
  - [ ] The median,
  - [ ] The difference between the two sample means. *Note this down for later*.
- [ ] Print the following measures of spread for each of the sample session lengths:
  - [ ] The standard deviation,
  - [ ] The variance,
  - [ ] The range,
  - [ ] The 25th, and 75th percentiles,
  - [ ] The interquartile range.
- [ ] Visualise the shape of the distribution of the `Session_length` variable by:
  - [ ] Building a histogram for the entire dataframe,
  - [ ] Building two histograms, one for each sample, on the same plot.
- [ ] Visualise the distribution of the `Session_length` variable, with boxplots:
  - [ ] First, for the entire dataframe, then
  - [ ] For each of the samples.

#### Optional
- [ ] Explore the distributions of the `Session_length` with respect to the two genders.
- [ ] Explore the distributions of the `Session_length` with respect to the continent data.
- [ ] Extract the month from the `Date` column and explore the distributions of the `Session_length` with respect to month.
- [ ] Extract the weekday from the `Date` column and explore the distributions of the `Session_length` with respect to each day of the week.



***
> If you get stuck doing any of the above challenges, then don't you worry! It's part of the learning process. <br><br>
Depending on the nature of the problem, we recommend using the following resources to aid you:<br>
>  1. Your notes from the workshop, where appropriate.
>  2. Google. Especially for debugging.
>  3. Your mentor. Especially for help on the more challenging concepts (e.g. p-values!) and debugging library installation issues.
>  4. The appropriate stage in the [walkthroughs](./walkthroughs/3_eda.md).
>  5. The completed notebook. Don't jump straight to this one; it should be your final resort!<br><br>

***


  <br />

  ___
  [Previous](2_cleaning.md) |  [Next](4_htesting.md)
