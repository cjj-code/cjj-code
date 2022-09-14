---
title: VMware虚拟机安装VMware Tools
date: 2021-05-09 20:42:15
cover: /images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-42-34.png
tags:
    - vmware
    - 虚拟机
categories:
    - 环境
---

# VMware Tools的安装

VMware Tools是VMware虚拟机的增强功能，在VMware的虚拟机内安装VMware tools能够大大提升我们操作虚拟机的体验

- 显著提升虚拟机的性能  
  主要为图形显示性能，例如鼠标卡顿

- 实现自适应窗口大小  
  当调整VMware窗口大小时，内部的虚拟机可以自动调整分辨率来适应窗口

- 实现虚拟机、宿主机文件拖拽  
  最实用的功能，不必解释

# Windows下的安装

vmware对Windows有良好的支持，得益于Windows的图形化操作界面，Windows系统安装VMware是最容易的，具体步骤如下（此处以Windows LTSC为例）：

1. 安装好Windows虚拟机后，在选项栏选择 workstation/虚拟机/安装VMware Tools

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-46-41.png)

2. 打开此电脑发现检测到驱动器，双击运行
    
    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-47-43.png)

3. 开始安装，无脑下一步即可

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-47-58.png)

4. 安装完成后虚拟机界面可能会有缩放，说明VMware安装成功，重启虚拟机

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-48-16.png)


# Linux下的安装

​ Linux需要借助命令行进行安装（最新版的Ubuntu20.4图形化操作貌似已可以实现）

kali Linux如果是虚拟机版会自带VMwareTools

1. 在选项栏选择 workstation/虚拟机/安装VMware Tools，应用栏会出现一个DVD图标，点进去

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-48-44.png)

2. 将里面的.tar.gz安装包复制出来

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-49-06.png)


3. 解压刚刚复制出来的压缩包

    ```shell
    $ tar -xzvf [.tar.gz压缩包文件名]
    ```
    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-49-44.png)

4. 在解压后的目录的根目录里打开终端，运行

    ```shell
    $ sudo ./vmware-install.pl
    ```

5. 输入密码后开始安装，安装过程会有停顿大概分以下三种操作

    - 输入密码后的第一个提示输入yes后回车
    - 有[yes]或者[no]根据提示输入yes或no回车
    - 只有路径没有提示则直接回车，直到出现enjoy。

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-50-50.png)

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-51-04.png)

    安装成功后重启虚拟机就OK了。

# macOS下的安装

macOS在点击“安装VMwareTools”时可能会出现报错，系统无法读取到VMware Tools镜像，需要自己下载Mac系统的VMwareTools镜像安装。

1. 下载VMwareTools镜像

    链接：https://wwe.lanzoui.com/iObPYp4mr0d

2. 打开虚拟机设置，在CD/DVD的连接一栏将VMwareTools安装镜像导进去（此时虚拟机为关机状态）

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-51-35.png)

3. 打开macOS，发现桌面出现镜像文件则导入成功，双击运行

    ![](/images/posts/VMware虚拟机安装VMware-Tools/2022-09-14-20-51-52.png)

4. 安装期间需要输入账户密码

    打开设置、安全与隐私，将左下角的锁点开，再选择App Store认可的安装