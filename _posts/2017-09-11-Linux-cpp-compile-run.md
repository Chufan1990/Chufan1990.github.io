---
layout: post
title: How to Compile and Run C/C++ program on Ubuntu
date: 2017-09-11
categories: blog
tags: [Linux, C++，Cpp, How to compile, How to run]
description: 
---

## Write and save the program

**C/C++** in **Ubuntu**

Open a simple text editor (e.g **gedit**), IDE ( **Eclipse**) or command line code editor (**Nano** or **Vim**). I'll be using gedit as it is very simple to use and it's recommended for beginner programmers. Right Click on Desktop or any directory (Browse File using **Nautilus**) and select create new File - *hello.c*/*hello.cpp* (*.c* extension is used to indicate that it's *C* program and *.cpp* means *C++*). Then write a simple program like this (and save the program press *Ctrl*+*C*).

```
// C++ program

#include <iostream>

int main()
{
	std::cout << "Hello! This is my first C++ program with Ubuntu!" <<endl;

	// Do something more if you want

	return 0;
}
```
```
// C program

#include <stdio.h>

int main()
{
	printf("Hello! This is my first C program with Ubuntu \n");

	// Do something more if you want

	return 0;
}
```

## Compile the program

**GCC**(*GNU Compiler Collection*) is installed by default in **Ubuntu**. To compile the program, open the terminal and move on to the target directory type the command - (where `gcc` implies complier name, then it asks for the file name of source program while `-o` option specifies the file name of the output program).
```
$ gcc hello.c -o hello1
```

if there is no syntax/semantic error in your program then the compiler will sucessfully generate an execute file, otherwise fix the program in your code.

## Execute the program

To execute the program, you need to run
```
./hello1
```
running a **C** program in **Ubuntu**.

### Compiling and Executing C++ program

The steps are almost same as abve but you need to install *g++* compiler, the file extenstion should be *.cpp* and in compilation phase replace *gcc* with *g++*. To install **G++** compiler, execute the command:
```
$ sudo apt-get install g++
```
