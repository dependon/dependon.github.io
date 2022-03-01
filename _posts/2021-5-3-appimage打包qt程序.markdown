---
layout:     post
title:      "appimage打包qt程序 "
subtitle:   "appimage打包qt程序"
date:       2021-5-3 15:00:00
author:     "lmh"
header-img: "img/post-think-try-write.jpg"
tags:
    - 聊聊
---
# linux下将qt程序打包成appimage程序

## 一.环境准备

### 1.1下载linuxdeployqt的程序（打包qt程序的工具）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413151441518.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

https://github.com/probonopd/linuxdeployqt/releases

下载appimage的包linuxdeployqt-7-x86_64.AppImage

下载下来更改一下权限sudo chmod 777 linuxdeployqt-7-x86_64.AppImage
arm的话，自行编译吧
### 1.2下载appimagekit（appimage工具）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413151447278.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

https://github.com/AppImage/AppImageKit/releases/

下载appimage的包appimagetool-x86_64.AppImage

下载下来更改一下权限sudo chmod 777 appimagetool-x86_64.AppImage
### 1.3本地环境安装
sudo apt install patchelf

### 1.4配置qt的位置
sudo vim ~/.bashrc {编辑 ~/.bashrc}
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413151459729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

配置qt5的环境

这里配置的qt环境由于我是使用deepinV20.2系统，系统自带qt5.15，我就才用了系统的环境

如果是自行安装的采用自行安装的路径即可

export PATH=/usr/lib/x86_64-linux-gnu/qt5/bin:$PATH 

export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH

export QT_PLUGIN_PATH=/usr/lib/x86_64-linux-gnu/qt5/plugins:$QT_PLUGIN_PATH

export QML2_IMPORT_PATH=/usr/lib/x86_64-linux-gnu/qt5/qml:$QML2_IMPORT_PATH


## 二.开始打包

### 2.1编译出可执行程序(realease版本)

获得可执行程序，将可执行程序拷贝到随便一个文件夹

这里就拷贝到文件夹11内

### 2.2linuxdeployqt发力
在这里linuxdeployqt-7-x86_64 登场

直接对可执行程序进行操作

./linuxdeployqt-7-x86_64.AppImage 程序目录/程序 -appimage
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413151744227.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)
报错了，因为glic版本问题
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413152908345.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413152917456.png)

如果glic>=2.27,你就需要加上参数 -unsupported-allow-new-glibc ，并且加上了该参数也许这个程序将不能在低版本发行版使用(没试过)

./linuxdeployqt-7-x86_64.AppImage 程序目录/程序  -appimage -unsupported-allow-new-glibc

大部分的依赖项都到了该程序目录内
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413153048892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

### 2.3修改desktop
因为默认生成的desktop存在问题，直接使用appimagetool打包会出现以下显示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413152855174.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

appimagetool, continuous build (commit effcebc), build 2084 built on 2019-05-01 21:02:41 UTC
WARNING: appstreamcli command is missing, please install it if you want to use AppStream metadata
Categories entry not found in desktop file
.desktop file is missing a Categories= key

他提醒你，缺少Categories= key，由于我们是qt程序，大部分是application，所以一般都是这样增加配置
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413152934759.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

Categories=Application;
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021041315282023.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)


更改名字那些就是跟freedesktop的教程一样，这里提供一个吗模板

[Desktop Entry]
Categories=Application;
Comment=x11opacity-tool
Comment[zh_CN]=linux窗口透明工具
Encoding=UTF-8
Exec=AppRun %F
GenericName=x11opacity-tool
GenericName[zh_CN]=linux窗口透明工具
Icon=default
Name=x11opacity-tool
Name[zh_CN]=linux窗口透明工具
StartupNotify=false
Terminal=false
Type=Application


修改了desktop文件


### 2.4appimagetool发力

执行 ./appimagetool-x86_64.AppImage 程序目录 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413153315324.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

生成成功！！，一个appimage包就打好了

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021041315314044.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)

执行![在这里插入图片描述](https://img-blog.csdnimg.cn/20210413153148497.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMDgxNzAy,size_16,color_FFFFFF,t_70)
这里应该是跨发行版执行
# 联系我
liuminghang0821@gmail.com