---
layout: page
title: Python Crash Course Chapter 6
description: My answers to Chapter 6 Python Crash Course Exercises
---

# Chapter 6


```python
# 6-1. Person: Use a dictionary to store information about a person you know. 
#Store their first name, last name, age, and the city in which they live. 
#You should have keys such as first_name, last_name, age, and city. 
#Print each piece of information stored in your dictionary.
Tnagase = {'first_name': 'Toshihiro', 'last_name': 'Nagase', 'age':22, 'city': 'Seattle'}
print(Tnagase)
```

    {'first_name': 'Toshihiro', 'last_name': 'Nagase', 'age': 22, 'city': 'Seattle'}



```python
# 6-2. Favorite Numbers: Use a dictionary to store people’s favorite numbers. 
# Think of five names, and use them as keys in your dictionary.
favorite_numbers = {
    'shaps': '5',
    'zach': '6',
    'toshi': '7',
    'samson': '8',
    }
numb = favorite_numbers['shaps']
print(f"Shaps' favorite number is {numb}.")

numb = favorite_numbers['zach']
print(f"Zach's favorite number is {numb}.")

numb = favorite_numbers['shaps']
print(f"Toshi's favorite number is {numb}.")

numb = favorite_numbers['shaps']
print(f"Samson's favorite number is {numb}.")
```

    Shaps' favorite language is 5.
    Zach's favorite language is 6.
    Toshi's favorite language is 5.
    Samson's favorite language is 5.



```python
# 6-3. Glossary: A Python dictionary can be used to model an actual dictionary. 
# However, to avoid confusion, let’s call it a glossary.
glossary = {
    'boolean': 'denoting a system of algebraic notation used to represent logical propositions, especially in computing and electronics.',
    'lists': 'a number of connected items or names written or printed consecutively, typically one below the other.',
    'variable': 'a data item that may take on more than one value during the runtime of a program.',
    'strings': 'data values that are made up of ordered sequences of characters',
    'index': 'a data structure to facilitate fast lookup of terms and clauses in a logic program, deductive database, or automated theorem prover.',
   }

definition = glossary['boolean']
print(f"boolean: {definition}.")

definition = glossary['lists']
print(f"lists: {definition}.")

definition = glossary['variable']
print(f"variable: {definition}.")

definition = glossary['strings']
print(f"strings: {definition}.")

definition = glossary['index']
print(f"index: {definition}.")

```

    boolean: denoting a system of algebraic notation used to represent logical propositions, especially in computing and electronics..
    lists: a number of connected items or names written or printed consecutively, typically one below the other..
    variable: a data item that may take on more than one value during the runtime of a program..
    strings: data values that are made up of ordered sequences of characters.
    index: a data structure to facilitate fast lookup of terms and clauses in a logic program, deductive database, or automated theorem prover..



```python
#6-4. Glossary 2: Now that you know how to loop through a dictionary, 
#clean up the code from Exercise 6-3 (page 99) by replacing your series of print() calls with a 
# loop that runs through the dictionary’s keys and values.

glossary = {
    'boolean': 'denoting a system of algebraic notation used to represent logical propositions, especially in computing and electronics.',
    'lists': 'a number of connected items or names written or printed consecutively, typically one below the other.',
    'variable': 'a data item that may take on more than one value during the runtime of a program.',
    'strings': 'data values that are made up of ordered sequences of characters',
    'index': 'a data structure to facilitate fast lookup of terms and clauses in a logic program, deductive database, or automated theorem prover.',
    'example 1': 'no definiton',
    'example 2': 'no definiton',
    'example 3': 'no definiton',
    'example 4': 'no definiton',
    'example 5':'no definiton',
}
for name in sorted(glossary.keys()):
    definition = glossary[name].title()
    print(f"{name.title()}: {definition}")

```

    Boolean: Denoting A System Of Algebraic Notation Used To Represent Logical Propositions, Especially In Computing And Electronics.
    Example 1: No Definiton
    Example 2: No Definiton
    Example 3: No Definiton
    Example 4: No Definiton
    Example 5: No Definiton
    Index: A Data Structure To Facilitate Fast Lookup Of Terms And Clauses In A Logic Program, Deductive Database, Or Automated Theorem Prover.
    Lists: A Number Of Connected Items Or Names Written Or Printed Consecutively, Typically One Below The Other.
    Strings: Data Values That Are Made Up Of Ordered Sequences Of Characters
    Variable: A Data Item That May Take On More Than One Value During The Runtime Of A Program.



```python
#6-5. Rivers: Make a dictionary containing three major rivers and the country each river runs through. One key-value pair might be 'nile': 'egypt'.

#Use a loop to print a sentence about each river, such as The Nile runs through Egypt.
#Use a loop to print the name of each river included in the dictionary.
#Use a loop to print the name of each country included in the dictionary.

rivers = {
    'Nile': 'Egpyt',
    'Mississippi': 'United States',
    'Yangtze': 'China',
    }

for name in sorted(rivers.keys()):
    country = rivers[name].title()
    print(f"{name.title()} runs through {country}.")

for name in sorted(rivers.keys()):
    print(f"{name.title()}")
    
for name in set(rivers.values()):
    print(name.title())
    

```

    Mississippi runs through United States.
    Nile runs through Egpyt.
    Yangtze runs through China.
    Mississippi
    Nile
    Yangtze
    United States
    Egpyt
    China



