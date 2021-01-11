# Data cleaning and transformation
Before we do any further exploration, or any hypothesis testing at all, we need to ensure our data is clean, and is in the right format.

## Cleaning
There are a few things to consider here. First, is missing values -- i.e. Nulls/NAs. We need to check if there are any at all, because the tests may not run properly if we leave them in -- and even if the functions for running the tests can ignore those NAs, their presence does not add any value to us as the analysts.

To make the entire dataset meaningful, we need to handle those Nulls in one of two main ways: either we replace them with something we infer to be the correct value, or we delete the row entirely. Deciding how we handle those Nulls will very much depend on the column at hand, so let's first find out where there are Nulls in our dataframe, if at all.

Once you've done this, you can now investigate that column(s) further to guide your decision. Remember you have one of two decisions to make here: either you delete those rows, or you fill those Nulls specifically with something you think is appropriate. If you do the latter, then you are making an inference, which may or not be correct, thereby biasing the sample. If you delete said rows then you are effectively reducing your sample size, which might affect the robustness of your tests.

> _Whichever method you end up choosing however, you will end up biasing your result in some way or another; there's always some cost associated with handling Nulls._

Once you've cleaned those NAs, the next thing to handle is incorrect data. Due to various reasons, perhaps due to human or system errors, you can end up with wrong information, which you have to handle before beginning any further exploration or testing.

Whilst there are no strict rules for the different forms wrong data can come in, you can look out for the following examples:

- Text when the variable should be numerical;
- Negative numbers when the variable should be positive;
- Generally nonsensical data like an age of 2016.

You should also look out for _outliers_, or extreme values. But be careful: determining a data point as extreme, does not mean you should remove it right away necessarily; keeping them might be useful. You also have to be conscious of how you are deciding that they are indeed outliers -- i.e. what makes them 'extreme'? Whilst you can use standard techniques like boxplots for example, understanding those points in the context of the dataset and/or the problem at hand, is most important.


## Transformation
Once you've managed to clean those Nulls, and handle any incorrect data, you can then start thinking about the structure of the data. This can mean various things depending on the project.

In our case, we need to make sure our data is in 'long' format, not 'wide' format, in order to run our test later on.

![Wide](./images/wide.JPG)
<br>**Fig. 1** - *Wide data - you can think of each column value as a column in and of its own right*.

![long](./images/long.JPG)
<br>**Fig. 2** - *Long data - where each row belongs to an observation, be it at the session or at the user level*.

In our case, the data is already in long format, so we don't need to make any transformations to structure.

However, it's important to know whether our data is at the user level, or at the session level. If our data is at the session level -- i.e. each row is a browsing session of our site -- then we may want to consider aggregating to get the user level -- where each row is a user, with an average browsing session length.

However, it's worth considering why we might want to do that in the first place -- or not at all. Whatever decision we make, to use session data, or user data, would greatly depend on the objective of the test. On one hand, if our users were shown both designs, for different sessions, and we were testing the differences the designs made on each of those session lengths, then it would make sense to keep it at the session level. On the other, if we were testing the effect of the designs on the users on average, then it would make more sense to group the sessions together for every user.

> There are various other metrics Sense Robotics could have chosen for their test. For e.g. they could have chosen Revenue Per Session (RPV), or average number of pageviews per session as their metrics. In both cases, it would have made more sense to keep the data at the session level. In our case however, our metric was session length, and each user was shown only one design - i.e. user 303 only ever saw design B -- which inclines us more to aggregate to the user level.


## Challenges
* [ ] Data Cleaning
  * [ ] Find which column(s) have any NA/Null values.
  * [ ] Investigate those rows specifically and make a decision to either delete them or replace the NAs with something you think is valid. There's no right or wrong answer here, so long as you are able to justify your position.
  * [ ] Explore for any incorrect data in any of the columns.
  * [ ] Handle the incorrect data, if there are any, appropriately.
<br><br>
* [ ] Data transformation
  * [ ] Ensure your data is in 'long' format.
  * [ ] [*OPTIONAL*] Convert the `Date` variable into a _`datetime`_ object using the appropriate function from `pandas`.
  * [ ] Check if the data is at the session level, or at the user level.
  * [ ] If at the session level, group the rows by `User_id`, so that each user only has one associated row, and the `Session_length` variable for that user is averaged across all their sessions.
  * [ ] When grouping the rows, create a new dataframe -- say, `df_grouped` -- for ease.
  * [ ] For this new dataframe, only keep the three columns: `User_id`, `Group`, and `Session_length`. For now, we can put the others to one side.


  ***
  > If you get stuck doing any of the above challenges, then don't you worry! It's part of the learning process. <br><br>
  Depending on the nature of the problem, we recommend using the following resources to aid you:<br>
  >  1. Your notes from the workshop, where appropriate.
  >  2. Google. Especially for debugging.
  >  3. Your mentor. Especially for help on the more challenging concepts (e.g. p-values!) and debugging library installation issues.
  >  4. The appropriate stage in the [walkthroughs](./walkthroughs/2_cleaning.md).
  >  5. The completed notebook. Don't jump straight to this one; it should be your final resort!<br><br>

  ***



  <br />

  ___
  [Previous](1_reading.md) |  [Next](3_eda.md)
