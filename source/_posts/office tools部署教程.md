---
title: office tools部署教程
date: 2022-02-21 22:58:37
cover: /images/posts/office%20tools部署教程/2022-09-11-16-52-05.png
tags:
categories:
  - 搞机日常/windows
---

## 前期准备

### 卸载office

如果电脑内有其他版本的MS Office，需要卸载干净，防止影响当前office部署
推荐卸载工具：[Geek](https://geekuninstaller.com)

### 下载office tools plus

下载好最新版本的office tools plus

官网地址：https://otp.landian.vip/zh-cn/

## 部署

### 打开office tool工具

将下载好的工具解压目录结构如下（演示的版本是v8.2.8.2）
![](/images/posts/office%20tools部署教程/2022-09-11-16-44-48.png)

打开exe文件，点击部署进入office部署界面，也就是安装office

![](/images/posts/office%20tools部署教程/2022-09-11-16-45-00.png)

注：如果解压后的目录中有`RunMe.bat`文件，则应该双击这个文件打开而不是打开exe文件

### 选择合适的office版本

点击添加产品秘钥，这里又很多版本可以选择，务必要选择对合适的版本

有以下两种情况

- 自己有正版的office

    安装对应的office版本，笔记本出厂自带的正版office一般为`Office 家庭和学生版`，在某宝或者其他途径获取到可用的激活秘钥就选择好对应版本

    不需要进行下面的第三步，部署好了之后直接登录激活或者输入秘钥激活就可以了。

- 手上没有正版的office

    选择带批量许可证的那几个版本（特别注意，没有批量许可证的版本会激活失败）

  ![](/images/posts/office%20tools部署教程/2022-09-11-16-45-19.png)

    此处选择了LTSC这个版本，这个版本是长期支持版本，也就是一次激活成功后长期有效，不需要隔段时间联网重新激活（一般第一次激活成功，以后会自动定期激活，注意不能取消对应的服务项的开机自启动）

### 开始部署

选择好需要安装的office应用，添加语言为默认的简体中文，后面的选项暂时不管，部署设置按照图中来，设置好了之后就可以点击右上角的开始部署了。弹出的对话框选择是

![](/images/posts/office%20tools部署教程/2022-09-11-16-45-29.png)

经过漫长的等待，安装成功后关闭界面回到office tools进行激活操作

## 激活

### 清除激活状态

进入激活界面，如果之前电脑有安装过其他版本的office，许可证管理清除所有许可证

![](/images/posts/office%20tools部署教程/2022-09-11-16-45-38.png)

### 安装许可证

选择自己刚刚部署的版本（默认的也可以），点击安装许可证

### 设置KMS服务器

在`KMS管理`处填入一个可用的KMS激活服务器，此处列举一些，最好百度上找最新的

```text
zh.us.to
kms.03k.org
kms.chinancce.com 
kms.shuax.com
kms.dwhd.org
kms.luody.info 
kms.digiboy.ir
kms.lotro.cc
www.zgbs.cc
cy2617.jios.org
```

果核剥壳

```text
主要地址：kms.ghpym.com
备用地址：kms.qkeke.com
```

端口不用管，点击保存设置

### 激活

提示成功应用设置后，点击右上角的激活，等待一段时间就可以激活成功了

![](/images/posts/office%20tools部署教程/2022-09-11-16-45-51.png)

打开world，查看是否成功激活

![](/images/posts/office%20tools部署教程/2022-09-11-16-46-01.png)

