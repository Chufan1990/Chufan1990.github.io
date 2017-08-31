---
layout: post
title: STL tips
date: 2015-3-02
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
$ vec.pop_back();
```

3. Define iterator

```
$ vector<T>::iterator;
```

4. Traversal

```
$ vector<T> vec;
$ vector<T>::iterator itor = vec.begin();
$ for( ; itor != vec.end();itor ++)
$ {
$ 	cout << * itor << endl;
$ };
```

- Similar to:
```
$ vector<T> vec;
$ for ( i = 0; i < vec.size(); i ++)
$ {
$ 	cout << vec[i] << endl;
$ };
...



