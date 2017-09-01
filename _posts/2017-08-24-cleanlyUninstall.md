---
layout: post
title: Uninstall packages cleanly
date: 2017-08-24
categories: blog
tags: [Ubuntu, Uninstall]
description: Following the steps  to uninstall packages cleanly
---
 How to fix the issure that being stuck in a login loop after uninstallation with command 
``` sudo apt-get remove _YOUR-PACKAGE-NAME_```

## A) Fix the boot loop first: 
> (if there is a login loop issure: after typing password the screen goes back and then redirects user back to the unity login page)
> 

1. at login screen type ```Ctrl``` + ```Alt``` + ```F1``` ( or ```F2``` .. ```F6```)

2. Enter a terminal in full black screen. From there install ```YOUR-PACKAGE-NAME``` AGAIN by
```
sudo apt-get install YOUR_PACKAGE_NAME
```
3. Go back to the normal login screen and now log in into your account

## B) Uninstall PACKAGE cleanly:

1. Refer to [this manual](http://codepub.cn/2015r/11/27/Ubuntu14-10-install-and-uninstall-sogou-input-method/) with Google translator

2. Open terminal again and you only need following commands:

```
sudo dpkg -l intial_letter_of_your_package* (like sogoupinyin you should type in so* here)

sudo apt-get purge package_name_from_the_list
 
sudo apt-get autoremove
```

3. Restart your computer
