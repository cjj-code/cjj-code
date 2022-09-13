---
title: vmware安装windows11
date: 2022-03-26 17:30:34
cover: /images/posts/vmware安装windows11/2022-09-11-16-39-36.png
tags:
categories:
---

windows11版本对硬件有了要求，比较低的配置是无法通过镜像的检测安装系统，无论是实体机还是虚拟机，安装windows11虚拟机需要使用pe安装

## 1. 获取windows11镜像

比较有名的系统iso镜像下载站是msdn
- 老版：https://msdn.itellyou.cn
- 新版：https://next.itellyou.cn
- hellowindows：https://hellowindows.cn

## 2. 准备启动U盘

将windows镜像写入U盘，作为系统启动盘。
强烈推荐：使用ventoy制作启动盘，直接将iso文件复制到U盘，具体操作请看[这里]()


## 3. vmware设置U盘启动

1. 正常创建一个虚拟机，操作系统类型可以设置为windows10，创建后不用设置使用iso镜像。
2. 开机，将U盘连接至虚拟机：依次选择导航栏中的Workstation(vm窗口较小的时候会有这个选项)/虚拟机/可移动设备/U盘设备名称
![](/images/posts/vmware安装windows11/2022-09-11-16-36-56.png)
U盘设备名称可以在右下角托盘中的usb图标右击可以看到
3. 等待片刻就会识别到U盘，保持鼠标焦点在虚拟机，及时按回车键
![](/images/posts/vmware安装windows11/2022-09-11-16-37-04.png)
到这里就成功了，加载完成后选择一个pe系统进入

## 4.开始安装系统

1. 分区
使用pe内置的`diskgenius`快速分区
![](/images/posts/vmware安装windows11/2022-09-11-16-37-16.png)
2. 开始安装
这里选择的安装工具是`WinNTSetup`，安装源已经放在U盘里选择那个win11的镜像就行，引导分区和安装分区如下
![](/images/posts/vmware安装windows11/2022-09-11-16-37-24.png)
安装、确定，等待安装成功重启就OK。这样安装不会触发镜像内的硬件检测
![](/images/posts/vmware安装windows11/2022-09-11-16-37-32.png)