```python
#6-7. People: Start with the program you wrote for Exercise 6-1 (page 99). 
# Make two new dictionaries representing different people, and store all three dictionaries in a list called people. 
# Loop through your list of people. As you loop through the list, print everything you know about each person.

dictionary1 = {
    'shaps': 'shapiro',
    'zach': 'singer',
    'toshi': 'nagase',
    'samson': 'bienstock',
    }

dictionary2 = {
    'Roman': 'Short',
    'Colin': 'Mclaughlin',
    'Michael': 'Shriver',
    'Ethan': 'Cardi',
    }

dictionary3 = {
    'Shiv': 'Khanna',
    'Ryan': 'Kadet',
    'Liam': 'Campbell',
    'tucker': 'livingstong',
    }

dictionaries = [dictionary1, dictionary2, dictionary3]

for dictionary in dictionaries:
    print(dictionary)
```

    {'shaps': 'shapiro', 'zach': 'singer', 'toshi': 'nagase', 'samson': 'bienstock'}
    {'Roman': 'Short', 'Colin': 'Mclaughlin', 'Michael': 'Shriver', 'Ethan': 'Cardi'}
    {'Shiv': 'Khanna', 'Ryan': 'Kadet', 'Liam': 'Campbell', 'tucker': 'livingstong'}



```python
#6-8. Pets: Make several dictionaries, where each dictionary represents a different pet. 
# In each dictionary, include the kind of animal and the owner’s name. 
# Store these dictionaries in a list called pets. 
# Next, loop through your list and as you do, print everything you know about each pet.

Cat = {
    'Owner': 'matt shapiro',
    'Type': 'bobcat',
    'color': 'blue',
    }

Dog = {
    'Owner': 'roman short',
    'Type': 'poodle',
    'color': 'black',
    }

Dove = {
    'Owner': 'zach singer',
    'Type': 'pigeon',
    'color': 'white',
    }

animals = [Cat, Dog, Dove]
for animal in animals:
    print(animal)
```

    {'Owner': 'matt shapiro', 'Type': 'bobcat', 'color': 'blue'}
    {'Owner': 'roman short', 'Type': 'poodle', 'color': 'black'}
    {'Owner': 'zach singer', 'Type': 'pigeon', 'color': 'white'}



```python
# 6-9. Favorite Places: Make a dictionary called favorite_places. Think of three names to use as keys in the dictionary, and store one to three favorite places for each person. To make this exercise a bit more interesting, ask some friends to name a few of their favorite places. 
#Loop through the dictionary, and print each person’s name and their favorite places.

favorite_places = {
    'Matt Shapiro': ['Philadelphia', 'Japan', 'Texas'],
    'Zach Singer': ['New Jersey', 'New York', 'Seattle'],
    'Samson Bienstock': ['Miami','Montreal','Rome'],
    }

for name, languages in favorite_places.items():
    print(f"\n{name.title()}'s favorite places are:")
    for language in languages:
        print(f"\t{language.title()}")
```

    
    Matt Shapiro's favorite languages are:
    	Philadelphia
    	Japan
    	Texas
    
    Zach Singer's favorite languages are:
    	New Jersey
    	New York
    	Seattle
    
    Samson Bienstock's favorite languages are:
    	Miami
    	Montreal
    	Rome



```python
# 6-11. Cities: Make a dictionary called cities. Use the names of three cities as keys in your dictionary. 
# Create a dictionary of information about each city and include the country that the city is in, 
# its approximate population, and one fact about that city. The keys for each city’s dictionary should be 
# something like country, population, and fact. Print the name of each city and all of the information 
# you have stored about it.

Cities = {
   'Seattle': {
       'Country': 'USA',
       'Population': 800000,
       'Fact': 'I am from here',
       },

   'New Jersey': {
       'Country': 'USA',
       'Population': 300000,
       'Fact': 'Zach is from here',
       },
   'Miami': {
       'Country': 'USA',
       'Population': 500000,
       'Fact': 'Samson is from here',
       },
   }

for username, user_info in Cities.items():
    print(f"\nPlace: {username}")
    full_name = f"{user_info['Country']}, {user_info['Population']}"
    Fact = user_info['Fact']

    print(f"\tCountry and Population: {full_name.title()}")
    print(f"\tFun Fact: {Fact.title()}")
```

    
    Place: Seattle
    	Country and Population: Usa, 800000
    	Fun Fact: I Am From Here
    
    Place: New Jersey
    	Country and Population: Usa, 300000
    	Fun Fact: Zach Is From Here
    
    Place: Miami
    	Country and Population: Usa, 500000
    	Fun Fact: Samson Is From Here



```python

```
