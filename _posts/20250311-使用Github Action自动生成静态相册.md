---
layout: post
title: "使用Github Action自动生成静态相册"
date: 2025-03-11 11:50:00 +08:00
categories: ["分享"]
tags: ["Github Action", "相册", "生成"]
---
## 前言

使用`memos`调用的相册虽然方便,但是也有一些痛点无法解决
1. 在CDN被刷流量之后,我已经几乎关闭所有的国内CDN服务,小水管服务器也无法满足大量图片同时加载,那龟速谁用谁知道.
2. S3存储太贵,在COS被刷了流量之后(没错,我就是这么倒霉),我决定多地备份,主要上传在github,利用Cloudflare+ vercel+github pages+ 其他SaaS. 这些服务的优点就是免费.
3. 模板来源于网络

## Deepseek

主要使用AI来解决主要功能代码,主打一个能用就行.至于有什么bug,一个简单的网页生成 能有什么逆天bug也没关系的....吧
主要代码是 `Python`

## 功能

- 我想要的功能

1. 上传图片到Github 仓库,触发 Actions 自动生成Html页面
2. 相册的缩略图需要压缩,点击显示原图,缓解小水管压力(没错,我会定时使用git拉取到国内服务器,主打一个多地都能访问)
3. 根据图片名称自动生成标题

- 更新
2024.12.29
又找了一个模板,自己觉得还可以
加了进去
在workflow里设置需要执行的脚本
两个脚本 分别为 `times.py` 和 `lens.py` 对应着两个模板


## 演示地址

lens模板  https://photo.asbid.cn
times模板  https://photo.sgcd.net

部署在Github Pages

## 使用

### 项目模板

https://github.com/jkjoy/generate-albums 

 
### 设置

 在自己仓库的`Settings`中找到

![指示](https://img.imsun.org/usr/uploads/2024/12/196751803.png)

`TOKEN`为你的 `Github token`

`REPO`为你想要生成相册的仓库名称 如`username/repo`

![设置](https://img.imsun.org/usr/uploads/2024/12/863352623.png)

### 上传规则

相册内容上传到 `photos` 这个目录下

`photos` 根目录下的照片默认标题为`分享生活`

新建文件夹, 该文件夹名称为此目录下所有图片的标题

- 照片同名txt中的文本为描述说明 最高优先级 
如 `1.jpg` `1.txt` 则使用`1.txt`中的文本为描述说明 

- 目录下`描述.txt`为此目录下所有图片的描述说明 第二优先级 

- 如果两者都没有则使用照片文件名为描述说明

### 其他部分

可以根据需求修改 `template`目录下对应模板的`index.html`文件 中的布局和内容.

每次修改仓库会自动触发Action 生成HTML到目标仓库,目标仓库可以使用`Github Pages`,也可以部署在Vercel,这里就不多做说明

### 演示 
https://photos-jkjkjoy.vercel.app/

 
