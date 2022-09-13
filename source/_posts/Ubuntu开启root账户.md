---
title: Ubuntu开启root账户
date: 2021-07-24 09:00:00
cover: /images/posts/Ubuntu开启root账户/2022-09-11-00-34-35.png 

tags:
    - linux
    - ubuntu
categories:
    - linux
---

### 创建root账户密码
/images/posts/Ubuntu开启root账户/2022-09-11-00-17-39.png
1. 打开命令行，输入如下命令

   ```shell
   sudo passwd root
   ```

2. 输入当前用户密码，回车

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-17-59.png)

3. 提示输入新的密码，这里其实是在设置root账户密码，回车后需再输入一次确认

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-18-08.png)

### 修改登录相关配置文件

1. 修改 50-ubuntu.conf 文件

   输入命令

   ```shell
   sudo gedit /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf
   ```

   在文件后面追加内容

   > greeter-show-manual-login=true
   >
   > all-guest=false

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-18-18.png)

2. 修改 gdm-autologin 文件

   输入命令

   ```shell
   sudo gedit /etc/pam.d/gdm-autologin
   ```

   注释掉第三行

   > \# auth required pam_succeed_if.so user != root quiet_success

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-18-27.png)

3. 修改 gdm-password 文件

   输入命令

   ```shell
   sudo gedit /etc/pam.d/gdm-password
   ```

   注释掉第三行

   > \# auth required pam_succeed_if.so user != root quiet_success

4. 修改 /root/.profile 文件

   输入命令

   ```shell
   sudo gedit /root/.profile
   ```

   将最后一行的

   > mesg n 2> /dev/null || true

   改为

   > tty -s&&mesg n || true

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-18-37.png)

### 登录root账户

1. 注销当前账户

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-18-45.png)

2. 使用root账户登录
   登录界面选择未列出，账户名输入root，密码就是刚刚设置的密码

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-18-52.png)

3. 进入系统后进入命令行查看

   ![](/images/posts/Ubuntu开启root账户/2022-09-11-00-19-05.png)

   显示当前为root账户登录

