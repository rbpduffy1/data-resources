# Text Analysis (Python)

## Setup instructions

### Data source

1. Download [the data](https://github.com/DecodedCo/data-resources/raw/master/datasets/text_analysis_workshop_data.zip) as a zip file
2. Unzip the file and move it to the same location as you normally run notebooks from

### Libraries

1. Run the following command in Anaconda prompt: `conda install -c conda-forge nltk wordcloud`
2. Start a new notebook in the same directory as your (unzipped) data file
3. Run the following code in your notebook:

```python
import pandas as pd  # Manage datasets
from nltk.sentiment.vader import SentimentIntensityAnalyzer  # Sentiment in social media
import seaborn as sns  # Plotting
from nltk.tokenize import word_tokenize  # Split text into words
from nltk.corpus import stopwords  # Lists of unimportant words
from collections import Counter  # Count word frequency
import matplotlib.pyplot as plt  # Visualisation
from wordcloud import WordCloud  # Wordclouds
from pandas.core.common import flatten  # Collapse lists of lists

import nltk
nltk.download("all")
```

If you see a pink message at this point, everything has worked as intended.

## Resources

[Completed workshop notebook](./text_analysis_workshop_completed_notebook.ipynb)

## Required regular expressions

- Remove hashtags and mentions: `[@#]\w+`

- Remove all non-letter characters: `[^a-z ]`
