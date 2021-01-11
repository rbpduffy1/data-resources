# Walkthrough: EDA
This section walks through the coding challenges given in the [_Exploratory Data Analysis (EDA)_](../3_eda.md) section of the activity.


## Challenge 1: Summary stats
- [ ] Print the summary statistics for:
  - [ ] The entire dataframe, and
  - [ ] The two samples separately.

We can do this as before with the `.describe()` function:

```python
# Summary stats
df.describe()
```

In the [first section](0_brief.md) section, we had already created two subsets, one for each design/group. Since then however, we did quite a bit of data cleaning and transformation, that the original variables `A` and `B` won't be up to date with.

Let's go ahead and re-create them:

```python
# Create subsets A and B
A = df[df['Group'] == 'A']

B = df[df['Group'] == 'B']
```

We can print the summary stats for A and B, as before:

```python
# Summary stats for A
A['Session_length'].describe()
```

And for B:

```python
# Summary stats for B
B['Session_length'].describe()
```



## Challenge 2: Measures of centrality
- [ ] Print the following measures of centrality for each of the samples session lengths:
  - [ ] The mean,
  - [ ] The median,
  - [ ] The difference between the two sample means. *Note this down for later*.

We can use the appropriate `pandas` functions to complete this challenge. To get the mean and median, we can the `.mean()` and the `.median()` functions respectively:

```python
# We can use the .mean() function to get the mean for Group A
A['Session_length'].mean()
```

And then the same for B:

```python
# The same function to get the mean for Group B
B['Session_length'].mean()
```

For the median:

```python
# We can use the .median() function to get the mean for Group A
A['Session_length'].median()
```

And then again for B:

```python
# The same function to get the mean for Group B
B['Session_length'].mean()
```

Finally, for the last challenge, we simply subtract one mean output from the other. The order doesn't matter, we only care about the magnitude of that difference.

```python
# Subtract the mean session of length of B from A (or vice versa)
A['Session_length'].mean() - B['Session_length'].mean()
```

We observe a difference of **1.592 seconds** between the average time users in group A spent on our site and the average time users spent on group B. Is this significant? Or is it simply due to random chance? This is what we will put to the test in the next section.


## Challenge 3: Measures of spread
- [ ] Print the following measures of spread for each of the sample session lengths:
  - [ ] The standard deviation,
  - [ ] The variance,
  - [ ] The range,
  - [ ] The 25th, and 75th percentiles,
  - [ ] The interquartile range.


As with the previous challenge, fortunately for us, the majority of these are already in-built functions.

We can use the `.std()` and the `.var()` from `pandas` to get the standard deviation and variance respectively.


```python
# To get the std of each sample:
A['Session_length'].std()

# B['Session_length'].std() for B
```

And the same for variance:

```python
# To get the variance of each sample:
A['Session_length'].var()

# B['Session_length'].var() for B
```

To find the range, we need to subtract the minimum value from the maximum value. We can use the `.min()` and the `.max()` functions to do this.

```python
# To find the range then, we subtract the min from the max for each group
A['Session_length'].max() - A['Session_length'].min()
```

```python
# And again for B
B['Session_length'].max() - B['Session_length'].min()
```

For percentiles, we'll refer to the `.percentile()` function from `numpy`. To get the 25th percentile for group A for example, we simply pass in the data, and set the parameter `q = 25`, as so:

```python
# To get the 25th percentile (or first quartile) of sample A:
np.percentile(A['Session_length'], q = 25)
```

To get the 75th percentile (or third quartile) we run the same function, with q = 75.

```python
# To get the 75th percentile (or first quartile) of sample A:
np.percentile(A['Session_length'], q = 75)
```

The interquartile range then is simply the range between the 75th and 25th percentiles -- or Q3-Q1.

For A:

```python
# To get the interquartile range for sample A:
np.percentile(A['Session_length'], q = 75) - np.percentile(A['Session_length'], q = 25)

# And then we can run the same for B.
```

Provide the outputs for each sample, and remember to make comments!


