---
title: linux下的python虚拟环境
date: 2021-09-05 15:39:19
cover: /images/posts/linux下的python虚拟环境/2022-09-11-14-32-05.png
tags:
    - 环境
    - python
    - linux
categories:
    - 环境
---

## 一、 安装virtualenvwrapper

使用pip安装virtualenvwrapper

```bash
sudo pip3 install virtualenvwrapper
```

#### 坑：
非root账户一定得加上sudo，否则不会生成virtualenvwrapper.sh脚本

另：如果进入了虚拟环境，使用pip下载包不必加上sudo，加上后默认将包安装在主环境下

## 二、查看本机python3和virtualenvwrapper.sh的路径

1. 查找python3的路径

   ```bash
   which python3
   ```

   > /usr/bin/python3

2. 查找virtualenvwrapper.sh脚本的路径

   ```bash
   sudo find / -name virtualenvwrapper.sh
   ```

   > /usr/local/bin/virtualenvwrapper.sh
   > find: ‘/run/user/1000/gvfs’: 权限不够

这两个路径在修改配置文件时会用到



## 三、修改当前用户bash的配置文件

1. 进入用户目录

   ```bash
   cd ~
   ```

2. 查看当前目录的.bashrc文件

   ```bash
   ls -a
   ```

   > .              .cache     Downloads   .icons      .pki             .rediscli_history  .vscode
   > ..             .config    dump.rdb    .imwheelrc  .presage         .Templates         .Xauthority
   > 安卓应用文件   .dbus      Envs        .java       .profile         .themes            .xsession-errors
   > .bash_history  Desktop    .gnome      .local      .Public          Videos             .xsession-errors.old
   > .bash_logout   .dmrc      .gnupg      Music       PycharmProjects  .viminfo
   > .bashrc        Documents  .gtkrc-2.0  Pictures    .python_history  .virtualenvs

3. 修改这个配置文件

   ```bash
   vim .bashrc 
   ```

   在文件结尾添加如下代码

   ```sh
   WORKON_HOME=~/Envs   
   VIRTUALENVWRAPPER_VIRTUALENV_ARGS='--no-site-packages' 
   VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
   source /usr/local/python3/bin/virtualenvwrapper.sh
   ```

   配置解释

   ```sh
   #设置virtualenv的统一管理目录，以后自动下载的虚拟环境都放在这
   WORKON_HOME=~/Envs   
   #添加virtualenvwrapper的参数，生成干净隔绝的环境
   VIRTUALENVWRAPPER_VIRTUALENV_ARGS='--no-site-packages'
   #指定python解释器的本体 
   VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3
   #执行virtualenvwrapper安装脚本
   source /usr/local/python3/bin/virtualenvwrapper.sh
   ```

## 四、重启命令行

如果配置成功，重启后会显示一段加载代码，以后打开命令行不会再出现这段加载代码

这时可以通过命令创建虚拟环境了

```bash
mkvirtualenv dj
```

> created virtual environment CPython3.7.3.final.0-64 in 437ms
> creator CPython3Posix(dest=/home/stu/Envs/dj, clear=False, no_vcs_ignore=False, global=False)
> seeder FromAppData(download=False, pip=bundle, setuptools=bundle, wheel=bundle, via=copy, app_data_dir=/home/stu/.local/share/virtualenv)
>  added seed packages: pip\=\=21.2.3, setuptools\=\=57.4.0, wheel\=\=0.37.0
> activators BashActivator,CShellActivator,FishActivator,PowerShellActivator,PythonActivator
> virtualenvwrapper.user_scripts creating /home/stu/Envs/dj/bin/predeactivate
> virtualenvwrapper.user_scripts creating /home/stu/Envs/dj/bin/postdeactivate
> virtualenvwrapper.user_scripts creating /home/stu/Envs/dj/bin/preactivate
> virtualenvwrapper.user_scripts creating /home/stu/Envs/dj/bin/postactivate
> virtualenvwrapper.user_scripts creating /home/stu/Envs/dj/bin/get_env_details

#### 坑：
重启命令行报错`virtualenv: error: unrecognized arguments: --no-site-packages`

查看virtualenv版本

```bash
virtualenv --version
```

发现版本号大于20，此时回到第三步中的修改配置文件，将

```sh
VIRTUALENVWRAPPER_VIRTUALENV_ARGS='--no-site-packages'
```

这一行删掉，重启命令行

因为从版本20开始，默认就是`--no-site-packages`

