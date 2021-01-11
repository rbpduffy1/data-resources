# Understanding your data

Now that we've posed our problem, it's time to get a look at our samples.

> *In a real-life A/B test of course, this is where you would begin the sampling process. We will assume we've done this now, and that the experiment has ended (we're probably in April 2020 right about now).*

## Reading in the data
********
DOWNLOAD
********

Once you've downloaded the data, labelled `sessions.csv`, and managed to import the `pandas` library successfully, you can now easily read it into your notebook with the `read_csv()` function. Once you've done that successfully, go ahead and output the first 5 rows to get a feel for the data.

Our dataframe has the following variables:
- **User_id**: Holds the unique IDs of each of our users.
- **Group**: This tells us whether our user was shown the first design (A) or the second design (B). Note that the user is shown *either one* but not both homepage designs.
- **Gender**: The gender of the user.
- **Continent**: The continent from which the user was visiting our site, for that particular browsing session.
- **Session_length**: The time the user spent on our homepage in *seconds*.
- **Date**: The start date of the session.

> <u>**Note**</u>: At this point, we're not sure if the data is at the user level -- i.e. each user has only one row representing them -- or at the session level -- i.e. each row represents a single browsing session of site, and many rows could belong to the same user. This is important to determine, but we'll do that in the next section.

## Getting a feel for your data
This is an important step in any project -- most especially in those where you didn't collect the data yourself! Here are a few ideas to get you started:

- Explore the dimensions of your dataframe -- how many rows and columns do we have?

- More specifically, how many samples do we have for A and B? I.e. how many of our users were given design A, and how many were given design B?

- Explore the data types in your dataframe -- which are categorical and which are numerical?

- Print the summary descriptive statistics for the numerical variables -- i.e. the mean, median, and perhaps percentiles.

## Challenges
- [ ] Download the dataset, `sessions.csv`.
- [ ] Read in the data using `pandas`.
- [ ] Get a feel for your data by:
  - [ ] Printing the first 5 rows and the last 5 rows.
  - [ ] Checking if there any columns beyond the ones mentioned above. If so, drop those columns.
  - [ ] Exploring the dimensions of the dataframe.
  - [ ] Exploring specifically the number of rows belonging samples A and B.
  - [ ] Exploring the data types of our variables.
  - [ ] Getting a high-level understanding of your dataset with one neat `pandas` function.
  - [ ] Printing the summary statistics for our dataframe using the appropriate `pandas` function.
  - [ ] Printing the summary statistics for samples A and B separately.

  ***
  > If you get stuck doing any of the above challenges, then don't you worry! It's part of the learning process. <br><br>
  Depending on the nature of the problem, we recommend using the following resources to aid you:<br>
  >  1. Your notes from the workshop, where appropriate.
  >  2. Google. Especially for debugging.
  >  3. Your mentor. Especially for help on the more challenging concepts (e.g. p-values!) and debugging library installation issues.
  >  4. The appropriate stage in the [walkthroughs](./walkthroughs/1_reading.md).
  >  5. The completed notebook. Don't jump straight to this one; it should be your final resort!<br><br>

  ***




  <br />

  ___
  [Previous](0_brief.md) |  [Next](2_cleaning.md)
