---
layout: page
title: Final Project Code & Conclusion
description: This is my Final Project Code and Conclusion.
---

## Discussion

The coding project will take in any XML file from Tuft's Perseus Digital Library and count the frequency of each word in the text. Tuft's Perseus Digital Lbrary is a digital repository that has Greek and Latin Texts and Translations. Users can find more information here: http://www.perseus.tufts.edu/hopper/about

This project will sort the words into descending order based off of frequency and output a bar graph. This allows user's who are researching texts around Zipf's model to input a XML file and display graph with frequency of words from the text. This tool can be used to see whether texts actually follow Zipf's law.

From the texts like Hemingway to Ceasar's Gallic War, we can see that most texts generally follow Zipf's law. The larger the text body, the closer it seems to align with the law. One outlier that I saw was Herodotus, which had two greek words that were by far the most popular words. Another intersting result I found was that different words were popular in different languages. For example, in english the most frequent word is "the" while in Latin, the most frequent word is "in".

This project is a starting point for research that can be done around word frequency. I am interested to learn about other languages outside of the classics. Will those texts also follow the same model? How will charachter based languages like Mandarin fare? I am also interested to look into Herodotus. What makes his texts different than the others? Do different authors have different models even if they speak the same language? Lastly, I am also interested in learning why certain words are popular in a language and different than in another.



## Code


```python
## Imports
from bs4 import BeautifulSoup
import re
import pandas as pd
import collections
import matplotlib.pyplot as plt
from bokeh.plotting import figure, show
from bokeh.io import output_file
from prettytable import PrettyTable
```


```python
## Method: Read XML File
## Inputs: String of XML file name from Perseus
## Return: list of words
def parse_xml(xml_file):
    with open(xml_file, encoding='utf8', mode='r') as f:
        TEI_String = f.read()
        soup = BeautifulSoup(TEI_String)
        newSoup = soup.find('text')
        # Removes HTML Tags
        textPerseus = newSoup.get_text()
        # Split the text into a list of words
        words = textPerseus.split()
        return(words)
```


```python
## Method: Count and Sort Words
## Takes in a list of Words
## Returns sorted dictionary
def count_sort(words):
    # Count the number of occurrences of each word
    word_counts = {}
    for word in words:
        if word in word_counts:
            word_counts[word] += 1
        else:
            word_counts[word] = 1

    #sort in descending order
    ## https://www.w3schools.com/python/ref_func_sorted.asp  
    sorted_word_counts = sorted(word_counts.items(), key=lambda x: x[1], reverse=True)
    return(sorted_word_counts)
```


```python
## Method: Make a Bokeh Graph
## Takes in a list
## Prints an output file with graph
def bokeh_graph(sorted_word_counts, term_numbers):
    # Extract the words and their counts into separate lists
    # Only Take Top 50 Words
    first_fifty_terms = sorted_word_counts[:term_numbers]
    words, counts = zip(*first_fifty_terms)

    # Create the bar plot
    p = figure(x_range=words, plot_height=500, plot_width=1000)
    p.vbar(x=words, top=counts, width=0.9)

    # Show the plot
    output_file("word_counts.html")
    show(p)
```


```python
## Method: Make A Table
def table_Pretty(sorted_word_counts, term_numbers):

    # Create a table to display the results
    table = PrettyTable()
    table.field_names = ["Word", "Frequency"]

    # Add the 30 most common words to the table
    for word, frequency in sorted_word_counts[:30]:
        table.add_row([word, frequency])

    # Print the table
    print(table)
```


```python
## Main:
## XML File = 'Perseus_text_1999.02.0002.xml'
wordsM = parse_xml('Perseus_text_1999.02.0002.xml')
sorted_word_countsM = count_sort(wordsM)
## Number of Terms we Want to See in Graph = 50
bokeh_graph(sorted_word_countsM,50)
## Number of Terms we Want to See in Table = 50
table_Pretty(sorted_word_countsM,50)
```

    +---------+-----------+
    |   Word  | Frequency |
    +---------+-----------+
    |    in   |    1219   |
    |    et   |    952    |
    |    ad   |    776    |
    |   cum   |    578    |
    |    ex   |    484    |
    |  atque  |    457    |
    |    se   |    433    |
    |    ut   |    395    |
    |   quod  |    391    |
    |    ab   |    368    |
    |   non   |    361    |
    |   qui   |    356    |
    |  neque  |    248    |
    |   esse  |    241    |
    |   quae  |    240    |
    |    a    |    206    |
    |   quam  |    203    |
    |    de   |    202    |
    |  Caesar |    202    |
    |    ac   |    194    |
    |    si   |    174    |
    |   aut   |    172    |
    |    ne   |    171    |
    | omnibus |    160    |
    |    eo   |    158    |
    |  omnes  |    152    |
    |   est   |    136    |
    | castris |    132    |
    |   eius  |    129    |
    |   sibi  |    127    |
    +---------+-----------+



```python

```
