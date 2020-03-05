# Text Analysis (Python)

In order to access this workshop's content, you will need to do the following:

1. Download [the data](https://github.com/DecodedCo/data-resources/raw/master/datasets/apple-tweets.zip) as a zip file
2. Unzip the file to your desired location
3. Run the following command in Anaconda prompt: `conda install -c conda-forge textblob nltk gensim wordcloud translate googletrans`
4. Start a new notebook from the same directory as your data
5. Run the following code in your notebook:

```
import pandas as pd # For dataframe manipulation

import nltk  # machine learning with text

from nltk.corpus import stopwords # List of common words

from nltk.tokenize import word_tokenize  # Split text into significant forms

from sklearn.feature_extraction.text import CountVectorizer  # Convert text to sparse matrices

import matplotlib.pyplot as plt  # Complex visualisation configuration

from wordcloud import WordCloud  # Create wordclouds

from textblob import TextBlob  # Sentiment analysis

from gensim.models import Word2Vec  # Understand word context

from translate import Translator  # Translate text

from googletrans import Translator as G_Translator  # Translate text
```
6. Once your notebook has successfully run the code above, run the code below in your notebook:

```
nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')
```

If you see a pink message at this point, everything has worked as intended (probably).
