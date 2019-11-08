# Text Analysis (Python)

In order to access this workshop's content, you will need the following import statements:

```
import pandas as pd # For dataframe manipulation

import nltk  # machine learning with text

from nltk.corpus import stopwords, wordnet  # List of common words

from nltk.tokenize import word_tokenize  # Split text into significant forms

from nltk.stem import WordNetLemmatizer  # Reduce words to their root form ("lemma")

from sklearn.feature_extraction.text import CountVectorizer  # Convert text to sparse matrices

import matplotlib.pyplot as plt  # Complex visualisation configuration

import seaborn as sns  # Visualisation

from wordcloud import WordCloud  # Create wordclouds

from textblob import TextBlob  # Sentiment analysis
```

Additionally, the lines of code below install data required by `nltk`:

```
nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')
```
