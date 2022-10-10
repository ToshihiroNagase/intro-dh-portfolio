# Programming Historian

This notebook is my first programming historian assignment.

https://programminghistorian.org/en/lessons/text-mining-with-extracted-features

Takeaway: This lesson taught me about the basics of HTRC feature reader. This lesson can help as a guide to analyze literary texts. For example, HTRC feature reader can be used to look at the amount times a word shows up in a specific text or across texts. This can be used to make a temporal analysis on the use of a word. Any research question that looks at word or word type usage, HTRC feature reader is a tool that help answer that question. A main takeaway from this project was learning about data visualization tools. By executing functions from MatPlotLib, I was able to visualize data that was in a table. This is helpful because viewing data in several different ways can help show various patterns that weren't otherwise easily noticeable. For example, it was cool to visualize the amount of words in each page and compare it with the amount of sentences in a page. This Programming Historian Lesson has helped me better see the connection between coding and humanities. Furthermore, it has helped see what types of tools are available to analyze texts. I am excited to continue learning about Python to further develop my understanding of Classics.


```python
print("This is Python code")
```

    This is Python code



```python
#Here the feature reader is imported and initialized with file paths pointing to two Extracted feature files.
from htrc_features import FeatureReader
import os
paths = [os.path.join('data', 'sample-file1.json.bz2'), os.path.join('data', 'sample-file2.json.bz2')]
fr = FeatureReader(paths)
for vol in fr.volumes():
    print(vol.title)
```

    June / by Edith Barnard Delano ; with illustrations.
    You never know your luck; being the story of a matrimonial deserter, by Gilbert Parker ... illustrated by W.L. Jacobs.



```python
for vol in fr.volumes(): ## for loops
    print(vol.title)
```

    June / by Edith Barnard Delano ; with illustrations.
    You never know your luck; being the story of a matrimonial deserter, by Gilbert Parker ... illustrated by W.L. Jacobs.



```python
# Reading a single volume
vol = fr.first()
vol
```




<strong><a href='http://hdl.handle.net/2027/nyp.33433074811310'>June / by Edith Barnard Delano ; with illustrations.</a></strong> by <em>Delano, Edith Barnard 1874-1946 , Storer, Florence. ill , Riverside Press prt , Houghton Mifflin Company pbl </em> (1916, 274 pages) - <code>nyp.33433074811310</code>




```python
#The volume id can be used to pull more information from other sources. The scanned copy of the book can be found from the HathiTrust Digital Library, when available, by accessing
print(vol.handle_url)
```

    http://hdl.handle.net/2027/nyp.33433074811310



```python
vol.ht_bib_url ##access to API
```




    'http://catalog.hathitrust.org/api/volumes/full/htid/nyp.33433074811310.json'




```python
tokens = vol.tokens_per_page() #returns a DataFrame
# Show just the first few rows, so we can look at what it looks like
tokens.head()
```




    page
    1    5
    2    0
    3    1
    4    0
    5    1
    Name: tokenCount, dtype: int64




```python
%matplotlib inline
tokens.plot() # uses a method from Pandas to visualize data
# tells Jupyter to show the plotted image directly in the notebook web page. It only needs to be called once, and isn’t needed if you’re not using notebooks.
```




    <AxesSubplot:xlabel='page'>




    
![png](output_8_1.png)
    



```python
tl = vol.tokenlist()
# Let's look at some words deeper into the book:
# from 1000th to 1100th row, skipping by 15 [1000:1100:15]
tl[1000:1100:15]
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24</th>
      <th>body</th>
      <th>went</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="6" valign="top">25</th>
      <th rowspan="6" valign="top">body</th>
      <th>.</th>
      <th>.</th>
      <td>4</td>
    </tr>
    <tr>
      <th>added</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>come</th>
      <th>VB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>green</th>
      <th>JJ</th>
      <td>1</td>
    </tr>
    <tr>
      <th>knew</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>moment</th>
      <th>NN</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
vol.tokenlist(case=False)
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>lowercase</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">1</th>
      <th rowspan="5" valign="top">body</th>
      <th>0</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>07481131</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3433</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>jun6</th>
      <th>.</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">268</th>
      <th rowspan="5" valign="top">body</th>
      <th>cambridge</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>cbe</th>
      <th>NN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>massachusetts</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>u</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>»</th>
      <th>NN</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>28524 rows × 1 columns</p>
</div>




```python
vol.tokenlist(pos=False)
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
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">1</th>
      <th rowspan="5" valign="top">body</th>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>07481131</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3433</th>
      <td>1</td>
    </tr>
    <tr>
      <th>JUN6</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">268</th>
      <th rowspan="5" valign="top">body</th>
      <th>CAMBRIDGE</th>
      <td>1</td>
    </tr>
    <tr>
      <th>MASSACHUSETTS</th>
      <td>1</td>
    </tr>
    <tr>
      <th>U</th>
      <td>1</td>
    </tr>
    <tr>
      <th>cbe</th>
      <td>1</td>
    </tr>
    <tr>
      <th>»</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>28308 rows × 1 columns</p>
