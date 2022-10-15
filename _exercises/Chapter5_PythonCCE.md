---
layout: page
title: Python Crash Course Chapter 5
description: My answers to Chapter 5 Python Crash Course Exercises
---

# Chapter 5

```python
#5.1
a = 20
b = 20
print("Does a = b? I predict true.")
print(a==b)
```

    Does a = b? I predict yes.
    True



```python
b = 1
a = 2
print("Is a>b? I predict true.")
print(a>b)
```

    Is a>b? I predict yes.
    True



```python
b=2
a=1
print("is a>b? I predict false.")
print(a>b)
```

    is a>b? I predict no.
    False



```python
name = 'shaps'
print("\nIs name == 'shaps'? I predict False.")
print(name == 'zach')
```

    
    Is name == 'shaps'? I predict False.
    False



```python
#5.2
# Tests for equality and inequality with strings
title = "The Great Gatsby"
print("Is title == 'The Great Man'? I predict False.")
print(title == 'The Great Man')
```

    Is title == 'The Great Man'? I predict False.
    False



```python
# Tests using the lower() method
title = "The Great Gatsby"
print("Is title.lower() == 'the great gatsby'? I predict True.")
print(title.lower() == 'the great gatsby')
```

    Is title.lower() == 'the great gatsby'? I predict True.
    True



```python
# Numerical tests involving equality and inequality, greater than and less than, greater than or equal to, 
# and less than or equal to
print("Is 100 == 50 + 50? I predict True.")
print(100 == 50 + 50)
print("\n")
print("Is 10 + 7 < 15? I predict False." )
print( 10 + 7 < 15)
print("\n")
print("Is 1 >= 1? I predict True.")
print( 1 >= 1)
```

    Is 100 == 50 + 50? I predict True.
    True
    
    
    Is 10 + 7 < 15? I predict False.
    False
    
    
    Is 1 >= 1? I predict True.
    True



```python
#tests using "and" and "or"
print("Is 10 == 10 and 5 == 5? I predict True.")
print(10 == 10 and 5 == 5)
```

    Is 10 == 10 and 5 == 5? I predict True.
    True



```python
print ("Is 10 == 10 or 5==6? I predict True.")
print (10 == 10 or 5==6)
```

    Is 10 == 10 or 5==6? I predict True.
    True



```python
# Test whether an item is in a list
names = ["Toshi", "Shaps", "Samson", "Zach"]
print("Is 'Shaps' in philosophers? I predict True.")
print("Shaps" in names)
```

    Is 'Shaps' in philosophers? I predict True
    True



```python
# Test whether an item is not in a list
names = ["Toshi", "Shaps", "Samson", "Zach"]
print("Is 'Shaps' not in philosophers? I predict False.")
print("Shaps" not in names)
```

    Is 'Shaps' not in philosophers? I predict False.
    False



```python
#5.6
age = 22
if age < 2:
    print("You are a baby.")
elif age >= 2 and age < 4:
    print("You are a toddler.")
elif age >=4 and age < 13:
    print("You are a kid.")
elif age >= 13 and age < 20:
    print("You are a teenager.")
elif age >=20 and age < 65:
    print("You are an adult.")
else:
    print("You are an elder")
```

    You are an adult.



```python
#5.7
favfruits = ["mango", "strawberry", "blueberry", "rasberry"]

if "apple" in favfruits:
    print("I really like apple")
    
if "blueberry" in favfruits:
    print("I really like blueberry")
    
if "rasberry" in favfruits:
    print("I really like rasberry")
    
if "banana" in favfruits:
    print("I really like banana")
    
if "lychee" in favfruits:
    print("I really like lychee")
```

    I really like blueberry
    I really like rasberry



```python
#5.8
usernames = ['admin', 'topbinz122', 't_nagas', 'ngagposh', 'fakeuser']
for username in usernames:
    if (username == 'admin'):
        print(f"Hello {username}, would you like to see a status report?")
    if (username != 'admin'):
        print(f"Hello {username}, thank you for logging in again.")
```

    Hello admin, would you like to see a status report?
    Hello topbinz122, thank you for logging in again.
    Hello t_nagas, thank you for logging in again.
    Hello ngagposh, thank you for logging in again.
    Hello fakeuser, thank you for logging in again.



```python
#5.9
usernames.clear() #CLEARS LIST
if usernames:
    usernames = ['admin', 'topbinz122', 't_nagas', 'ngagposh', 'fakeuser']
    for username in usernames:
        if (username == 'admin'):
            print(f"Hello {username}, would you like to see a status report?")
        if (username != 'admin'):
            print(f"Hello {username}, thank you for logging in again.")
else:
    print("We need to find some users!")
```

    We need to find some users!



```python
#5.10
# Make a list of five or more usernames called current_users.
current_users = ['admin', 'topbinz122', 't_nagas', 'ngagposh', 'fakeuser']

#Make another list of five usernames called new_users.
# Make sure one or two of the new usernames are also in the current_users list.
new_users = ['topbinz122', 't_nagas', 'chickenbutt', 'notmenotyounotus', 'whydofliesfly']

# Loop through the new_users list to see if each new username has already been used. 
#If it has, print a message that the person will need to enter a new username. 
#If a username has not been used, print a message saying that the username is available.

for username in new_users:
    if username.lower() in current_users:
        print(f"{username} is not available, please choose a new username.")
    else:
        print(f"{username} is available.")
```

    topbinz122 is not available, please choose a new username.
    t_nagas is not available, please choose a new username.
    chickenbutt is available.
    notmenotyounotus is available.
    whydofliesfly is available.



```python

```
