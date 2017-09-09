---
layout: post
title: Linux Command *chmod*
date: 2017-09-09
categories: blog
tags: [Linux, command line, chmod]
description: Change permissions of files or directories.
---

## About chmod

**chmod** is used to change the *permission* of *files* or *directories*.

## Overview

On *Linux* and other *Unix*-like *operating systems*, there is a set of rules for each file which defines who can access that file, and how they can access it. These rules are called file *permissions* or file *modes*. The command name **chmod** stands for "change mode", and it is used to define the way a file can be accessed.

Before continuing, you should read the section [What Are Files Permissions, And How Do They Work?](https://www.computerhope.com/unix/uumask.htm#filepermissions) in our documentation of [umask](https://www.computerhope.com/unix/uumask.htm) command. It contains a comprehensive description of how to define and express file permissions.

In general,**chmod** commands takes the form:
```
chomd options permissions file name
```

If no *options* are specified, **chmod** modifies the permissions of the file specified by *file name* to the permissions specified by *permissions*.

*permissions* defines the permissions for the owner of the file (the "user"), members of the group who owns the file (the "group"), and anyone else ("others"). There are two ways to represent these permissions: with symbols (alphanumeric characters), or with octal numbers (the digit **0** through **7**).

Let's say you are the owner of a file named **myfile**, and you want to set its permissions so that:

1. the **u**ser can **r**ead, **w**rite, and e**x**ecute it;

2. members of your **g**roup can **r**ead and e**x**ecute it; and

3. **o**thers may only **r**ead it.

This command will do the trick
```
chmod u=rwx,g=rx,o=r myfile
```

This example uses symbolic permissions notation. The letters **u**, **g** and **o** stand for "**user**", "**group**", and "**others**". The equals sign ("**=**") means "set the permissions exactly like this", and the letter "**r**","**w**", and "**x**" stand for "read", "write", and "execute", respectively. The commas separate the different classes of permissions, and there are no space in between them.

Here is the equivalent command using octal permissions notation:
```
chmod 754 myfile
```

Here the digits **7**, **5**, and **4** each individually represent the permissions for the user, group, and others, in that order.Each digit is a combination of the numbers **4**, **2**, **1** and **0**.

- **4** stands for "read"

- **2** stands for "write"

- **1** stands for "execute", and

- **0** stands for "no permission".

So **7** is the combination of permissions **4**+**2**+**1** (read, write, and execute), **5** is **4**+**0**+**1** (read, no write, and execute), and **4** is **4**+**0**+**0** (read, no write, and no execute).


## chmod syntax
```
chmod [OPTION]... MODE[,MODE]... FILE...

chmod [OPTION]... OCTAL-MODE FILE...

chmod [OPTION]... --reference=RFILE FILE...
```

## Options

|**-c**, **--changes** | Lke **--verbose**, but gives verbose output only when a change is actually made.|
|**-f**, **--silent**, **--quiet** | Quiet mode; suppress most error message. |
|**-v**, **--verbose** | Verbose mode;output a diagnostic message for every file processed.
|**--no-preserve-root** | Do not treat ‘/’ (the root directory) in any special way, which is the default setting. |
|**--reference=RFILE** | Set permissions to match those of file *RFILE*, ignoring any specified *MODE* | 
|**-R**, **--recursive** | Change files and directories recursively. |
|**--help** | Display a help message and exit. |
|**--version** | Output version information and exit. |