</div>




```python
vol.tokenlist(pages=False, case=False, pos=False)
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>lowercase</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="11" valign="top">body</th>
      <th>!</th>
      <td>526</td>
    </tr>
    <tr>
      <th>!'</th>
      <td>1</td>
    </tr>
    <tr>
      <th>!u</th>
      <td>1</td>
    </tr>
    <tr>
      <th>!—why</th>
      <td>1</td>
    </tr>
    <tr>
      <th>"</th>
      <td>1666</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>—</th>
      <td>167</td>
    </tr>
    <tr>
      <th>•</th>
      <td>9</td>
    </tr>
    <tr>
      <th>•5</th>
      <td>1</td>
    </tr>
    <tr>
      <th>•;</th>
      <td>1</td>
    </tr>
    <tr>
      <th>••</th>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>4528 rows × 1 columns</p>
</div>




```python
vol.tokenlist(section='header')
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">15</th>
      <th rowspan="5" valign="top">header</th>
      <th>...</th>
      <th>:</th>
      <td>1</td>
    </tr>
    <tr>
      <th>CONTENTS</th>
      <th>NNS</th>
      <td>1</td>
    </tr>
    <tr>
      <th>GREEN</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>I</th>
      <th>PRP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>I.</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">265</th>
      <th rowspan="2" valign="top">header</th>
      <th>AT</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>HOME</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">267</th>
      <th rowspan="3" valign="top">header</th>
      <th>9</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>AT</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>HOME</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>692 rows × 1 columns</p>
</div>




```python
vol.tokenlist(section='group')
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
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">1</th>
      <th>0</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>07481131</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3433</th>
      <th>CD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>JUN6</th>
      <th>.</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">268</th>
      <th>CAMBRIDGE</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>MASSACHUSETTS</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>U</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>cbe</th>
      <th>NN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>»</th>
      <th>NN</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>29924 rows × 1 columns</p>
</div>




```python
?vol.tokenlist #Documentation
```


```python
tl_simple = vol.tokenlist(pos=False, pages=False)
# .sample(5) returns five random words from the full result
tl_simple.sample(5)
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>regarded</th>
      <td>1</td>
    </tr>
    <tr>
      <th>usual</th>
      <td>6</td>
    </tr>
    <tr>
      <th>coal</th>
      <td>2</td>
    </tr>
    <tr>
      <th>lived</th>
      <td>5</td>
    </tr>
    <tr>
      <th>heart</th>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple['count'] > 100
```




    section  token
    body     !         True
             !'       False
             !u       False
             !—why    False
             "         True
                      ...  
             —         True
             •        False
             •5       False
             •;       False
             ••       False
    Name: count, Length: 4892, dtype: bool




```python
matches = tl_simple['count'] > 100
tl_simple[matches].sample(5)
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>that</th>
      <td>505</td>
    </tr>
    <tr>
      <th>but</th>
      <td>178</td>
    </tr>
    <tr>
      <th>to</th>
      <td>1086</td>
    </tr>
    <tr>
      <th>a</th>
      <td>671</td>
    </tr>
    <tr>
      <th>been</th>
      <td>135</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple[tl_simple['count'] > 100].sample(5)
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>had</th>
      <td>455</td>
    </tr>
    <tr>
      <th>so</th>
      <td>140</td>
    </tr>
    <tr>
      <th>from</th>
      <td>102</td>
    </tr>
    <tr>
      <th>with</th>
      <td>301</td>
    </tr>
    <tr>
      <th>when</th>
      <td>146</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple[(tl_simple['count'] > 150) & (tl_simple['count'] < 200)]
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="7" valign="top">body</th>
      <th>Mr.</th>
      <td>159</td>
    </tr>
    <tr>
      <th>be</th>
      <td>196</td>
    </tr>
    <tr>
      <th>but</th>
      <td>178</td>
    </tr>
    <tr>
      <th>do</th>
      <td>179</td>
    </tr>
    <tr>
      <th>is</th>
      <td>170</td>
    </tr>
    <tr>
      <th>on</th>
      <td>190</td>
    </tr>
    <tr>
      <th>—</th>
      <td>167</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.loc[(17),] #select information from page 17
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
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="11" valign="top">body</th>
      <th rowspan="2" valign="top">"</th>
      <th>''</th>
      <td>5</td>
    </tr>
    <tr>
      <th>``</th>
      <td>5</td>
    </tr>
    <tr>
      <th>'m</th>
      <th>VBP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>,</th>
      <th>,</th>
      <td>5</td>
    </tr>
    <tr>
      <th>.</th>
      <th>.</th>
      <td>10</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>we</th>
      <th>PRP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>when</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>why</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>within</th>
      <th>IN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>you</th>
      <th>PRP</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>113 rows × 1 columns</p>
