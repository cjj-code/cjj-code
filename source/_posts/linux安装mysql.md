---
title: linux安装mysql
date: 2021-09-15 15:25:26
cover: /images/posts/ubuntu安装mysql/2022-09-11-14-34-02.png
tags:
   - 环境
   - mysql
categories:
   - 环境
---

此方法适用于Debian的发行版（Debian、Ubuntu、Deepin）

## 一、直接使用apt安装

1. 安装mysql服务端、核心程序

   ```bash
   sudo apt-get install mysql-server
   ```

2. 安装mysql客户端

   ```bash
   sudo apt-get install mysql-client
   ```

3. 验证是否安装成功

   ```bash
   sudo netstat -tap | grep mysql
   ```

4. 开启mysql服务

   ```bash
   sudo service mysql start
   ```

==注==：如果apt安装时提示找不到mysql源用方法二

## 二、添加mysql到apt源

1. 下载mysql deb包

   在[mysql官网下载页面](https://dev.mysql.com/downloads/)，选择`MySQL Community Server`，下拉框选择`Debian Linux`，点击正下方的图片的`Download Now`

   ![](/images/posts/ubuntu安装mysql/2022-09-11-14-34-46.png)

   下一个页面点击下载

2. apt更新

   在下载的包所在目录运行

   ```bash
   sudo dpkg -i <deb包名>
   ```

   此时命令行会变成一个界面

   ![](/images/posts/ubuntu安装mysql/2022-09-11-14-34-57.png)

   这里选择第一个

   ![](/images/posts/ubuntu安装mysql/2022-09-11-14-35-08.png)

   版本按需求，一般选择最新版

   ![](/images/posts/ubuntu安装mysql/2022-09-11-14-35-47.png)

   接下来选择OK后确认

   这个界面没有完全恢复成正常的命令行，可能是deepin的bug，不用管它，正常输命令

3. 从 MySQL apt存储库更新包信息

   ```bash
   sudo apt-get update
   ```

4. 安装mysql

   ```bash
   sudo apt-get install mysql-server
   ```

   - 此安装会顺带将mysql-client一并安装

   - 安装过程会提示设置mysql登录密码，免去了后期更改配置文件的麻烦

   - 密码验证方式选择推荐的强验证方式
