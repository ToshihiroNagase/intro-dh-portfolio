---
layout: page
title: Chonicling America API Assignment
description: Learning about API
---

# Chronicling America API Assignment
In this assignment, you are tasked with:
* searching Chronicling America's API for a key word of your choice
* parsing your results from a dictionary to a `DataFrame` with headings "title", "city", 'date", and "raw_text"
* processing the raw text by removing "\n" characters, stopwords, and then lemmatizing the raw text before adding it to a new column called "lemmas."
* saving your `DataFrame` to a csv file

If you need any help with this assignment please email micah.saxton@tufts.edu



```python
# Using the Chronicling America create a search for any term you'd like 
# (i.e. "Civil War", "Louisiana Purchase", "Babe Ruth" etc.) 
# Then parse your results into a DataFrame with headings "title", "city", 'date", and "raw_text". 
# Next, clean up the raw text by removing "\n" characters, stopwords, and then lemmatize the raw text 
#before adding it to a new column called "lemmas." Finally, save as .csv. 
#When you're finished upload your notebook to your DH portfolio under "Exercises."
```


```python
#Took From: https://stackoverflow.com/questions/69284181/modulenotfounderror-no-module-named-en-core-web-sm
!pip install spacy -q
!python -m spacy download en_core_web_sm -q
```

    [38;5;2m✔ Download and installation successful[0m
    You can now load the package via spacy.load('en_core_web_sm')



```python
# imports
import requests
import json
import math
import pandas as pd
import spacy
```


```python
# initial search
#By searching chicken url: https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1=1777&date2=1963&proxtext=chicken&x=18&y=15&dateFilterType=yearRange&rows=20&searchType=basic
# add &format=json
url = 'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1=1777&date2=1963&proxtext=chicken&x=16&y=8&dateFilterType=yearRange&rows=20&searchType=basic&format=json'
response = requests.get(url) # makes the webpage a object
raw = response.text  # draws the text from webpage as a string
results = json.loads(raw)  # changes string into dict

```


```python
# find total amount of pages
total_Pages = math.ceil(results['totalItems'] / results['itemsPerPage'])
print(total_Pages)
```

    112885



```python
results.keys
print('totalItems:', results['totalItems'])
print('endIndex:', results['endIndex'])
print('startIndex:', results['startIndex'])
print('itemsPerPage:', results['itemsPerPage'])
print('Length and type of items:', len(results['items']), type(results['items']))
```

    totalItems: 2257687
    endIndex: 20
    startIndex: 1
    itemsPerPage: 20
    Length and type of items: 20 <class 'list'>



```python
# query the api and save to dict 
data = []
start_date = '1900'
end_date = '1963'
search_term = 'chicken'
for i in range(1, total_Pages+1):  # total_pages+1
    url = (f'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1={start_date}'
           f'&date2={end_date}&proxtext={search_term}&x=16&y=8&dateFilterType=yearRange&rows=20'
           f'&searchType=basic&format=json&page={i}')  # f-string
    response = requests.get(url)
    raw = response.text
    print(response.status_code)  # checking for errors
    results = json.loads(raw)
    items_ = results['items']
    for item_ in items_:
        temp_dict = {}
        temp_dict['title'] = item_['title_normal']
        temp_dict['city'] = item_['city']
        temp_dict['date'] = item_['date']
        temp_dict['raw_text'] = item_['ocr_eng']
        data.append(temp_dict)
```

    200
    200
    200
    200
    504


```python
# convert dict to dataframe
df = pd.DataFrame.from_dict(data)
```


```python
#Check
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>city</th>
      <th>date</th>
      <th>raw_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>1962-11-11</td>
      <td>1. Brown chicken in skillet 3 C °° k 45 minute...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>1944-11-26</td>
      <td>SPECIAL\nFLAVOR\n"fifae evet# 4kv\ndbAe*/\nOld...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>1946-06-23</td>
      <td>The hub of the yards, the turntable has an eng...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>1948-09-05</td>
      <td>WONDERFUL\nin canned soup\ndiscovered in natio...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>evening star.</td>
      <td>[Washington]</td>
      <td>1961-10-29</td>
      <td>• /\n( |l»♦ » » • '\nWilk htJrr.Wkit «^K\nchic...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# convert date column from string to date-time object
df['date'] = pd.to_datetime(df['date'])
```


```python
# sort by date
sorted_df = df.sort_values(by='date')
```


```python
# write fuction to process text
nlp = spacy.load("en_core_web_sm")

junk_words = ['hesse']  # you can add any words you want removed here

def process_text(text):
    """Remove new line characters and lemmatize text. Returns string of lemmas"""
    text = text.replace('\n', ' ')
    doc = nlp(text)
    tokens = [token for token in doc]
    no_stops = [token for token in tokens if not token.is_stop]
    no_punct = [token for token in no_stops if token.is_alpha]
    lemmas = [token.lemma_ for token in no_punct]
    lemmas_lower = [lemma.lower() for lemma in lemmas]
    lemmas_string = ' '.join(lemmas_lower)
    return lemmas_string
    
```


```python

```


```python
# apply process_text function to raw_text column
sorted_df['lemmas'] = sorted_df['raw_text'].apply(process_text)
```


```python
sorted_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>city</th>
      <th>date</th>
      <th>raw_text</th>
      <th>lemmas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>52</th>
      <td>saint paul globe.</td>
      <td>[Saint Paul]</td>
      <td>1905-01-01</td>
      <td>TOMMY HOG'S FATHER MOST SADLY MISTOOK L ~~~L\n...</td>
      <td>tommy hog father sadly mistook l think easy fi...</td>
    </tr>
    <tr>
      <th>39</th>
      <td>san francisco call.</td>
      <td>[San Francisco]</td>
      <td>1905-01-15</td>
      <td>TOMMY HOG'S FATHER MOST SADLY MISTOOK\nWHEN HE...</td>
      <td>tommy hog father sadly mistook think easy fire...</td>
    </tr>
    <tr>
      <th>46</th>
      <td>san francisco call.</td>
      <td>[San Francisco]</td>
      <td>1911-03-12</td>
      <td>UNCLE MOSE &gt;l\nPUPS\nvia\n■ Hi i ii i\nS&gt; How ...</td>
      <td>uncle mose l pups hi ii s dog know hid snow ko...</td>
    </tr>
    <tr>
      <th>11</th>
      <td>san francisco call.</td>
      <td>[San Francisco]</td>
      <td>1911-04-30</td>
      <td>STEPBROTHERS\nGus promised to take the chicken...</td>
      <td>stepbrothers gus promise chicken straight home...</td>
    </tr>
    <tr>
      <th>36</th>
      <td>san francisco call.</td>
      <td>[San Francisco]</td>
      <td>1911-05-21</td>
      <td>YENS © i By Taylorl\nHe Always Bane Unlucky Fe...</td>
      <td>yens taylorl bane unlucky feßer willie fibb dw...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save to csv
sorted_df.to_csv(f'../data/{search_term}{start_date}-{end_date}.csv', index=False)
```
