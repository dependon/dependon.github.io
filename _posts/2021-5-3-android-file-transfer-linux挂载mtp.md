---
layout:     post
title:      "用android-file-transfer-linux替换掉 gvfs-mtp来挂载mtp "
subtitle:   "用android-file-transfer-linux替换掉 gvfs-mtp来挂载mtp"
date:       2021-5-3 16:00:00
author:     "lmh"
header-img: "img/post-think-try-write.jpg"
tags:
    - 聊聊
---
#  用android-file-transfer-linux替换掉 gvfs-mtp来挂载mtp

## 问题现状

在我使用gvfs-mtp挂载的时候,无论读取文件还是获取对应文件夹下所有文件的路径等操作,都非常的卡顿,比本地慢了大概100倍,所以选择使用android-file-transfer-linux来挂载设备是非常优秀的,我感觉就是gvfs-mtp协议层的问题(传输速度一样，但是在读取文件信息速度缓慢异常)

## 仓库地址

github的网站是https://github.com/whoozle/android-file-transfer-linux/

## 如何使用android-file-transfer-linux提供的mount工具挂载

android-file-transfer-linux 的cmake工程编译提供了一个aft-mtp-mount
可以通过执行mkdir ~/mydevice1
aft-mtp-mount ~/mydevice1
即可挂载上去
可以多设备挂载,只需要路径不同即可(两个设备同时挂载上了,但是不知道为啥只有第一个挂载信号被监听到了,但是在终端或者文件管理系统都是找得到这两个挂载路径的)
mkdir ~/mydevice1
aft-mtp-mount ~/mydevice1
mkdir ~/mydevice2
aft-mtp-mount ~/mydevice2

卸载设备:
fusermount -u ~/mydevice1
fusermount -u ~/mydevice2
## 挂载不成功
你需要把gvfs-mtp或者其他正在挂载或者使用mtp的程序给kill掉,才能挂载成果

## 测试平台
国产操作系统UOS1020(deepin)