</div>




```python
tl.loc[(17, 'body'),] #select body section of page 17
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">"</th>
      <th>''</th>
      <td>5</td>
    </tr>
    <tr>
      <th>``</th>
      <td>5</td>
    </tr>
    <tr>
      <th>'m</th>
      <th>VBP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>,</th>
      <th>,</th>
      <td>5</td>
    </tr>
    <tr>
      <th>.</th>
      <th>.</th>
      <td>10</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>we</th>
      <th>PRP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>when</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>why</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>within</th>
      <th>IN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>you</th>
      <th>PRP</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>113 rows × 1 columns</p>
</div>




```python
tl.loc[(17, 'body', 'Anne'),] #select words of Anne in body section
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
      <th>count</th>
    </tr>
    <tr>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.loc[(slice(None), slice(None), "Anne"),] #select count of words of Anne in all body
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>56</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>59</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>64</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>73</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>74</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>75</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>86</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>90</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>91</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>95</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>102</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>109</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>110</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>113</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>115</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>116</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>118</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>119</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>120</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>4</td>
    </tr>
    <tr>
      <th>121</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>122</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>126</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>127</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>129</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>139</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>142</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>143</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>145</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>146</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>147</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>149</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>152</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>157</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>159</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>162</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>164</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>166</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>171</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>179</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>182</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>185</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>192</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>194</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>195</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>197</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>201</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>219</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>224</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>225</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>264</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.loc[([37, 38, 52]),] #select pages 37, 38, 52
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">37</th>
      <th rowspan="5" valign="top">body</th>
      <th>!</th>
      <th>.</th>
      <td>5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">"</th>
      <th>''</th>
      <td>6</td>
    </tr>
    <tr>
      <th>``</th>
      <td>6</td>
    </tr>
    <tr>
      <th>'</th>
      <th>''</th>
      <td>1</td>
    </tr>
    <tr>
      <th>'cause</th>
      <th>,</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">52</th>
      <th rowspan="5" valign="top">body</th>
      <th>wrinkled</th>
      <th>JJ</th>
      <td>1</td>
    </tr>
    <tr>
      <th>you</th>
      <th>PRP</th>
      <td>4</td>
    </tr>
    <tr>
      <th>yours</th>
      <th>PRP</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">—</th>
      <th>CC</th>
      <td>1</td>
    </tr>
    <tr>
      <th>RB</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>377 rows × 1 columns</p>
</div>




```python
tl.loc[(slice(None), slice(None), ["Anne", "Hilary"]),] #Select counts for ‘Anne’ or ‘Hilary’ from all pages
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>19</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>20</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>259</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>264</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>265</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>266</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>267</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>115 rows × 1 columns</p>
</div>




```python
tl_all = vol.tokenlist(section='all')
chapter_pages = tl_all.loc[(slice(None), slice(None), "CHAPTER"),]
chapter_pages
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>35</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>56</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>73</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>91</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>115</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>141</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>158</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>174</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>193</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>217</th>
      <th>body</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>231</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>246</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Get just the page numbers from the search for "CHAPTER"
page_numbers = chapter_pages.index.get_level_values('page')

# Visualize the tokens-per-page from before
tokens.plot()

# Add vertical lines for pages with "CHAPTER"
import matplotlib.pyplot as plt
for page_number in page_numbers:
    plt.axvline(x=page_number, color='red')
```


    
![png](output_28_0.png)
    



```python
token_idx = tl.index.get_level_values("token")
tl[token_idx.str.isalpha()]
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <th>body</th>
      <th>JUNE</th>
      <th>NN</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">7</th>
      <th rowspan="4" valign="top">body</th>
      <th>LIBRARY</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>MEW</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>OF</th>
      <th>IN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>YORK</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">268</th>
      <th rowspan="5" valign="top">body</th>
      <th>A</th>
      <th>DT</th>
      <td>1</td>
    </tr>
    <tr>
      <th>CAMBRIDGE</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>MASSACHUSETTS</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>U</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>cbe</th>
      <th>NN</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>26199 rows × 1 columns</p>
