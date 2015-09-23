# Python Objects

* Python has numerous data types, including:
    * Numbers
        * Integers, or int
        * Floating point numbers for decimals, or float
    * Text
        * Strings of characters, or str
    * Collections
        * Ordered collections, or list
        * Key-value collection pairs, or dict

## Numbers

### Int

> Integers, or int, are non-decimal numbers, which can be assigned to variables.

```python
>>> a = 1
>>> print(a)
1
```

### Float

> Floating point numbers, or float, are numbers that can represent decimals.

```python
>>> a = float(1)
>>> print(a)
1.0
>>> b = 1.0
>>> print(b)
1.0
```

## Text

### String

> Although numbers get us very far with purely mathematical data, for biological data and more abstract applications, we need ways to represent and hold text. Strings, or str, are quotation-enclosed characters to represent text.

```python
>>> a = ""
>>> print(a)

>>> b = "How was lunch? Did you eat well?"
>>> print(b)
How was lunch? Did you eat well?
```

## Collections

### List

> Lists are a versatile way to store ordered, diverse data for access later. Using a list is much more readable, and generalizable than using a separate variable for each element. Single elements can be accessed by their position in the list, or multiple items can be selected with a slice.

```python
>>> a = []
>>> print(a)
[]
>>> b = [1, 2, "Lunch", 3.5, 8]
>>> print(b)
[1, 2, "Lunch", 3.5, 8]
>>> b[1]
2
>>> b[1:3]
[2, "lunch"]
```

### Dictionary

> Dictionaries, or dict, are key-to-value pairs, like a treasure chest with only a given treasure for each key.

```python
>>> a = {}
>>> print(a)
{}
>>> b = {3: 5, 4: 6}
>>> print(b)
{3: 5, 4: 6}
>>> b[3]
5
```
