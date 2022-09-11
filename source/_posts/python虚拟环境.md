---
title: python虚拟环境
date: 2021-05-20 14:29:26
cover: /images/posts/python虚拟环境/2022-09-11-00-15-00.png
tags:
    - python
    - 环境
categories:
    - 环境
---
# python虚拟环境


## 1. 什么是虚拟环境

python虚拟环境是独立于已经安装的python环境的环境，各个环境之间互不影响。比如我正在学习python爬虫，我可以创建一个名为spider的虚拟环境专门放置与爬虫有关的包，过段时间我学习Django，可以创建一个名为dj的环境安装Django。

​		不仅仅是方便管理，虚拟环境还能减少环境冲突和包之间的冲突以及其他不必要的麻烦，比如以下场景：

- 项目A使用的是Django1.9，而项目B需要Django2.1

- 项目A使用python2.7，项目B使用python3.8

## 2. 虚拟环境管理包（virtualenvwrapper）

### 2.1 部署

确保python环境正常，在命令行下，用pip安装virtualenvwrapper

- Windows：

  ```shell
  pip install virtualenvwrapper-win
  ```
    添加环境变量WORKON_HOME
    变量：WORKON_HOME
    值：指定存放虚拟环境的目录
- linux：

  ```shell
  sudo pip install virtuallenvwrapper
  ```
  创建一个存放虚拟环境的文件夹
  ```shell
  cd ~
  mkdir .envs
  ```
  添加环境变量
  ```
  sudo vim ~/.bashrc
  ```
  添加如下内容
  ```text
  export WORKON_HOME=$HOME/.envs
  export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
  export VIRTUALENVWRAPPER_VIRTUALENV=/usr/local/bin/virtualenv
  source /usr/local/bin/virtualenvwrapper.sh
  ```
  - `WORKON_HOME`为指定的存放虚拟环境的目录
  - `VIRTUALENVWRAPPER_PYTHON`指定生成虚拟环境的python
  - `VIRTUALENVWRAPPER_VIRTUALENV`为virtualenv脚本的路径，
 查看Python和virtualenvwrapper的路径：
  ```
  whereis python3
  whereis virtualenv
  ```

### 2.2 常用操作

1. 创建虚拟环境（创建后会自动进入创建的虚拟环境）

   ```shell
   mkvirtualenv <name>
   ```

   <name>为虚拟环境的名称

2. 退出虚拟环境

   ```shell
   deactivate
   ```

3. 进入虚拟环境

   ```shell
   workon <name>
   ```

   进入虚拟环境后用pip安装python包只会安装在该虚拟环境下

4. 删除虚拟环境

   ```shell
   rmvirtualenv <name>
   ```

## 3. 第三方包管理工具（anaconda）

### 3.1  下载anaconda

下载地址：https://www.anaconda.com/download/

### 3.2 常用操作

- 环境操作

  1. 创建虚拟环境

     ```shell
     conda create -n <name> python=3.6
     ```

     或

     ```shell
     conda create --name <name> python=3.6
     ```

     可以通过python --version查看python版本


  2. 切换、进入虚拟环境

     ```shell
     activate <name>
     ```

  3. 卸载虚拟环境

     ```shell
     conda remove --name <name> --all
     ```

  4. 查看所有的虚拟环境

     ```shell
     conda env list
     ```

- 包操作

  1. 安装包

     ```shell
     conda install <name>
     ```

     或

     ```shell
     pip install <name>
     ```

  2. 卸载包

     ```shell
     conda remove <name>
     ```

     或

     ```shell
     pip uninstall <name>
     ```

  3. 查看当前环境下所有的包

     ```shell
     conda list
     ```

  4. 删除指定环境下所有的包

     ```shell
     conda remove -n <name> --all
     ```

  5. 更新指定的包

     ```shell
     conda update <name>
     ```

## 4. 更改虚拟环境的路径

1. 添加环境变量

   变量名：WORKON_HOME

   变量值：虚拟环境路径

   ![](/images/posts/python虚拟环境/2022-09-11-00-00-47.png)

2. 修改虚拟环境配置文件

   打开python的安装目录下的Scripts文件夹，找到mkvirtualenv.bat文件

   ![](/images/posts/python虚拟环境/2022-09-11-00-00-57.png)

   右击，点击编辑，找到第24行的

   set "venvwrapper.default_workon_home=%USERPROFILE%\Envs"

   修改为

   set "venvwrapper.default_workon_home=%WORKON_HOME%\Envs"

   ![](/images/posts/python虚拟环境/2022-09-11-00-01-07.png)

   此后使用mkvirtualenv创建的虚拟环境将会创建在D:env/Pyenv下