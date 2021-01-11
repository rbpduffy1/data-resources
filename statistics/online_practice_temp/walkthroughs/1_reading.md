# Walkthrough: Reading the data
This section walks through the coding challenges given in the [_Understanding your data_](../1_reading.md) section of the activity.


## Challenge 1: Download the dataset
- [ ] Download the dataset, `sessions.csv`.


## Challenge 2: Read in the data
- [ ] Read in the data using `pandas`.

We can do this using the `.read_csv()` function, specifying the file name correctly. Let's say we call our Pandas dataframe, _`df`_.

```python
# We read in the .csv file using the 'read_csv' function from pandas
df = pd.read_csv('sessions.csv')
```


## Challenge 3: Getting a feel for your data
- [ ] Get a feel for your data by:
  - [ ] Checking if there any columns beyond the ones mentioned above. If so, drop those columns.
  - [ ] Exploring the dimensions of the dataframe.
  - [ ] Exploring specifically the number of rows belonging samples A and B.
  - [ ] Exploring the data types of our variables.
  - [ ] Getting a high-level understanding of your dataset with one neat `pandas` function.
  - [ ] Printing the summary statistics for our dataframe using the appropriate `pandas` function.
  - [ ] Printing the summary statistics for samples A and B separately.


### Challenge 3.1: Printing the first and last five rows
To do this, we can run the handy `.head()` and `.tail()` functions from `pandas`.

```python
# Show the first 5 rows
df.head()
```

```python
# Show the last 5 rows
df.tail()
```


### Challenge 3.2: Column verification
From the output in challenge 3.1 above, we can quickly see that our dataframe has the following features:

- **Unnamed: 0**: An index column.
- **User_id**: Holds the unique IDs of each of our users.
- **Group**: This tells us whether our user was shown the first design (A) or the second design (B). Note that the user is shown *either one* but not both homepage designs.
- **Gender**: The gender of the user.
- **Continent**: The continent from which the user was visiting our site, for that particular session.
- **Session_length**: The time the user spent on our homepage in *seconds*.
- **Date**: The start date of the session.

We also notice that the 'read' function also created an index column, which we should remove. We could do this by:

- **Option 1**: Running the `.drop()` method on our dataframe to drop the column in question.

```python
# Drop the index column from our dataframe
df.drop('Unnamed: 0', axis = 1, inplace = True)
```

- **Option 2**: Running the `read_csv()` function again with and setting the parameter `index_col = 0` to indicate the 0th column is an index column and Pandas should remove it.

```python
# Specify index_col = 0 when re-reading the dataframe:
df.read_csv('sessions.csv', index_col = 0)

# Check it's done its job right
df.head()
```


### Challenge 3.3: Exploring the dimensions
We can do this simply by using the `.shape` attribute on our dataframe:

```python
# Explore dimensions of our dataframe using the .shape attribute
df.shape
```

This returns _`(8000, 6)`_, which means our dataframe has 8000 rows and 6 columns.

### Challenge 3.4: Exploring dimensions of each sample
Whilst we can do this in one direct line of code, it may be wise to create two separate subsets for later use. Let's saw we call the first `A` and the second `B` that represent rows in the dataframe where the `Group` variable equals *A* and *B* respectively.

```python
# Create a subset for Group A
A = df[df['Group'] == 'A']

# Dimensions of A:
A.shape
```

```python
# Create a subset for Group B
B = df[df['Group'] == 'B']

# Dimensions of B:
A.shape
```


### Challenge 3.5: Data types
We can find out our data types by applying the `.dtypes` attribute to our dataframe.

```python
# Use the .dtypes attribute to get the data types in our dataframe
df.dtypes
```
We seem to have four categorical features:
- `Group`,
- `Gender`,
- `Continent` and
- `Date`

And two numerical features:
- `User_id` and
- `Session_length`.




### Challenge 3.6: One neat function  
We can also use the handy `.info()` function which gives us lots of other information as well, such as the dimensions of the dataset, the data types, which columns have NAs, and the amount of memory the data is using in our computer.

```python
# using .info() instead
df.info()
```

Of the two numerical features, `Session_length` is our response variable, so we can start with exploring it further first.

### Challenge 3.7: Summary statistics
We can get the summary statistics for `Session_length` by applying the `.describe()` function, which prints pretty much everything we need.

```python
# Get the summary stats for Session_length using the .describe() method
df['Session_length'].describe()
```
Note that running the function on the entire dataframe -- i.e. `df.describe()` would give us the summary statistics for both `User_id` and `Session_length` but we're only interested in the latter.

If we wanted to summarise the above further, we can choose say, the mean and standard deviation to describe our session times. From the output, the mean session time was **270.47 seconds** with a standard deviation of **30.80 seconds**.

However, we also notice that the **minimum** session time was -268.52 seconds! This of course doesn't make sense, and we should find an appropriate way to deal with this value -- as well as any other negative session time -- before running our tests.


### Challenge 3.8: Summary statistics for each sample
Similarly, we can run the `.describe()` function on our two samples separately.

```python
# Print the summary stats for A
A['Session_length'].describe()
```
And then again for B:

```python
# Print the summary stats for B
B['Session_length'].describe()
```

We notice that both outputs have troubling negative times, which we will delve into in the next section.




  <br />

  ___
  [Previous](0_brief.md) |  [Next](2_cleaning.md)
