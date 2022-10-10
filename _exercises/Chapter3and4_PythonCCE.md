---
layout: page
title: Python Crash Course Chapter 3 and 4
description: My answers to Chapter 3 and 4 Python Crash Course Exercises
---

# Chapter 3


```python
##3.1
friends = ["Samson", "Zach", "Shaps"]
print(friends[0])
print(friends[1])
print(friends[2])
```

    Samson
    Zach
    Shaps



```python
#3.2
friends = ["Samson", "Zach", "Shaps"]
print(f"Why do you smell funny {friends[0]}?")
print(f"Hi {friends[1]}! We should get some food.")
print(f"Peace out {friends[2]}!")
```

    Why do you smell funny Samson?
    Hi Zach! We should get some food.
    Peace out Shaps!



```python
#3.3
vehicles = ["boat", "plane", "scooter"]
print(f"I love going home on the {vehicles[0]}.")
print(f"I think {vehicles[1]} is the best way to move fast.")
print(f"I like riding the {vehicles[2]}.")
```

    I love going home on the boat.
    I think plane is the best way to move fast.
    I like riding the scooter.



```python
#3.4
guests = ['albert einstein', 'barack obama', 'alexander the great']
print(f"Yo {guests[0].title()}, come to my dinner.")
print(f"Yo {guests[1].title()}, come to my dinner.")
print(f"Yo {guests[2].title()}, come to my dinner.")
```

    Yo Albert Einstein, come to my dinner
    Yo Barack Obama, come to my dinner
    Yo Alexander The Great, come to my dinner



```python
#3.5
guests = ['albert einstein', 'barack obama', 'alexander the great']
print(f"Yo {guests[0].title()}, come to my dinner.")
print(f"Yo {guests[1].title()}, come to my dinner.")
print(f"Yo {guests[2].title()}, come to my dinner.")

busyGuest = guests.pop()
print(f"{busyGuest.title()} is too busy to come to dinner.")

newGuest = 'yoyo nagase'
guests.append(newGuest)
print(f"Yo {guests[0].title()}, come to my dinner.")
print(f"Yo {guests[1].title()}, come to my dinner.")
print(f"Yo {guests[2].title()}, come to my dinner.")
```

    Yo Albert Einstein, come to my dinner.
    Yo Barack Obama, come to my dinner.
    Yo Alexander The Great, come to my dinner.
    Alexander The Great is too busy to come to dinner.
    Yo Albert Einstein, come to my dinner.
    Yo Barack Obama, come to my dinner.
    Yo Yoyo Nagase, come to my dinner.



```python
#3.6
guests = ['albert einstein', 'barack obama', 'alexander the great']
print(f"Yo {guests[0].title()}, come to my dinner.")
print(f"Yo {guests[1].title()}, come to my dinner.")
print(f"Yo {guests[2].title()}, come to my dinner.")

print("I have a bigger table so I can invite more guests!")

guests.insert(0, "homer")
guests.insert(2, "joe biden")
guests.append("russel wilson")

#could use for loop
print(f"Yo {guests[0].title()}, come to my dinner.")
print(f"Yo {guests[1].title()}, come to my dinner.")
print(f"Yo {guests[2].title()}, come to my dinner.")
print(f"Yo {guests[3].title()}, come to my dinner.")
print(f"Yo {guests[4].title()}, come to my dinner.")
print(f"Yo {guests[5].title()}, come to my dinner.")
```

    Yo Albert Einstein, come to my dinner.
    Yo Barack Obama, come to my dinner.
    Yo Alexander The Great, come to my dinner.
    I have a bigger table so I can invite more guests!
    Yo Homer, come to my dinner.
    Yo Albert Einstein, come to my dinner.
    Yo Joe Biden, come to my dinner.
    Yo Barack Obama, come to my dinner.
    Yo Alexander The Great, come to my dinner.
    Yo Russel Wilson, come to my dinner.



