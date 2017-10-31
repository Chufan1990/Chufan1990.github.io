---
layout: post
title: Make 命令
date: 2017-09-25
categories: blog
tags: [Linux, Make]
description: Make命令
---

## 1. Make的概念

**Make**顾名思义就是要做出某个文件。例如要做出 `a.txt`
```
$ make a.txt
```
如果我们执行这条命令，并不会起作用，因为**Make**命令还不知道要如何制作`a.txt`，需要告诉它如何调用其他命令完成这个目标。
比如，假设`a.txt`依赖于`b.txt`和`c.txt`，是后面两个文件链接（**cat**命令）的产物。那么**Make**需要知道下面的规则：
```
a.txt: b.txt c.txt
	cat b.txt c.txt > a.txt
```
也就是说，`make a.txt`这条命令的背后，实际上分成两步：第一步，确认`b.txt`和`c.txt`必须已经存在；第二部，使用`cat`命令将这两个文件合并，输出新的文件。

像这个样的规则，都写在一个叫**Makefile**的文件中，`make`命令依赖于这个文件进行构建。**Makefile**文件也可以写成`makefile`，或者用命令行参数指定为其他文件名。
```
$ make -f rules.txt
# or
$ make --file= rules.txt
```

## 2. Makefile文件的格式
构建规则都写在**Makefile**文件里面，要学会如何使用**Make**命令，就必须学会如何编写**Makefile**文件。

### 2.1 概述
**Makefile**文件由一系列规则（*rules*）构成。每条规则的形式如下
```
<target> : <prerequisites>
[tab]	<commands>
```
上面第一行冒号前面的部分叫做**目标**（*target*），冒号后面的部分叫做**前置条件**（*prerequisities*）;第二行必须有一个`tab`键起首，后面跟着**命令**（*commands*）。

**目标**是必须的，不可省略。**前置条件**和**命令**都是可选的，但是两者之中必须至少存在一个。

每条规则就明确两件事：构成**目标**的**前置条件**是什么，以及如何构建。

## 2.2 目标（target）
一个**目标**
