# Basics

## Data structures
### Lists
Simple lists:
```python
animals = ["cat", "dog", "chicken", "pig", "sheep"]

# Access to the list with index
print(animals[0])  # cat
print(animals[1])  # dog
print(animals[-1])  # Prints the last item (sheep)
print(animals[-2])  # Prints the second to last item (pig)
```

List of lists:
```python
random_list = [[0, 1, 5, 8, 6],
				[4, 5, 6, 1],
				[4, 8, 7, 7, 5, 1, 3, 5]]

# Access to the list with index of list and index of value
print(random_list[1][1])  # 5
```

### Tuples
Unlike other data structures, tuples cannot be modified.
```python
tuple = (2, 5, 5)
tuple2 = ("One", "Two", "Three", "Four")
```

### Dictionnaries
```python
dictionnary = {"Belgium":"Brussels", "France":"Paris", "Portugal":"Lisbonne"}
print(dictionnary["Belgium"])  # Brussels
print(dictionnary["Brussels"])  # Key error
print(dictionnary[0])  # Key error
```


## Conditionals
### if/else
```python
if (var > 10):
	print("Greater than 10")
elif (var < 10):
	print("Lower than 10")
else:
	print("Equals 10")
```


## Loops
### While
```python
while (condition == True):
	# Do something that might change condition
```

### For
To iterate through a data structure or a file:
```python
for i in list:
	print(i)
```

To iterate a certain number of times (from 0 to 10):
```python
for i in range(0,10):
	print(i)
```


## Logical operators
### OR (or)
```python
if (False or True):
	print("This is true!")
```

### AND (and)
```python
if (False and True):
	print("This is false!")
```

## Modules
To add external modules or methods to python:
```python
import time  # time.sleep(2)
import time as t  # t.sleep(2)
from time import sleep  # sleep(2)
from time import sleep as s  # s(2)
```

To add other python files to the project:
If mylib is in the same directory:
```python
import mylib  # mylib.mymethod()
from mylib import mymethod  # mymethod()
```

If mylib is in another directory (./directory/):
```python
import directory.mylib  # directory.mylib.mymethod()
from directory import mylib  # mylib.mymethod()
```

