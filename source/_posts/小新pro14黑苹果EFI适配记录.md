---
title: 联想小新pro13 2020黑苹果配置记录
date: 2022-09-30 21:26:12
cover: /images/posts/小新pro14黑苹果EFI适配记录/2022-09-14-21-05-27.png
tags:
categories:
---

今天是个难忘的日子，来点料

# 电脑硬件配置

机型：`联想小新pro13 2020 i7`

| 硬件 | 配置 |
| --- | --- |
| 处理器 | Intel Core i7 10710 |
| 内存 | 16GB ddr4 2667MHz |
| 硬盘 | 西数 SN730 1TB |
| 核显 | Intel Iris Plus Graphics 620 |
| 独显 | NVIDIA MX350 |
| 有线网卡 | Realtek RTL8111 |
| 无线网卡 | Intel WiFi6 AX201 160MHz |
| 声卡 | Realtek ALC257 |
| 显示器 | 13.3 英寸 IPS 2560x1600 |

说明：此机型为2020年大火的黑苹果机型，早就相中了，疫情被封期间在咸鱼上淘的。正是因为其各项配置黑苹果潜力大，有众多大佬维护EFI，驱动已经相当完善，日常使用与白苹果已经相差不大。

# 配置EFI

## 获取EFI

[黑果小兵长期维护机型](https://blog.daliansky.net/Hackintosh-long-term-maintenance-model-checklist.html)，EFI地址：https://github.com/daliansky/XiaoXinPro-13-hackintosh

`Releases` 中的 `opencore` 版本已经更新至OC0.8.4

![](/images/posts/小新pro14黑苹果EFI适配记录/2022-11-17-22-57-05.png)

下载这个EFI文件在本地解压

文件结构大致如下

```shell
$ tree .
.
├── BOOT                          # 引导文件夹
│   └── BOOTx64.efi               # 引导文件
└── OC                            # OC 文件夹
    ├── ACPI                    # ACPI 存放的文件夹
    │   ├── SSDT-EC.aml
    │   ├── SSDT-PLUG.aml
    │   │── SSDT-PNLF.aml
    │       ...
    ├── Drivers                   # OC 驱动的文件夹
    │   ├── AudioDxe.efi
    │   ├── CrScreenshotDxe.efi
    │   ├── HiiDatabase.efi
    │       ...
    ├── Kexts                     # 存放内核拓展 kexts 的文件夹
    │   ├── AppleALC.kext
    │   ├── Lilu.kext
    │   ├── WhateverGreen.kext
    │       ...
    ├── OpenCore.efi              # OC 的核心文件
    ├── Resources                 # OC 的主题样式
    │   ├── Audio
    │   ├── Font
    │   ├── Image
    │   └── Label
    └── Tools                     # OC 小工具文件夹
        ├── BootKicker.efi
        ├── ChipTune.efi
        ├── CleanNvram.efi
            ...
```


大佬制作好的EFI是针对所有该机型配置的一个通用版，需要针对自己的配置进行更改才能真正使用。

## 配置EFI的工具

`OCAuxiliaryTools`: https://github.com/ic005k/OCAuxiliaryTools

`OpenCore Configurator`: https://mackie100projects.altervista.org

这里选择`OCAuxiliaryTools`来配置OpenCore

打开EFI文件夹中的`config.plist`文件

![](/images/posts/小新pro14黑苹果EFI适配记录/2022-11-17-23-47-28.png)


## 配置网卡驱动

> 由于英特尔网卡不支持隔空投送，所以大量黑苹果玩家都习惯更换一个博通网卡以追求更加完美的mac生态，EFI也是照顾大部分玩家的需求加上了博通网卡的支持。本机型的EFI更是直接没有在配置文件中启用网卡驱动，需要自己根据使用的网卡来配置网卡参数。



## 更换序列号

> 原本的config配置中是有序列号等信息的，但是这个序列号是这个EFI文件下载时初始的序列号，可能有很多人图省事没有更换序列号直接使用这个EFI，这就导致原本的EFI中的序列号可能有很多人在用，我们最好不要直接用这个序列号，需要自己更换。

进入`PI`模块(PlatformInfo)下的`通用`选项卡, 这里有机型相关的参数设置以及`设备序列号`的设置
OCC编辑器可以一键生成序列号，这点还是很方便的

![](/images/posts/小新pro14黑苹果EFI适配记录/2022-11-18-00-41-44.png)

注：选择机型尽量选择和自己CPU相近的，设置完之后保存一下

# 安装mac系统

## 划分mac分区

一般1个T的硬盘到手，我会按照如下分区

| 分区大小 | 分区类型 | 分区作用 | 说明 |
| :---: | :---: | --- | --- |
| 500MB | efi | Windows引导分区 | EFI分区 |
| 500MB | efi | OpenCore引导分区 | OpenCore引导文件存放位置 |
| 80GB | ntfs | Windows系统分区 | 用作C盘 |
| 400GB | ntfs | Windows数据分区 | 用作D盘 |
| 500GB | apfs | MacOS分区 | 用于安装MacOS系统 |


## 制作系统安装U盘

## 安装mac系统

# 系统优化

## 常用环境

## 常用软件安装