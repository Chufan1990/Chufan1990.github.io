---
layout: post
title: Solve MATLAB issue Unable To Initialize The Video Obtian Properties
date: 2017-09-25
categories: blog
tags: [Linux, MATLAB, VideoReader, unable to initialize]
description: How to solve MATLAB R2017a linux VideoReader unable to initialize issue. 
---

## Cannot read video MATLAB R2017a Linux!!

```
"could not read file due to an unexpected error. Reason: Unable to initialize the video obtian properties"

Error in VideoReader (line 172)
		obj.init(filename);
```

Newer version of some *gstreamer* plugins require a later version of *libstdc++* than the one which is shipped with **MATLAB**

As a workaround you can run MATLAB on the version of *libstdc++* installed on your system:

1. Change directory to the `glnxa64` folder under your **MATLAB** 
```
$ cd YOUR_MATLAB_DIRECTORY/sys/os/glnxa64/
``` 

2. Rename *libstdc++.so.6* to *backuplibstdc++.so.6*
```
$ mv libstdc++.so.6 backuplibstdc++.so.6
```

3. Rename *libstdc++.so.6.0.xx* to *backuplibstdc++.so.6.0.xx*
```
$ mv libstdc++.so.6.0.xx backuplibstdc++.so.6.0.xx
```

4. Restart *MATLAB* and execute the code again