## Challenge 4: Histograms
- [ ] Visualise the shape of the distribution of the `Session_length` variable by:
  - [ ] Building a histogram for the entire dataframe,
  - [ ] Building two histograms, one for each sample, on the same plot.

Histograms are a great visual technique for understanding your distribution. We'll use a library called `seaborn` here as it was built for the purposes of data visualisation, and is very easy to get started with.

First, make sure the following runs error-free. For neatness purposes, scroll up and run this code in the Libraries section of your notebook:

```python
# The main visualisation library
import seaborn as sns

# For more granular manipulations of our graphs
import matplotlib.pyplot as plt

# To display our graphs in the notebook by default
%matplotlib inline
```

Seaborn is great for many high-level functions, but for more nuanced manipulations like adding a legend, changing titles, and rotating axis labels, we'll use an older and more flexible library called `matplotlib`. We run the final magic function to make our lives easier and display the graphs as we run the functions -- which may seem like it should be the default but isn't!

To build a histogram in seaborn, we use the `.distplot()` function, passing only one parameter, `a`, which is the data variable itself.

```python
# Distribution plot = Histogram in Seaborn lingo!
sns.distplot(a = df['Session_length'])
```

From the plot, we can see our data looks quite a bit like the normal distribution: it has one peak and the data seems to be symmetrical about this peak. We can also see that this peak seems to be around the ~270secs mark -- which is quite close to our mean!

To plot two distribution plots on the same axes -- one for each sample, A and B. We can run the same line of code twice in _the same cell_ in our notebook. Once you've run this, you can also add a legend for clarity using the following from `matplotlib`:

```python
# For group A and B separately
sns.distplot(A['Session_length'])

sns.distplot(B['Session_length'])


# We can add a legend using the following function (from matplotlib)
plt.legend(['Group A', 'Group B'])
```

Make sure the order of the legend categories is correct. In the above example, we ran the `.distplot()` function for sample A first, then that for sample B -- in which case, 'Group A' should be listed first in the legend labels.

From the above plot, we can see that the distributions of the sample are quite similar. This seems to be both in their shape -- i.e. width, symmetry and height -- and in closeness in value -- i.e. the peaks seem very close, if not identical to eachother, and the distributions overlap massively.

Reflecting on our research question: <br>
_**Did changing homepage designs between A and B, significantly affect average browsing session time?**_

It seems the answer is 'No': the difference  between our datasets, and specifically their means (i.e. the peaks of the distribution plots) seems almost non-existent, let alone significant!

## Challenge 5: Boxplots
- [ ] Visualise the distribution of the `Session_length` variable, with boxplots:
  - [ ] First, for the entire dataframe, then
  - [ ] For each of the samples.


Boxplots give us quite a bit of information all in one plot, and so can be quite powerful. We can use the `boxplot()` function from `seaborn` to build one.

The function takes the following main parameters:
- `x` -- this is the variable we'll be plotting on the X-axis
- `y` -- this is the variable we'll be plotting on the Y-axis

We'll need at least one of the above to run the function.

Optionally, you can also manipulate various other parameters, including the `whis` parameter. This specifies how big you want the 'whiskers' to be as a factor of the interquartile range. The default value is 1.5 -- i.e. the right whisker is set at _Q3 + 1.5*IQR_ and the left at _Q1 - 1.5*IQR_.

```python
# Specify either the 'x' or the 'y' parameter here

sns.boxplot(x = df['Session_length'])
```

Because the function is can take in two variables -- `x` and `y` -- we can easily plot the distributions of both samples on the same axes. In contrast, because the `.distplot()` function only took one variable, it meant we had to run two lines of code to get the two graphs on the same axes.

```python
#Instead of running two lines of code, the boxplot function allows us to separate the data by a categorical variable of our choice -- here, we choose 'Group'

sns.boxplot(x = df['Session_length'], y = df['Group'])
```


## *OPTIONAL* Challenges
- [ ] Explore the distributions of the `Session_length` with respect to the two genders.
- [ ] Explore the distributions of the `Session_length` with respect to the continent data.
- [ ] Extract the month from the `Date` column and explore the distributions of the `Session_length` with respect to month.
- [ ] Extract the weekday from the `Date` column and explore the distributions of the `Session_length` with respect to each day of the week.


