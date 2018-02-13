---
layout: post
title: STRING MANIPULATION, GUESS-and-CHECK, APPOXIMATEIONS, BISECTION
date: 2018-02-13
categories: blog
tags: [MIT, Python]
description: MIT Open Course of Python
---

## TODAY
------
* string manipulation 
* guess and check algorithms
* approximate solutions
* bisection method

## STRINGS
------
* think of as a **sequence** of case sensitive characters
* can compare strings with `==`, `>`, `<` etc.
* `len()` is a function used to retrieve the **length** of string in the parentheses

```python
s = "abc"
len(s) # -> evaluates to 3
```

------
* squere brackets used to perform **indexing** into a string to get the value at a certain index/position

```python
s = "abc"
# index :  0  1  2 <- index always starts at 0
# index : -3 -2 -1 <- last element always at index = -1
```

------
* can **slice** strings using `[start:stop:step]`
* if give two numbers, `[start:stop], step = 1` by default
* you can also omit numbers and leave just colons

```python
s = "abcdefgh"
s[3:6]		# -> evaluates to "def", same as s[3:6:1]
s[3:6:2] 	# -> evaluates to "df"
s[::]		# -> evaluates to "abcdefgh", same as s[0:len(s):1]
s[::-1]		# -> evaluates to "hgfedbca", same as s[-1:-(len(s)+1):-1]
s[4:1:-2]	# -> evaluates to "ec"
```

------
* stirngs are **immutable** - cannot be modified

```python
s = "hello"
s[0] = 'y'		# -> given an error
s = 'y' + s[1:len(s)]	# -> is allowed, s bound to new object
```

## for LOOPS RECAP
------
* `for` loops have a **loop variable** that iterates over a set of values

```python
for var in range(4):		# -> `var` iterates over values 0,1,2,3
    <expressions>		# expressions inside loop executed with each value for var

for var in range(4,6):		# -> `var` iterates over values 4, 5
    <expressions>
```

* `range` is a way to iterate over numbers, but a for loop variable can **iterate over any set of values**, not just numbers!

## STRINGS AND LOOPS
------
* these two code snippets do the same thing
* bottom one is more "pythonic"

```python
s = "abcdefgh"
for index in range(len(s)):
    if s[index] == 'i' or s[index] == 'u':
	print("There is an i or u")

for char in s:
    if char == 'i' or char == 'u':
	print("There is an i or u")
```


