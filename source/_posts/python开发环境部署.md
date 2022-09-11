---
title: python开发环境部署
date: 2021-05-20 09:09:51
cover: /images/posts/python开发环境部署/2022-09-10-23-49-27.png
tags:
   - 环境
   - python
categories:
   - 环境
---
## Windows下的安装

1. 进入[python官方下载页面](https://www.python.org/downloads/)下载合适版本的Python
   ![](/images/posts/python开发环境部署/2022-09-10-23-19-13.png)

2. 双击运行，勾选Add Python 3.6 to PATH，并选择第二项自定义安装Python
   ![](/images/posts/python开发环境部署/2022-09-10-23-19-25.png)

   勾选的选项为给Python添加环境变量，这一步很重要，若此处忘记勾选，安装成功后也要手动添加环境变量

3. 检查是否全部勾选，点击下一步

   ![](/images/posts/python开发环境部署/2022-09-10-23-13-29.png)

4. 勾选Install for all users，然后选择合适的安装路径，点击下一步

   ![](/images/posts/python开发环境部署/2022-09-10-23-19-45.png)

5. 点击install弹出的提示框中点击是，则开始安装

   ![](/images/posts/python开发环境部署/2022-09-10-23-19-55.png)

6. 安装成功后点击close关闭安装窗口，打开命令行检查是否安装成功，输入python后回车

   ![](/images/posts/python开发环境部署/2022-09-10-23-20-08.png)

   至此，Python3.6安装成功

   

## Linux下的安装

Linux自带python2环境，但版本较低，不太适合现在的开发

#### apt安装

1. 打开终端输入

   ```shell
   sudo apt-get install python3.6
   ```

2. 下载pip包管理工具

   linux下载的python不会附带pip包管理工具的安装，需要额外手动安装

   ```shell
   sudo apt-get install python3-pip
   ```

#### 离线包解压安装

1. 安装python3.5可能使用的依赖

   ```shell
   yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
   ```

2. 到python官网找到下载路径, 也可以用wget下载

   ```shell
   wget https://www.python.org/ftp/python/3.5.3/Python-3.5.3.tgz
   ```

3. 解压tgz包

   ```shell
   tar -zxvf Python-3.5.3.tgz
   ```

4. 把python移到/usr/local下面

   ```shell
   mv Python-3.5.3 /usr/local
   ```

5. 删除旧版本的python依赖

   ```shell
   ll /usr/bin | grep python
   rm -rf /usr/bin/python
   ```

6. 进入python目录

   ```shell
   cd /usr/local/Python-3.5.3/
   ```

7. 配置

   ```shell
   ./configure
   ```

8. 编译 make

   ```shell
   make
   ```

   编译，安装

   ```shell
   make install
   ```

9. 删除旧的软链接，创建新的软链接到最新的python

   ```shell
   rm -rf /usr/bin/python
   ln -s /usr/local/bin/python3.5 /usr/bin/python
   python -V
   ```