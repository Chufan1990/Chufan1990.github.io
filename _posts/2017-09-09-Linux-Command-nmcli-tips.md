---
layout: post
title: Linux NetwordManager: nmcli 
date: 2017-09-08
categories: blog
tags: [linux command: nmcli]
description: Linux, Network Manager, nmcli 

---

## 使用NETOWORK MANAGER命令行工具 nmcli

用户和脚本都可使用命令行工具 **nmcli** 控制 **NetworkManager**。该命令的基本格式为：
```
nmcli OPTIIONS OBJECT { COMMAND | help }
```

其中 **OBJECT** 可为 ```general```、```networking```、 ```radio```、 ```connection```或 ``` device ```之一。

最常用的选项为： ```-t ```, ```--terse```(用于脚本)、 ```-p```, ```--pretty```选项（用于用户）及 ```-h```, ```--help```选项。

在**nmcli**中采用命令完成功能，无论何时您不确定可用的命令选项时，都可以按**tab**查看。

**nmcli**工具有一些内置的上下文相关的帮助信息。例如：运行以下命令，并注意不同之处：

```
~]$ nmcli help
Usage: nmcli [OPTIONS] OBJECT { COMMAND | help }

OPTIONS
  -t[erse]                                   terse output
  -p[retty]                                  pretty output
  -m[ode] tabular|multiline                  output mode
  -f[ields] <field1,field2,...>|all|common   specify fields to output
  -e[scape] yes|no                           escape columns separators in values
  -n[ocheck]                                 don't check nmcli and NetworkManager versions
  -a[sk]                                     ask for missing parameters
  -w[ait] <seconds>                          set timeout waiting for finishing operations
  -v[ersion]                                 show program version
  -h[elp]                                    print this help

OBJECT
  g[eneral]       NetworkManager's general status and operations
  n[etworking]    overall networking control
  r[adio]         NetworkManager radio switches
  c[onnection]    NetworkManager's connections
  d[evice]        devices managed by NetworkManager
```

```
~]$ nmcli general help
Usage: nmcli general { COMMAND | help }

  COMMAND := { status | hostname | permissions | logging }

  status

  hostname [<hostname>]

  permissions

  logging [level <log level>] [domains <log domains>]
```

在上面的第二个示例中，这个帮助信息与对象```general```有关。

显示**NetworkManager**总体状态：
```
nmcli general status
```

要控制**NetworkManager**日志记录：
```
nmcli general logging
```

要显示所有连接：
```
nmcli connection show
```

要只显示当前活动链接，如下所示添加 ```-a```, ```--active```：
```
nmcli connection show --active
```

显示由**NetworkManager**识别到设备及其状态：
```
nmcli device status
```

可简化命令并省略一些选项。例如：可将命令
```
nmcli connection modify id 'MyCafe' 802-11-wireless.mtu 1350
```
简化为
```
nmcli con mod MyCafe 802-11-wireless.mtu 1350
```

可省略```id```选项，因为在这种情况下对于**nmcli**来说连接ID（名称）是明确的。熟悉这些命令后可做进一步简化。例如：可将
```
nmcli connection add type ethernet
```
改为
```
nmcli c a type eth
```

> 
> **注意**
> 如有疑问，请使用```tab```完成功能。
> 

## 使用nmcli启动和停止接口

可使用**nmcli**工具启动和停止任意网络接口，其中包括主接口。例如：

```
nmcli con up id bond0
nmcli con up id port0
nmcli dev disconnect iface bond0
nmcli dev disconnect iface ens3
```

> 
> **注意**
> 建议使用```nmcli dev disconnet iface iface-name```命令，而不是 ```nmcli con down id id-string```命令，因为连接断开可将放到“手动”模式，这样做用户让**NetworkManager**启动某个连接前，或发生外部事件（比如载波变化、休眠或睡眠）前，不会启动任何自动连接。
> 

## nmcli互动连接编辑器

**nmcli**工具有一个互动连接编辑器。请运行以下命令使用该工具：
```
~]$ nmcli con edit
```

此时会提示从显示的列表中选择有效连接类型。输入连接类型后，就会显示**nmcli**提示符。如果熟悉连接类型，也可以在```nmcli con edit```命令中添加```type```选项，从而直接进入提示符。编辑现有连接配置的格式如下：
```
nmcli con edit [id | uuid | path] ID
```

要添加和编辑新连接配置，请采用以下格式：

```
nmcli con edit [type new-connection-type] [con-name new-connection-name]
```

在**nmcli**提示符后输入```help```查看可用命令列表。使用```describe```命令获取设置及其属性描述，格式如下：
```
describe setting.property
```

例如：
```
nmcli> describe team.config
```

## 了解nmcli选项

很多**nmcli**命令是可以顾名思义的，但有几个选项需要进一步了解：

**type-**连接类型。

允许值为：```adsl```, ```bone```, ```bond-slave```, ```bridge```, ```bridge-slave```, ```bluetooth```, ```cdma```, ```ethernet```, ```gms```, ```infiniband```, ```olpc-mesh```, ```team```, ```team-slave```, ```vlan```, ```wifi```, ```wimax```.

每个连接类型都有具体类型的命令选项。按**tab**建查看该列表。```type```选项可用与如下命令：```nmcli connection add```和```nmcli connection edit```。

**con-name-**为连接配置分配的名称。

如果未指定连接名称，则会以如下格式生成名称：
```
type-ifname[-number]
```

连接名称是```connection profile```的名称，不应与代表某个设备的名称混淆（比如 wlan0, ens3, em1 等等）。虽然用户可根据接口为连接命名，但这是两回事。
