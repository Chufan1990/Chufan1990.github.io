---
layout: post
title: STRING MANIPULATION, GUESS-and-CHECK, APPOXIMATEIONS, BISECTION
date: 2018-02-13
categories: blog
tags: [MIT, Python]
description: MIT Open Course of Python
---

## TODAY
~~~
* string manipulation 
* guess and check algorithms
* approximate solutions
* bisection method

## STRINGS
~~~
* think of as a **sequence** of case sensitive characters
* can compare strings with `==`, `>`, `<` etc.
* `len()` is a function used to retrieve the **length** of string in the parentheses

```python
s = "abc"
len(s) # -> evaluates to 3
```
~~~
* squere brackets used to perform **indexing** into a string to get the value at a certain index/position

```python
s = "abc"
# index : 0   1  2 <- index always starts at 0
# index : -3 -2 -1 <- last element always at index = -1
```
~~~
* can **slice** strings using `[start:stop:step]`
* if give two numbers, `[start:stop], step = 1` by default
* you can also omit numbers and leave just colons
