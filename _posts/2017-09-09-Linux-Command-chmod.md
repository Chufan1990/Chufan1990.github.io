---
layout: post
title: Linux Command chmod
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

|**-c**, **-****-changes** | Lke **-****-verbose**, but gives verbose output only when a change is actually made.|
|**-f**, **-****-silent**, **-****-quiet** | Quiet mode; suppress most error message. |
|**-v**, **-****-verbose** | Verbose mode;output a diagnostic message for every file processed.
|**-****-no-preserve-root** | Do not treat ‘**/**’ (the root directory) in any special way, which is the default setting. |
|**-****-reference=***RFILE* | Set permissions to match those of file *RFILE*, ignoring any specified *MODE* | 
|**-R**, **-****-recursive** | Change files and directories recursively. |
|**-****-help** | Display a help message and exit. |
|**-****-version** | Output version information and exit. |

## Technical Description

**chmod** changes the file mode of each specified *FILE* according to *MODE*, which can be either a symbolic representation of changes to make, or an octal number representing the bit pattern for the new mode bits.

The format of symbolic mode is:

> [**ugoa**...][[+-=][*perms*...]...]

where *perms* is either zero or more letters from the set **r**, **w**, **x**, **X**, **s** and **t**, or a single letter from the set **u**, **g**, and **o**. Multiple symbolic modes can be given, separated by commas.

A combination of the letters **u**, **g**, **o**, and **a** controls which users' access to the file will be changed; the user who owns it (**u**), other users in the file's group (**g**), other users not in the file's group(**o**), or all users (**a**). If none of these are given, the effect is as if **a** were given, but bits that are set in the umask are not affected.

The operator **+** causes the selected file mode bits to be added to the existing file mode bits of each file; **-** causes them to removed except that a directory's unmentioned set user and group ID bits are not affected.

The letters **r**, **w**, **x**, **X**, **s** and **t** select file mode bits for the affected users: read(**r**), write(**w**), execute(**x**), execute only if the file is a directory or already has execute permission for some user(**X**), set user or group ID on execution(**s**), restricted deletion flag or sticky bit(**t**). For directories, the execute option **x** and **X** define permission to view the directory's contents.

Instead of one or more of these letters, you can specify exactly one of the letters **u**, **g**, or **o**: the permissions granted to the user who owns the file(**u**), the permission granted to other users who are members of the file's group(**g**), and the permissions granted to users that are in neither of the two preceding categories(**o**).

A numeric mode is from one to four octal digits(**0**-**7**), derived by adding up the bits with value **4**, **2**, and **1**. Omitted digits are assumed to be leading zeros. The first digit selects the set user ID (**4**) and set goup ID(**2**) are restriced deletion or sticky (**1**) attributes. The seconde digit selects permissions for the user who owns the read (**4**), write (**2**), and execute (**1**); the third selects permissions for other users in the file's group, with the same values; and the forth for the other users not in the file's group, with the same values.

**chmod** never changes the permissions of symbolic links; the **chmod** system call cannot change their permissions. However, this is not a problem since the permission of symbolic links are never used. However, for each symbolic link listed on the command line, **chmod** changes the permissions of the pointed-to file. In contrast, **chmod** ignores symbolic links encountered during recursive directory traversals.
