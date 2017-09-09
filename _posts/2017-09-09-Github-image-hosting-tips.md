---
layout: post
title: Github做图床
date: 2015-3-02
categories: blog
tags: [Github, 图床, image hosting]
description: 新手向 Github简单图床教程
---

## 以raw形式上传图片至Github

> 请参照[迁移博客图片者的福音：使用GitHub做免费不限流量图床]

- 在GitHub穿件创建任意Repository

- 利用GitHub的Windows客户端clone至本地(Linux可使用命令`git clone *YOUR_REPOSITORY_ADDRESS*`)

- 将需要上传的文件放入本地的文件夹

- 利用GitHub的Windows客户端commit
> Linux系统可使用命令
> ```
> $ git add -A
> $ git commit -m "*YOUR_MESSAGE*"
> S git push
> ```

- 网页浏览复制图片URL，如
```
https://github.com/Chufan1990/Chufan1990.github.io/blob/master/img/2011120710381445.jpg
```
将URL中`blog`替换为`raw`，即
```
https://github.com/Chufan1990/Chufan1990.github.io/raw/master/img/2011120710381445.jpg
```


