---
title: 用QT、QImage来制作简单图像处理工具
date: 2022-01-20 20:29:11
tags:
---
# 用QT、QImage来制作简单图像处理工具

## 源码地址:
[https://github.com/dependon/simple-image-filter](https://github.com/dependon/simple-image-filter)

## 下载地址(windows版本)
github 下载: [https://github.com/dependon/simple-image-filter/releases/download/1.1.0/simple_image.exe](https://github.com/dependon/simple-image-filter/releases/download/1.1.0/simple_image.exe)

csdn下载: [https://download.csdn.net/download/qq_43081702/36420400](https://download.csdn.net/download/qq_43081702/36420400)

百度云盘: 
链接: [https://pan.baidu.com/s/1MEaqK4UqjLQsR4ZbcrySwg](https://pan.baidu.com/s/1MEaqK4UqjLQsR4ZbcrySwg) 
提取码: k6ec 
## 技术层面
QImage作为容器全权操作，采用了qt+dtk或者默认qt实现

## 实现滤镜技术
实现了老照片、反色滤镜、磨皮滤镜、暖色滤镜、冷色滤镜、灰度滤镜、锐化等滤镜，代码简单，可扩展性强。

##  程序图片


### 磨皮滤镜
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210518142043861.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)


### 多滤镜支持
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210518142106731.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)



### 图片裁切
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210518142114765.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)


### 裁切代码源自:
Clipping function reference:
https://github.com/Leopard-C/ImageCropper