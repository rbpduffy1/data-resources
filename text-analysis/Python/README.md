# Text Analysis (Python)

## Setup instructions

### Libraries

This workshop requires an important library, which you are unlikely to already have installed. In order to install it, run the following command in the terminal:

`pip install nltk`

If you normally use `conda` to install libraries, rather than `pip`, then open Anaconda Prompt and run this command instead:

`conda install -c conda-forge nltk`

In order to check that the libraries have installed correctly, and that you have all the other necessary modules, complete the following steps:

1. Start a new notebook in the same directory as your (unzipped) data file
2. Run the following code in your notebook:

```python
import nltk  # our go-to tool for text processing
import pandas as pd  # for data manipulation and loading
from nltk.sentiment.vader import SentimentIntensityAnalyzer  # for sentiment analysis
import seaborn as sns  # for plotting
from nltk.tokenize import word_tokenize, sent_tokenize  # for word and sentence tokenisation
from nltk.corpus import stopwords  # lists of unimportant words (in several languages)
from collections import Counter  # to count word frequencies
import matplotlib.pyplot as plt  # for visualisation
from pandas.core.common import flatten  # to collapse lists of lists
```

There should be **no output** from this cell.

If the code above runs without error, you've got all the libraries required for the workshop installed. If any of the libraries fail to import, you'll need to install each one using `conda` or `pip`, depending on your specific tech setup.

### Required data files

The workshop also requires some supplementary data files. Inside your notebook, run the following code:

```python
# Download word lists

nltk.download("all")
```

If you see a pink message at this point, everything has worked as intended. If you see an error message, please refer to the [installation errors](#installation-errors) section at the end of this document.

## Resources

* [Completed workshop notebook](workshop_completed.ipynb)
* [Dataset for this workshop (a collection of tweets to @Apple)](apple_tweets.csv)

## Instructions for downloading the data

* Go to [this link](apple_tweets.csv).
* Click the **download** button on the right, which should take you to a text page - this is the raw CSV file being displayed in your browser.
* Right click on the page and select "save as". If your computer doesn't recognise the file type automatically (comma-separated values, or CSV), select "all files" for the format and name the file `apple_tweets.csv`.

## Installation errors

Please note that the downloader application used here may be blocked by firewalls within your work environment. This is likely due to security restrictions preventing code from calling resources by URL.

If this is the case, you will need to first comment out the line containing nltk.download(), so that it does not run as part of the code. After this, download the [ntlk_data file](https://github.com/DecodedCo/data-resources/raw/master/datasets/text_analysis_workshop_nltk_data.zip).

Once the file has downloaded, you will need to place it in the appropriate directory. This varies between machines, but the options below should work for different operating systems:

### For Windows

`~[user directory]\AppData\Roaming\`

You will need to enter the path up to AppData directly into File Explorer as it is a hidden folder.

### For Mac

`~[user directory]\`

Place the file inside the directory, and unzip it. It should create a folder called "nltk_data" in the same location.
If you work in an environment, where you cannot alter the AppData directory, or changes are wiped within the same directory, alternative locations to store in the nltk_data folder, these can placed in:

- The root folder of your Anaconda/Miniconda installation
- The root of other drives, where data does not get wiped
