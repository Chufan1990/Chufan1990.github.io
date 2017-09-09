---
layout: post
title: STL tips
date: 2017-08-23
categories: blog
tags: [STL]
description: vector, list, map 
---

## 1. vector

vector template contains functions like push_back(), pop_back(), size(), begin(), end(), front(), back().

1. First we define a vector:

```
$ vector<T> vec;
```

2. Add or delete element:

```
$ vec.push_back(1);
$ vec.push_back(3);
$ vec.push_back(5);
$ vec.push_back(1);
$ vec.pop_back();
```

3. Define iterator

```
$ vector<int>::iterator;
```

4. Traversal

```
$ vector<int> vec;
$ vector<int>::iterator itor = vec.begin();
$ for( ; itor != vec.end();itor ++)
$ {
$ 	cout << * itor << endl;
$ };
```

> Similar to:

```
$ vector<T> vec;
$ for ( i = 0; i < vec.size(); i ++)
$ {
$ 	cout << vec[i] << endl;
$ };
```

## 2. list

list contains all functions vector. Traversal, however, can only be executed with iterator.

1. Define a list

```
$ list<int> l;
$ l.push_back(1);
$ l.push_back(3);
$ l.push_back(5);
$ l.push_back(1);
$ l.pop_back();
```

2. Traversal

```
$ list<int>::iterator itor = l.begin();
$ for ( ; itor != l.end(); itor++)
$ {
$	cout << *itor << endl;
$ };
```

> compile error:

```
$ for( i = 0; i < l.size(); i++)
$ {
$	cout << list[i] <<endl; \\encounter some error here
$ };
```

## 3. map


