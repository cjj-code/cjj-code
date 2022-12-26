---
title: vscode远程开发配置
date: 2022-02-19 17:30:06
cover: /images/posts/vscode远程开发配置/2022-09-11-14-39-23.png
tags:
    - vscode
categories:
    - 环境
---

# SSH

## 1. 远程连接

### 1.1 安装ssh插件

进入插件安装界面，搜索ssh，认准微软官方插件，安装第一个

![](/images/posts/vscode远程开发配置/2022-09-11-14-39-44.png)

安装后会附带安装其他一个或两个ssh插件（均是微软官方插件），同时左侧栏中会增加远程连接功能

### 1.2 连接远程服务器
点击左侧新增的电脑图标，点击+号添加一个远程连接
![](/images/posts/vscode远程开发配置/2022-09-11-14-39-53.png)

在输入框汇中根据提示的格式添加远程连接，用户名就是远程服务器的账户
```shell
ssh <用户名>@<ip>        # 例：ssh root@192.168.0.1
```
回车后选择ssh一个配置文件的保存路径，一般选第一个，记住这个路径，添加成后点击右方图标连接会新建一个窗口连接远程服务器

![](/images/posts/vscode远程开发配置/2022-09-11-14-40-04.png)


## 2. 免密登录

vscode在连接远程服务器时每次进入或者打开一个新的文件夹时都需要输入登录密码，非常麻烦

### 2.1 本地生成公钥和私钥

用`ssh-keygen`命令生成密钥对

打开终端，输入命令，有提示直接回车

![](/images/posts/vscode远程开发配置/2022-09-11-14-40-14.png)

此时，在以下路径中会生成两个文件

```
C:/用户/O_O/.ssh   # O_O为用户名
```

> - id_rsa: 私钥
> - id_rsa.pub: 公钥

![](/images/posts/vscode远程开发配置/2022-09-11-14-41-03.png)

### 2.2 公钥上传至远程

使用文本编辑器打开公钥文件，复制出里面的公钥

公钥格式大致为

```txt
ssh-rsa 秘钥 用户名@设备名
```

进入服务器端的`/root/.ssh/`目录（非root账户是`/home/<用户名>/.ssh`）

打开`authorized_keys`文件，如果没有就创建，将刚刚复制的公钥粘贴进去，保存


### 2.3 修改ssh配置文件

接下来为vscode配置私钥

windows下vscode的ssh配置文件在`/用户/O_O/.ssh/config`文件，打开这个文件。每个条目的大致格式如下

```txt> 
HOST <连接名称>
  HostName <远程主机IP>
  User <用户名>
  IdentityFile "C:\Users\O_O\.ssh\id_rsa"
```

最后一行是我们需要添加的配置，值为私钥文件的路径

执行完上述步骤后，不出意外的话再次打开vscode就不需要密码就可以直接进入服务器了


# SFTP

与ssh方式不同，sftp是在本地映射出一个与服务器上相同的项目，修改在本地修改，需要的时候将修改上传至服务器（也可设置自动上传修改）

## 安装插件

直接去vscode应用商店搜索sftp，安装star数量最多的那个

![](/images/posts/vscode远程开发配置/2022-11-29-22-32-45.png)

官方地址：https://marketplace.visualstudio.com/items?itemName=Natizyskunk.sftp

## 配置

服务器的用户、密码、映射路径等是在vacode配置文件中配置

