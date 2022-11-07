---
layout: page
title: Python Crash Course Chapter 8
description: My answers to Chapter 8 Python Crash Course Exercises
---

```python
#8-1. Message: Write a function called display_message() that prints one sentence telling everyone what you are learning about in this chapter. 
#Call the function, and make sure the message displays correctly.

def display_message():
    print("Hello! We are learning about functions.")

display_message()
```

    Hello! We are learning about functions.



```python
#8-2. Favorite Book: Write a function called favorite_book() that accepts one parameter, title. 
# The function should print a message, such as One of my favorite books is Alice in Wonderland. 
# Call the function, making sure to include a book title as an argument in the function call.

def display_message(bookname):
    print(f"My favorite book is {bookname.title()}.")

display_message("The Great Gatsby")
```

    My favorite book is The Great Gatsby.



```python
# 8-3. T-Shirt: Write a function called make_shirt() that accepts a size and the text of a message that 
# should be printed on the shirt. The function should print a sentence summarizing the size of the shirt 
# and the message printed on it. Call the function once using positional arguments to make a shirt. 
# Call the function a second time using keyword arguments.

def make_shirt(size, text):
    print(f"The shirt size is: {size}. The text on the shirt is: {text}")
          
make_shirt("m", "Dont say hi")
make_shirt(size='m', text='Dont say hi')
```

    The shirt size is: m. The text on the shirt is: Dont say hi
    The shirt size is: m. The text on the shirt is: Dont say hi



```python
#8-5. Cities: Write a function called describe_city() that accepts the name of a city and its country. 
# The function should print a simple sentence, such as Reykjavik is in Iceland. 
# Give the parameter for the country a default value. Call your function for three different cities, 
# at least one of which is not in the default country.

def describe_city(city, country = "Iceland"):
    print(f"The city {city} is in {country}")
    
describe_city("Reykjavic")
describe_city("Colorado","United States of America")
describe_city(city = "Beijing",country = "China")


```

    The city Reykjavic is in Iceland
    The city Colorado is in United States of America
    The city Beijing is in China



```python
#8-6. City Names: Write a function called city_country() that takes in the name of a city and its country. 
#The function should return a string formatted like this:
#"Santiago, Chile"
# Call your function with at least three city-country pairs, and print the values that are returned.

def city_country(city, country):
    print(f"{city}, {country}")

city_country("Seattle", "USA")
city_country("Vancouver", "Canada")
city_country("Quito", "Ecuador")
```

    Seattle, USA
    Vancouver, Canada
    Quito, Ecuador



```python
#8-7. Album: Write a function called make_album() that builds a dictionary describing a music album. 
#The function should take in an artist name and an album title, and it should return a dictionary 
#containing these two pieces of information. Use the function to make three dictionaries representing 
#different albums. Print each return value to show that the dictionaries are storing the album information correctly.

# Use None to add an optional parameter to make_album() that allows you to store the number of songs on an album. 
#If the calling line includes a value for the number of songs, add that value to the album’s dictionary. 
# Make at least one new function call that includes the number of songs on an album.

def make_album(artist, title):
    person = {'artist': artist, 'title': title}
    return person

def make_albumtwo(artist, title, songnum = None):
    person = {'artist': artist, 'title': title}
    if songnum:
        person['songnum'] = songnum
    return person

album = make_album('Ed Sheeran', 'X')
print(album)

album = make_album('Shawn Mendes', 'illuminate')
print(album)

album = make_album('BETWEEN FRIENDS', 'we just need some time together')
print(album)

album = make_albumtwo('BETWEEN FRIENDS', 'we just need some time together',songnum = 2)
print(album)
```

    {'artist': 'Ed Sheeran', 'title': 'X'}
    {'artist': 'Shawn Mendes', 'title': 'illuminate'}
    {'artist': 'BETWEEN FRIENDS', 'title': 'we just need some time together'}
    {'artist': 'BETWEEN FRIENDS', 'title': 'we just need some time together', 'songnum': 2}



```python

```