### `Session_length` and `Gender`
To explore this relationship, we simply need to swap in the `Gender` variable in our seaborn plots.

For the distribution plots, it might also make it easier to create a subset for the different gender values.

```python
# Subsets for Males and Females
male = df[df['Gender'] == 'Male']

female = df[df['Gender'] == 'Female']

# For males and females separately
sns.distplot(male['Session_length'])

sns.distplot(female['Session_length'])


# We can add a legend using the following function (from matplotlib)
plt.legend(['Male users', 'Female users'])
```


For the boxplot, it's simply a matter of swapping in either the `x` or the `y` parameter.

```python
#Instead of running two lines of code, the boxplot function allows us to separate the data by a categorical variable of our choice -- here, we choose 'Gender'

sns.boxplot(x = df['Session_length'], y = df['Gender'])
```


### `Session_length` and `Continent`
We can approach this as we did with the `Gender` variable.


```python
# Subsets for each Continent
Americas = df[df['Continent'] == 'Americas']

Asia = df[df['Continent'] == 'Asia']

Africa = df[df['Continent'] == 'Africa']

Europe = df[df['Continent'] == 'Europe']

Oceania = df[df['Continent'] == 'Oceania']

# For each continent separately
sns.distplot(Americas['Session_length'])

sns.distplot(Asia['Session_length'])

sns.distplot(Africa['Session_length'])

sns.distplot(Europe['Session_length'])

sns.distplot(Oceania['Session_length'])


# We can add a legend using the following function (from matplotlib)
plt.legend(['Americas', 'Asia', 'Africa', 'Europe', 'Oceania'])
```

Too crammed! Try exploring pairs of continents instead.

For boxplots, this is much simpler:

```python
#Instead of running two lines of code, the boxplot function allows us to separate the data by a categorical variable of our choice -- here, we choose 'Continent'

sns.boxplot(x = df['Session_length'], y = df['Continent'])
```


### `Session_length` and `Month`
To explore this relationship, we need to first extract the month data from the `Date` column. We can do this easily once the column has been converted into a `datetime` format.

> See the [previous walkthrough](2_cleaning.md) for how to do this!

We can create a column, called `Month` in the following way, using the handy datetime `month_name()` function from `pandas`.

```python
# New column called 'Month'
df['Month'] = df['Date'].apply(lambda x: x.month_name())
```

For distribution plots:

```python
# Subsets for each Month
jan = df[df['Month'] == 'January']

feb = df[df['Month'] == 'February']

mar = df[df['Month'] == 'March']


# For each month separately
sns.distplot(jan['Session_length'])

sns.distplot(feb['Session_length'])

sns.distplot(mar['Session_length'])


# We can add a legend using the following function (from matplotlib)
plt.legend(['January', 'February', 'March'])
```

For boxplots:

```python
sns.boxplot(y = df['Month'], x = df['Session_length'])
```


### `Session_length` and `Weekday`
Similarly to the previous challenge, we again need to extract the weekday information from the `Date` column. We can do this with either an attribute like `dayofweek` which returns the position of the day in a week, or with a function like `day_name()` which returns the actual name of the day of the week.

Again, we extract his information and put it in a new column, called `Weekday`.

```python
# New column called 'Weekday'
df['Weekday'] = df['Date'].apply(lambda x: x.day_name())
```

For distribution plots:

```python
# Subsets for each Day of the week
mon = df[df['Weekday'] == 'Monday']

tue = df[df['Weekday'] == 'Tuesday']

wed = df[df['Weekday'] == 'Wednesday']

thu = df[df['Weekday'] == 'Thursday']

fri = df[df['Weekday'] == 'Friday']

sat = df[df['Weekday'] == 'Saturday']

sun = df[df['Weekday'] == 'Sunday']

# We can now choose any pair and plot to compare.
```

For boxplots:

```python
sns.boxplot(y = df['Weekday'], x = df['Session_length'])
```




  <br />

  ___
  [Previous](2_cleaning.md) |  [Next](4_htesting.md)
