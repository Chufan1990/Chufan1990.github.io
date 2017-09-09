---
layout: post
title: Github做图床
date: 2017-09-09
categories: blog
tags: [Github, 图床, image hosting]
description: 新手向 Github简单图床教程
---

## 以raw形式上传图片至Github

> 请参照[迁移博客图片者的福音：使用GitHub做免费不限流量图床](http://jingpin.jikexueyuan.com/article/36279.html)

- 在GitHub穿件创建任意Repository

- 利用GitHub的Windows客户端clone至本地
> Linux可使用命令
> ```
> git clone YOUR_REPOSITORY_ADDRESS
> ```

- 将需要上传的文件放入本地的文件夹

- 利用GitHub的Windows客户端commit
> Linux系统可使用命令
> ```
> $ git add -A
> $ git commit -m "YOUR_MESSAGE"
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

## 延伸阅读

转载[GithubTricks: Upload Images & Live Demos](http://solutionoptimist.com/2013/12/28/awesome-github-tricks/)

## 通过GitHub的隐藏功能issue

当前GitHub上没有提供asset管理工具，但是利用GitHub中的``issues``特性可以进行CDN asset的管理。合理利用``issues``会使得上传文件到知识库特别的简单，这些资料不会被*commit/change*跟踪，当在知识库中创建``issues``时，可采用简单的``drag-n-drop``拖拽上传资源至*repository*，步骤如下：

- 创建一个新issue

![](https://github.com/Chufan1990/Chufan1990.github.io/raw/master/img/13bc7eea-132a-11e7-9654-00e275ce3af1.JPG)

- 拖拽图片进去，一次可以添加多个文件（然后把图片的引用复制过来，粘贴到*markdown*)

![](https://github.com/Chufan1990/Chufan1990.github.io/raw/master/img/19_upload_fig.JPG)

- 上传完``issue``之后，就可以直接在图片上右键复制图片URL
