---
layout: page
title: NER Assignment
description: Topic Model
---

# NER Assignment
Georeferencing automatically detected place names in Edward Gibbon's *Decline and Fall of the Roman Empire* using the Pleiades gazatteer and `spaCy`.

Your assignment this week is to output a `CSV` file of place names, frequency and coordinates, as we did in class for a chapter of Gibbon of your choice. Try to find a chapter with a lot of places as we will be turning this data into an online map next week. The steps are:

* Choose a chapter from the text
* Begin a function by parsing input text
* Create a `spaCy` dictionary of entities and frequency
* Use the Pleiaes data from class to find coordinates for each place name
* Run your function on your chosen chapter
* Save your final `CSV`
* Come to class on Monday, ready to use it


```python
# import and download any relevant data
!python -m spacy download en_core_web_sm
!pip install wget
```

    Collecting en-core-web-sm==3.4.1
      Downloading https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-3.4.1/en_core_web_sm-3.4.1-py3-none-any.whl (12.8 MB)
    [K     |████████████████████████████████| 12.8 MB 3.5 MB/s eta 0:00:01
    [?25hRequirement already satisfied: spacy<3.5.0,>=3.4.0 in /Applications/anaconda3/lib/python3.9/site-packages (from en-core-web-sm==3.4.1) (3.4.3)
    Requirement already satisfied: wasabi<1.1.0,>=0.9.1 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.10.1)
    Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.10 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.10)
    Requirement already satisfied: pathy>=0.3.5 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.10.1)
    Requirement already satisfied: jinja2 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.11.3)
    Requirement already satisfied: srsly<3.0.0,>=2.4.3 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.4.5)
    Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (4.64.0)
    Requirement already satisfied: pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.10.2)
    Requirement already satisfied: catalogue<2.1.0,>=2.0.6 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.8)
    Requirement already satisfied: typer<0.8.0,>=0.3.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.7.0)
    Requirement already satisfied: numpy>=1.15.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.21.5)
    Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.0.9)
    Requirement already satisfied: thinc<8.2.0,>=8.1.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (8.1.5)
    Requirement already satisfied: packaging>=20.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (21.3)
    Requirement already satisfied: spacy-loggers<2.0.0,>=1.0.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.0.4)
    Requirement already satisfied: langcodes<4.0.0,>=3.2.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.3.0)
    Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.8)
    Requirement already satisfied: requests<3.0.0,>=2.13.0 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.27.1)
    Requirement already satisfied: setuptools in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (61.2.0)
    Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /Applications/anaconda3/lib/python3.9/site-packages (from spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.7)
    Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /Applications/anaconda3/lib/python3.9/site-packages (from packaging>=20.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.0.4)
    Requirement already satisfied: smart-open<7.0.0,>=5.2.1 in /Applications/anaconda3/lib/python3.9/site-packages (from pathy>=0.3.5->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (6.2.0)
    Requirement already satisfied: typing-extensions>=4.1.0 in /Applications/anaconda3/lib/python3.9/site-packages (from pydantic!=1.8,!=1.8.1,<1.11.0,>=1.7.4->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (4.1.1)
    Requirement already satisfied: charset-normalizer~=2.0.0 in /Applications/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.4)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /Applications/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (1.26.9)
    Requirement already satisfied: idna<4,>=2.5 in /Applications/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (3.3)
    Requirement already satisfied: certifi>=2017.4.17 in /Applications/anaconda3/lib/python3.9/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2021.10.8)
    Requirement already satisfied: blis<0.8.0,>=0.7.8 in /Applications/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.7.9)
    Requirement already satisfied: confection<1.0.0,>=0.0.1 in /Applications/anaconda3/lib/python3.9/site-packages (from thinc<8.2.0,>=8.1.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (0.0.3)
    Requirement already satisfied: click<9.0.0,>=7.1.1 in /Applications/anaconda3/lib/python3.9/site-packages (from typer<0.8.0,>=0.3.0->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (8.0.4)
    Requirement already satisfied: MarkupSafe>=0.23 in /Applications/anaconda3/lib/python3.9/site-packages (from jinja2->spacy<3.5.0,>=3.4.0->en-core-web-sm==3.4.1) (2.0.1)
    [38;5;2m✔ Download and installation successful[0m
    You can now load the package via spacy.load('en_core_web_sm')
    Collecting wget
      Downloading wget-3.2.zip (10 kB)
    Building wheels for collected packages: wget
      Building wheel for wget (setup.py) ... [?25ldone
    [?25h  Created wheel for wget: filename=wget-3.2-py3-none-any.whl size=9675 sha256=f9c64ae45609aba98983993b2c16de892051157f15fa54c628e0a14fdcd94e93
      Stored in directory: /Users/toshihironagase/Library/Caches/pip/wheels/04/5f/3e/46cc37c5d698415694d83f607f833f83f0149e49b3af9d0f38
    Successfully built wget
    Installing collected packages: wget
    Successfully installed wget-3.2



```python
import pandas as pd
import spacy
nlp = spacy.load('en_core_web_sm') # good idea to initialize here
import collections
#Download Text
import wget
import os
if not os.path.isfile('gibbon_text.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/gibbon_text.csv')

# downloading the Pleiades data we need:
if not os.path.isfile('places.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/places.csv')
if not os.path.isfile('names.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/names.csv')
names = pd.read_csv('names.csv')
places = pd.read_csv('places.csv')

```


```python
gibbon_by_chapter = pd.read_csv('gibbon_text.csv').rename(columns={'Unnamed: 0':'chapter'})
gibbon_by_chapter
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
      <th>chapter</th>
      <th>StringText</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Chapter 1</td>
      <td>\nIn the second century of the Christian era, ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Chapter 2</td>
      <td>\nIt is not alone by the rapidity or extent of...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chapter 3</td>
      <td>\nThe obvious definition of a monarchy seems t...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chapter 4</td>
      <td>\nThe mildness of Marcus, which the rigid disc...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chapter 5</td>
      <td>\nThe power of the sword is more sensibly felt...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Chapter 67</td>
      <td>\nThe respective merits of Rome and Constantin...</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Chapter 68</td>
      <td>\nThe siege of Constantinople by the Turks att...</td>
    </tr>
    <tr>
      <th>68</th>
      <td>Chapter 69</td>
      <td>\nIn the first ages of the decline and fall of...</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Chapter 70</td>
      <td>\nIn the apprehension of modern times, Petrarc...</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Chapter 71</td>
      <td>\nIn the last days of Pope Eugenius the Fourth...</td>
    </tr>
  </tbody>
</table>
<p>71 rows × 2 columns</p>
</div>




```python
# any helper functions you may need
def get_pleiades_id(term):
    name_row = names.loc[names['attested_form'] == term]
    if len(name_row) == 1:
        return int(name_row.place_id.iloc[0])
    else:
        name_row = names.loc[names['romanized_form_1'] == term]
        if len(name_row) == 1:
            return int(name_row.place_id.iloc[0])
        else:
            name_row = names.loc[names['romanized_form_2'] == term]
            if len(name_row) == 1:
                return int(name_row.place_id.iloc[0])
            else:
                name_row = names.loc[names['romanized_form_3'] == term]
                if len(name_row) == 1:
                    return int(name_row.place_id.iloc[0])
                else:
                    return None

def get_lat(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_latitude.iloc[0]
    
def get_long(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_longitude.iloc[0]
```


```python
# final functions
def get_locations(chapter):
    text = nlp(chapter)
    place_freq = collections.defaultdict(int)
    for entity in text.ents:
        if (entity.label_ == 'GPE') or (entity.label_ == 'LOC'):
            place_freq[entity.text] += 1 
    place_freq = dict(place_freq)
    place_freq_df = pd.DataFrame.from_dict(place_freq, orient='index').reset_index().rename(columns={'index':'place_name',0:'frequency'})
    places = pd.read_csv('places.csv')
    names = pd.read_csv('names.csv')
    place_freq_df['pleiades_id'] = place_freq_df['place_name'].apply(get_pleiades_id)
    place_freq_final = place_freq_df.dropna().reset_index(drop=True)
    place_freq_final['lat'] = place_freq_final['pleiades_id'].apply(get_lat)
    place_freq_final['long'] = place_freq_final['pleiades_id'].apply(get_long)
    return place_freq_final
```


```python
fifth_chapter = gibbon_by_chapter['StringText'][4]
get_locations(third_chapter)
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
      <th>place_name</th>
      <th>frequency</th>
      <th>pleiades_id</th>
      <th>lat</th>
      <th>long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rome</td>
      <td>17</td>
      <td>423025.0</td>
      <td>41.891775</td>
      <td>12.486137</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Africa</td>
      <td>1</td>
      <td>775.0</td>
      <td>32.500000</td>
      <td>7.500000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hercules</td>
      <td>1</td>
      <td>266032.0</td>
      <td>37.500000</td>
      <td>-0.500000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aricia</td>
      <td>1</td>
      <td>422844.0</td>
      <td>41.721400</td>
      <td>12.673347</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cinna</td>
      <td>1</td>
      <td>483971.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save result as CSV
get_locations(fifth_chapter).to_csv('ch4gibbon_places.csv')
```


```python

```
