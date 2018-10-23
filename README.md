# test
# CentOS Everything Software Management
[TOC]
## Linux distribution
CentOS-7-x86_64-Everything-1511.iso  
默认桌面环境：Gnome

## 普通用户免密码使用sudo
使用以下命令编辑文件：/etc/sudoers
```shell
# sudo visudo
```
在文件中添加以下内容：
```txt
long ALL=(ALL) NOPASSWD: ALL
```
注意：上述内容一定要添加到/etc/sudoers尾部，否则后可能被它之的设置覆盖。

## 快捷键打开终端
默认桌面环境gnome下的启动终端命令：
```shell
/usr/bin/gnome-terminal
```
在Applications > System Tools > Settings > Keyboard > Shortcuts > Custom Shortcuts中添加以下内容：
```txt
Name: run a terminal
Command: /usr/bin/gnome-terminal
```
设置快捷键为：**ctr+alt+t**

## 删除firefox浏览器
```shell
# sudo yum remove -y firefox
```

## 安装python-pip
```shell
# sudo yum install -y epel-release
# sudo yum install -y python-pip
# sudo pip install --upgrade pip
```

## 安装chrome浏览器
### 1. 配置chrome的yum源
使用以下命令新建文件：/etc/yum.repos.d/google-chrome.repo
```shell
# sudo vim /etc/yum.repos.d/google-chrome.repo
```
添加以下内容
```yum
[google-chrome]
name=google-chrome
baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch
enabled=1
gpgcheck=0
gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub
```
注意，如果不可以访问google，建议把gpgcheck设置为0，否则设置为1。
### 2. 安装chrome浏览器
```shell
# sudo yum info google-chrome-stable
# sudo yum install -y google-chrome-stable
```

### 3. 启动chrome浏览器
```shell
# google-chrome &
```
注意，chrome安装之后图标会出现在系统中，可以用**windows**键查看。

## 安装g++
默认情况下gcc和gdb已经安装
```shell
# sudo yum install -y gcc-c++
```

## 安装五笔输入法
```shell
# sudo yum install -y ibus-table-wubi
# sudo reboot
```
在Settings->Region & Language->Input source下添加**chinese(wubi-jidian86)**

## 安装性能统计工具：perf
```shell
# sudo yum install -y perf
```

## 安装shadowsocks-qt5
使用以下命令新建/etc/yum.repos.d/shadowsocks.repo
```shell
# sudo vim /etc/yum.repos.d/shadowsocks.repo
```
在文件中添加以下内容：
```txt
[librehat-shadowsocks]
name=Copr repo for shadowsocks owned by librehat
baseurl=https://copr-be.cloud.fedoraproject.org/results/librehat/shadowsocks/epel-7-$basearch/
type=rpm-md
skip_if_unavailable=True
gpgcheck=1
gpgkey=https://copr-be.cloud.fedoraproject.org/results/librehat/shadowsocks/pubkey.gpg
repo_gpgcheck=0
enabled=1
enabled_metadata=1
```
使用以下命令安装shadowsocks：
```shell
sudo yum update
sudo yum install shadowsocks-qt5
```
代理设置  
进入设置**Settings->Network->Network Proxy**，打开代理,使用**sock**协议
```txt
local address: 127.0.0.1
local port: 1080
```

## vim常用设置
```txt
set nu  # show line number
set paste # paste mode without autoindent
```

## 安装sublime text 3
### Install the GPG key:
```shell
# sudo rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg
```
### Select the channel to use:
```shell
Stable
# sudo yum-config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo
Dev
# sudo yum-config-manager --add-repo https://download.sublimetext.com/rpm/dev/x86_64/sublime-text.repo
```
###
以上两个步骤可以会因为网络问题出错，可以直接新建文件**/etc/yum.repos.d/sublime-txt.repo**，并添加以下内容
```txt
[sublime-text]
name=Sublime Text - x86_64 - Stable
baseurl=https://download.sublimetext.com/rpm/stable/x86_64
enabled=1
gpgcheck=1
gpgkey=https://download.sublimetext.com/sublimehq-rpm-pub.gpg
```
### Update yum and install Sublime Text
```shell
# sudo yum update -y
# sudo yum install -y sublime-text
```
### Add sublime text 3 to the CentOS 7 Application Menu Finally
we want to add sublime 3 to the CentOS 7 Application menu.  
Create a text file called “sublime_text_3.desktop” inside the **/usr/share/application** directory.
```shell
# vim /usr/share/applications/sublime_text_3.desktop
```
Then add the following entries and save the file.
```txt
[Desktop Entry]
Version=1.0
Type=Application
Name=Sublime Text
GenericName=Text Editor
Comment=Sophisticated text editor for code, markup and prose
Exec=/opt/sublime_text_3/sublime_text %F
Terminal=false
MimeType=text/plain;
Icon=/opt/sublime_text_3/Icon/128x128/sublime-text.png
Categories=TextEditor;Development;
StartupNotify=true
Actions=Window;Document;
```
Notice that Exec and Icon are corresponding to the installation directory. now you should see the sublime 3 text editor launcher on the application menu under the programming sub category.  
### Add Desktop Shortcut
To add CentOS 7 Desktop shortcut, create a text file called sublime3.desktop on your desktop and add the following entries.
```shell
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Name=Sublime Text
Exec=/opt/sublime_text_3/sublime_text %F
Terminal=false
Icon=/opt/sublime_text_3/Icon/128x128/sublime-text.png
```
Then double click to run the file and Click on Mark as Trusted button, when you get the “Untrusted application launcher” dialog. Once you click the Mark as Trusted button, Shortcut to the sublime text editor will appear on your CentOS Desktop. OK then! this is the end of this article. You can see how easy it was to install sublime text editor on Linux CentOS 7.

## 安装git
```shell
sudo yum install -y git
```

## 安装automake
```shell
sudo yum install -y automake
```
命令会安装automake所需要的全部包，包括m4,autoconf, autoamke, libtool
autoconf包: autoscan autoheader autoconf
automake包: aclocal automake
