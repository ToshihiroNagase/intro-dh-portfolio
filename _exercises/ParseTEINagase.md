---
layout: page
title: TEI Assignment
description: TEI Gibbon Fise and Fall
---

# Parsing a TEI Document

## Instructions

1. Parse the tei text of Gibbon's _Decline and Fall_ as found in `gibbon.xml`.
2. Extract all the footnotes and remove extraneous white space.
3. Place footnotes in a dataframe.
4. Save the dataframe as a csv file.

## Parsing TEI


```python
# imports
from bs4 import BeautifulSoup
import re
import pandas as pd
```


```python
# load xml file
with open('gibbon.xml', encoding='utf8', mode='r') as f:
    TEI_String = f.read()
```


```python
# use BeatifulSoup to instntiate tei object
TEI_Object = BeautifulSoup(TEI_String)
```


```python
# find all margin notes
foot_notes = TEI_Object.find_all('note', attrs={'place': 'margin'})
```


```python
# clean margin notes and add to a list
final_foot_notes = []
for foot_note in foot_notes:
    foot_note = re.sub(r'[\ \n]{2,}', '', foot_note.text)  # remove excess space
    final_foot_notes.append(foot_note)
```


```python
# convert list to dataframe
foot_notes_df = pd.DataFrame(final_foot_notes)
```


```python
# check dataframe
foot_notes_df.head()
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aureolus invades Italy, is defeated and beſieg...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A. D. 268.</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A. D. 268. March 20. Death of Gallienus.</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Character and elevation of the emperor Claudius.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Death of Aureolus.</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save datafram as csv
foot_notes_df.to_csv('foot_notes.csv')
```


```python

```