</div>




```python
tl_simple.sort_values('count').head()
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>dangers</th>
      <td>1</td>
    </tr>
    <tr>
      <th>falsely</th>
      <td>1</td>
    </tr>
    <tr>
      <th>smilingly</th>
      <td>1</td>
    </tr>
    <tr>
      <th>fancy</th>
      <td>1</td>
    </tr>
    <tr>
      <th>smashed</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple.sort_values('count', ascending=False).head()
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>,</th>
      <td>3251</td>
    </tr>
    <tr>
      <th>"</th>
      <td>1666</td>
    </tr>
    <tr>
      <th>the</th>
      <td>1565</td>
    </tr>
    <tr>
      <th>.</th>
      <td>1534</td>
    </tr>
    <tr>
      <th>and</th>
      <td>1249</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.groupby(level=["pos"]).sum()
#The output is a count of how often each part-of-speech tag (“pos”) occurs in the entire book.
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
      <th>count</th>
    </tr>
    <tr>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>$</th>
      <td>2</td>
    </tr>
    <tr>
      <th>''</th>
      <td>954</td>
    </tr>
    <tr>
      <th>,</th>
      <td>3276</td>
    </tr>
    <tr>
      <th>-LRB-</th>
      <td>4</td>
    </tr>
    <tr>
      <th>-RRB-</th>
      <td>6</td>
    </tr>
    <tr>
      <th>.</th>
      <td>2345</td>
    </tr>
    <tr>
      <th>:</th>
      <td>398</td>
    </tr>
    <tr>
      <th>CC</th>
      <td>1731</td>
    </tr>
    <tr>
      <th>CD</th>
      <td>509</td>
    </tr>
    <tr>
      <th>DT</th>
      <td>3224</td>
    </tr>
    <tr>
      <th>EX</th>
      <td>90</td>
    </tr>
    <tr>
      <th>FW</th>
      <td>27</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>4541</td>
    </tr>
    <tr>
      <th>JJ</th>
      <td>2457</td>
    </tr>
    <tr>
      <th>JJR</th>
      <td>101</td>
    </tr>
    <tr>
      <th>JJS</th>
      <td>66</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>663</td>
    </tr>
    <tr>
      <th>NC</th>
      <td>4</td>
    </tr>
    <tr>
      <th>NN</th>
      <td>4700</td>
    </tr>
    <tr>
      <th>NNP</th>
      <td>2686</td>
    </tr>
    <tr>
      <th>NNPS</th>
      <td>9</td>
    </tr>
    <tr>
      <th>NNS</th>
      <td>1342</td>
    </tr>
    <tr>
      <th>PDT</th>
      <td>36</td>
    </tr>
    <tr>
      <th>POS</th>
      <td>376</td>
    </tr>
    <tr>
      <th>PRP</th>
      <td>3845</td>
    </tr>
    <tr>
      <th>PRP$</th>
      <td>1062</td>
    </tr>
    <tr>
      <th>RB</th>
      <td>2939</td>
    </tr>
    <tr>
      <th>RBR</th>
      <td>74</td>
    </tr>
    <tr>
      <th>RBS</th>
      <td>20</td>
    </tr>
    <tr>
      <th>RP</th>
      <td>192</td>
    </tr>
    <tr>
      <th>SYM</th>
      <td>2</td>
    </tr>
    <tr>
      <th>TO</th>
      <td>1102</td>
    </tr>
    <tr>
      <th>UH</th>
      <td>231</td>
    </tr>
    <tr>
      <th>VB</th>
      <td>1776</td>
    </tr>
    <tr>
      <th>VBD</th>
      <td>3445</td>
    </tr>
    <tr>
      <th>VBG</th>
      <td>601</td>
    </tr>
    <tr>
      <th>VBN</th>
      <td>933</td>
    </tr>
    <tr>
      <th>VBP</th>
      <td>702</td>
    </tr>
    <tr>
      <th>VBZ</th>
      <td>417</td>
    </tr>
    <tr>
      <th>WDT</th>
      <td>105</td>
    </tr>
    <tr>
      <th>WP</th>
      <td>244</td>
    </tr>
    <tr>
      <th>WP$</th>
      <td>2</td>
    </tr>
    <tr>
      <th>WRB</th>
      <td>309</td>
    </tr>
    <tr>
      <th>XP</th>
      <td>5</td>
    </tr>
    <tr>
      <th>``</th>
      <td>812</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Find most common tokens in the entire volume (sorting by most to least occurrences)
tl.groupby(level="token").sum().sort_values("count", ascending=False)
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
      <th>count</th>
    </tr>
    <tr>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>,</th>
      <td>3251</td>
    </tr>
    <tr>
      <th>"</th>
      <td>1666</td>
    </tr>
    <tr>
      <th>the</th>
      <td>1565</td>
    </tr>
    <tr>
      <th>.</th>
      <td>1534</td>
    </tr>
    <tr>
      <th>and</th>
      <td>1249</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>marketing</th>
      <td>1</td>
    </tr>
    <tr>
      <th>markets</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Perci&lt;</th>
      <td>1</td>
    </tr>
    <tr>
      <th>Pawn</th>
      <td>1</td>
    </tr>
    <tr>
      <th>murmuring</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>4892 rows × 1 columns</p>
</div>




```python
#Count how many pages each token/pos combination occurs on
tl.groupby(level=["token", "pos"]).count()
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>!</th>
      <th>.</th>
      <td>168</td>
    </tr>
    <tr>
      <th>!'</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>!u</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>!—why</th>
      <th>JJ</th>
      <td>1</td>
    </tr>
    <tr>
      <th>"</th>
      <th>''</th>
      <td>206</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>•</th>
      <th>NNS</th>
      <td>1</td>
    </tr>
    <tr>
      <th>•5</th>
      <th>''</th>
      <td>1</td>
    </tr>
    <tr>
      <th>•;</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">••</th>
      <th>NC</th>
      <td>1</td>
    </tr>
    <tr>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>5564 rows × 1 columns</p>