```python
#3.7
guests = ['albert einstein', 'barack obama', 'alexander the great', 'homer', 'joe biden', 'russel wilson']

print("Sorry, it turns out I can only invite two people to dinner")

print((f"Yo {guests[-1].title()}, sorry you cant come."))
guests.pop()

print((f"Yo {guests[-1].title()}, sorry you cant come."))
guests.pop()

print((f"Yo {guests[-1].title()}, sorry you cant come."))
guests.pop()

print((f"Yo {guests[-1].title()}, sorry you cant come."))
guests.pop()

print(f"Hello {guests[0]}, you can come.")
print(f"Hello {guests[1]}, you can come.")

del guests[0]
del guests[0]
print(guests)
```

    Sorry, it turns out I can only invite two people to dinner
    Yo Russel Wilson, sorry you cant come.
    Yo Joe Biden, sorry you cant come.
    Yo Homer, sorry you cant come.
    Yo Alexander The Great, sorry you cant come.
    Hello albert einstein, you can come.
    Hello barack obama, you can come.
    []



```python
#3.8
vacations = ["Rome", "China", "Egypt", "Athens", "Mexico"]
print(vacations)
print(sorted(vacations))
print(vacations)

vacations.reverse()
print(vacations)

vacations.reverse()
print(vacations)

vacations.sort()
print(vacations)

vacations.sort(reverse=True)
print(vacations)
```

    ['Rome', 'China', 'Egypt', 'Athens', 'Mexico']
    ['Athens', 'China', 'Egypt', 'Mexico', 'Rome']
    ['Rome', 'China', 'Egypt', 'Athens', 'Mexico']
    ['Mexico', 'Athens', 'Egypt', 'China', 'Rome']
    ['Rome', 'China', 'Egypt', 'Athens', 'Mexico']
    ['Athens', 'China', 'Egypt', 'Mexico', 'Rome']
    ['Rome', 'Mexico', 'Egypt', 'China', 'Athens']


## Chapter 4


```python
##4.1
pizzas = ["sausage", "chicken", "olive"]
for pizza in pizzas:
    print(pizza)
for pizza in pizzas:
    print(f"I like {pizza} pizza.")
for pizza in pizzas:
    print(f"I like {pizza} pizza.")
print("I really love pizza!")
```

    sausage
    chicken
    olive
    I like sausage pizza.
    I like chicken pizza.
    I like olive pizza.
    I like sausage pizza.
    I like chicken pizza.
    I like olive pizza.
    I really love pizza!



```python
##4.2
animals = ["chicken", "dove", "penguin"]
for animal in animals:
    print(animal)
```

    chicken
    dove
    penguin



```python
for animal in animals:
    print(f"{animal} is a bird.")
```

    chicken is a bird.
    dove is a bird.
    penguin is a bird.



```python
for animal in animals:
    print(f"{animal} is a bird.")
print("These are all birds")
```

    chicken is a bird.
    dove is a bird.
    penguin is a bird.
    These are all birds



```python
##4.3
for num in range(1,21):
    print(num)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20



```python
##4.6
for num in range(1, 21, 2):
    print(num)
```

    1
    3
    5
    7
    9
    11
    13
    15
    17
    19



```python
##4.10
animals = ["dove", "rooster", "chicken", "goose", "duck", "ostrich", "blue jay", "raven", "pigeon"]
print("The first three animals in the list are:")
for animal in animals[0:3]:
    print("\t" + animal)
    
print("Three animals from the middle of the list are:")
for animal in animals[3:6]:
    print("\t" + animal)
    
print("The last three animals in the list are:")
for animal in animals[6:9]:
    print("\t" + animal)
```

    The first three animals in the list are:
    	dove
    	rooster
    	chicken
    Three animals from the middle of the list are:
    	goose
    	duck
    	ostrich
    The last three animals in the list are:
    	blue jay
    	raven
    	pigeon



```python
##4.11
pizzas = ["sausage", "chicken", "olive"]
friend_pizzas = pizzas[:]
pizzas.append("basil")
friend_pizzas.append("ricotta")
```


```python
print("My pizzas are")
for pizza in pizzas:
    print("\t" + pizza)
    
print("My friend's pizzas are")
for pizza in friend_pizzas:
    print("\t" + pizza)
```

    My pizzas are
    	sausage
    	chicken
    	olive
    	basil
    My friend's pizzas are
    	sausage
    	chicken
    	olive
    	ricotta



```python

```