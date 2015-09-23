# Conditions and Loops

* Execute code only upon a condition
    * if condition, do something
* Can continue to execute code while a condition is true
    * while condition, do something
* Can execute code for a predetermined length
    * for item in sequence

## If/Else Conditions

* Simple code execution upon satisfying a condition
* Can include test conditions if the first condition fails using elif, short for "else if"
* Can execute code if no condition satisfied (else)

```python
>>> if True:
...     print(1)
1
>>> if False:
...     print(1)
... elif True:
...     print(2)
2
>>> if False:
...     print(1)
... elif False:
...     print(2)
... else:
...     print(3)
3
```

## While Loops

* Executes code until condition is false

```python
>>> number = 4
>>> while number:
...     print(number)
...     number -= 1
4
3
2
1
```

## Loops of predetermined length

* Executes code for each item in a given collection
* Can make collections based on the length of a collection
* Strings act like ordered collections too, can be part of a for loop

```python
>>> numbers = [1, 3, 2, 4]
>>> for value in range(number):
...     print(value)
1
3
2
4
>>> for value in range(len(number)):
...     print(value)
0
1
2
3
>>> for character in "lunch":
...     print(character)
l
u
n
c
h
```
