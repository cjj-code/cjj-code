---
title: piexl4刷机root记录
date: 2022-11-27 23:34:18
cover: /images/posts/piexl4刷机root记录/2022-11-27-23-46-17.png
tags:
categories:
---

# 准备工作

## 镜像和文件

### 刷机包

去piexl官网去下载谷歌官方刷机包
镜像地址：[https://developers.google.com/android/images#flame](https://developers.google.com/android/images#flame)
piexl4官方镜像包含安卓10-安卓13，这里选择了安卓10的最新版

![](/images/posts/piexl4刷机root记录/2022-11-27-23-48-41.png)

下载写来后是一个zip压缩包，需要解压

### TWRP

> 非必须，如果使用修补boot镜像方式获取root就不需要下载twrp

进入twrp官网：[https://twrp.me](https://twrp.me/)，点击`Devices`根据机型选择合适的twrp镜像

![](/images/posts/piexl4刷机root记录/2022-11-27-23-49-07.png)

piexl是谷歌原版安卓机型，依次选择Google/Google Piexl 4 (flame)

![](/images/posts/piexl4刷机root记录/2022-11-27-23-49-20.png)

这里区分了欧版还是美版，我手上的是欧版，这里选择`Americas`

![](/images/posts/piexl4刷机root记录/2022-11-27-23-49-32.png)

安卓10及以上的系统使用的是`A/B分区`或`模拟A/B分区`，刷twrp需要固化，所以这里`img`文件和`zip`文件都要下载

### Magisk

GitHub项目地址：[https://github.com/topjohnwu/Magisk](https://github.com/topjohnwu/Magisk)
在[releases](https://github.com/topjohnwu/Magisk/releases)里下载apk

![](/images/posts/piexl4刷机root记录/2022-11-27-23-49-42.png)

若使用twrp方式root，magisk下载到本地后，复制一份并把`.apk`后缀改为`.zip`

## 解锁BootLoader

# 刷机

## 进入fastboot模式

方式一：关机状态下
piexl关机状态进入fastboot模式：`电源键`+`音量-`
长按直至进入fastboot

> 细节：放开时电源键先放，偶尔会出现放手后直接进入系统

方式二：开机状态下
开机状态可以使用adb命令直接进入fastboot

```bash
$ adb reboot fastboot
```

## 刷机

解压下载的刷机包
手机fastboot模式下，双击`flash-all.bat`即可开始刷机，期间手机会自动重启几次

![](/images/posts/piexl4刷机root记录/2022-11-27-23-49-53.png)


> .bat是Windows的批处理文件，如果是在Mac或Linux下刷机则是运行flash-all.sh文件

# 获取root权限

## 修补boot镜像方式

解压下载的官方刷机包后，再解压里面的zip文件，找到boot.img文件，使用adb命令将这个镜像推至安卓设备

![](/images/posts/piexl4刷机root记录/2022-11-27-23-50-02.png)

![](/images/posts/piexl4刷机root记录/2022-11-27-23-50-11.png)

```bash
$ adb push ./boot.img /sdcard/Download/
```

### 安装magisk

直接使用adb命令向安卓设备安装magisk

```bash
$ adb install ./Magisk.apk
```

### 修补boot镜像

手机打开安装好的Magisk，点击安装，选择修补一个文件
选择刚刚推至手机Download目录的boot.img镜像文件，点击修复
此时Download文件夹下会生成一个.img文件，这就是修补了magisk后的boot镜像

> 为了方便后续操作，修补后的img文件重命名成`m_boot.img`

### 刷入boot镜像

在电脑端将刚刚修补的magisk镜像拉回电脑本地

```bash
$ adb pull /sdcard/Download/m_boot.img ./
```

然后让手机进入fastboot模式刷这个boot镜像

```bash
$ adb reboot fastboot
```

A/B分区最好是将A分区和B分区都刷一遍

```bash
$ fastboot flash boot_a ./m_boot.img
$ fastboot falsh boot_b ./m_boot.img
```

非ab分区只需`fastboot flash boot <boot镜像地址>`即可

## 第三方recovery方式

### 刷入twrp

A/B分区的系统刷入twrp需要分两步走：临时twrp -> 固化

### 安装magisk模块

安装好twrp先不急着进入系统，先重启回到recovery模式刷入magisk模块

### 安装magisk软件

固化好twrp后，进入系统，并安装magisk app 

```bash
$ adb install ./Magisk.apk
```

重启之后再次打开magisk app就可以看到成功root了

# 救砖

A/B分区系统在刷twrp时最容易变砖，表现为可以开机，但无法进入安卓系统，或只进入TWRP（即recovery模式）

## 重刷boot分区

root操作导致的手机变砖往往是因为损坏了boot分区导致，尤其是刷第三方recovery也就是twrp时，很容易变砖。
最简单的方式就是提取官方原版镜像中的boot.img文件重新刷入boot分区

## 重新刷机

重刷boot分区也无法进入系统，直接重新刷机。只要能进fastboot，都可以说问题不大。
无论卡在哪个界面，都可以试试强制进入fastboot，这里piexl4是“长按电源+音量-键”，然后从本文步骤2开始重新刷系统

## 9008救砖

如果手机直接被刷成黑砖，连较为底层的fastboot也无法进入，只能尝试进入9008模式（EDL串口线刷模式）救砖

> 9008只对搭载高通骁龙处理器的机型有用，piexl4使用的是高通骁龙855，可以使用此方式救黑砖，但并不能保证100%成功。为了防患于未然，在刷机前最好备份字库和基带串号等，9008模式无法恢复这些。

## 钞能力

没有什么是一撮💵解决不了的，如果有，那就多来几撮~
以上方法都不奏效且设备急用，就去某宝找专业人士吧。
但是，身为一名搞机人士，该有的折腾精神还是得有的。

# 常用Magisk模块

## 抓包软件证书迁移至系统

## 更换字体

## 修改系统调度

