---
layout: post
title: Linux Netword Manager Command: nmcli
date: 2017-09-08
categories: blog
tags: [linux command: nmcli]
description: Linux, Network Manager, nmcli 
---

##使用NETOWORK MANAGER命令行工具 nmcli

用户和脚本都可使用命令行工具 **nmcli** 控制 **NetworkManager**。该命令的基本格式为：
```
nmcli OPTIIONS OBJECT { COMMAND | help }
```

其中 **OBJECT** 可为 ```general```、```networking```、 ```radio```、 ```connection```或 ``` device ```之一。

最常用的选项为： ```-t ```, ```--terse```(用于脚本)、 ```-p```, ```--pretty```选项（用于用户）及 ```-h```, ```--help```选项。

在**nmcli**中采用命令完成功能，无论何时您不确定可用的命令选项时，都可以按**tab**查看。

**nmcli**工具有一些内置的上下文相关的帮助信息。例如：运行以下命令，并注意不同之处：