</div>




```python
from numpy import log
def tfidf(x):
    return x * log(1+vol.page_count / x.count())
# Will take a few seconds to run, depending on your system
idf_scores = tl.groupby(level=["token"]).transform(tfidf)
idf_scores[1000:1100:30]
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24</th>
      <th>body</th>
      <th>went</th>
      <th>VBD</th>
      <td>2.105417</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">25</th>
      <th rowspan="3" valign="top">body</th>
      <th>added</th>
      <th>VBD</th>
      <td>2.958376</td>
    </tr>
    <tr>
      <th>green</th>
      <th>JJ</th>
      <td>2.958376</td>
    </tr>
    <tr>
      <th>moment</th>
      <th>NN</th>
      <td>2.378223</td>
    </tr>
  </tbody>
</table>
</div>




```python
vol.line_counts()
#How many vertically spaced lines of text, a measure related to the phyical format of the page.
```




    page
    1      3
    2      1
    3      1
    4      0
    5      1
          ..
    270    0
    271    0
    272    0
    273    1
    274    1
    Name: lineCount, Length: 274, dtype: int64




```python
vol.sentence_counts()
#How many sentences of text: a measure related to the content on a page.
```




    page
    1      1
    2      0
    3      1
    4      0
    5      1
          ..
    270    0
    271    0
    272    0
    273    0
    274    0
    Name: sentenceCount, Length: 274, dtype: int64




```python
vol.empty_line_counts()
# How many larger vertical spaces are there on the page between lines of text
```




    page
    1      1
    2      1
    3      0
    4      0
    5      0
          ..
    270    0
    271    0
    272    0
    273    1
    274    1
    Name: emptyLineCount, Length: 274, dtype: int64




```python
vol.begin_line_chars()
vol.end_line_chars()
```

    /Applications/anaconda3/lib/python3.9/site-packages/htrc_features/parsers.py:428: FutureWarning: In a future version of pandas all arguments of DataFrame.sort_index will be keyword-only.
      df.sort_index(0, inplace=True)





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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>place</th>
      <th>char</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">1</th>
      <th rowspan="2" valign="top">body</th>
      <th rowspan="2" valign="top">end</th>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <th>body</th>
      <th>end</th>
      <th>:</th>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <th>body</th>
      <th>end</th>
      <th>E</th>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <th>body</th>
      <th>end</th>
      <th>.</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">267</th>
      <th rowspan="2" valign="top">body</th>
      <th rowspan="2" valign="top">end</th>
      <th>n</th>
      <td>1</td>
    </tr>
    <tr>
      <th>t</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">268</th>
      <th rowspan="3" valign="top">body</th>
      <th rowspan="3" valign="top">end</th>
      <th>A</th>
      <td>1</td>
    </tr>
    <tr>
      <th>S</th>
      <td>1</td>
    </tr>
    <tr>
      <th>e</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>3106 rows × 1 columns</p>
</div>




```python
#The count of different characters along the left-most and right-most sides of a page
```


```python
line_counts = vol.line_counts()
plt.plot(line_counts)
```




    [<matplotlib.lines.Line2D at 0x7fd265cad400>]




    
![png](output_41_1.png)
    



```python

```
