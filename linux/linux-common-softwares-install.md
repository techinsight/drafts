---
title: Ubuntu常用软件安装流程整理

tags:
  - ubuntu
  - linux

categories:
  - linux

author: 散人

date: 2018-06-29 00:18:14

---

每次安装ubuntu之后，需要查找安装常用软件，现在整理一下常用软件及其安装。我的ubuntu版本是ubuntu mate 17.10，整理的软件也是安装成功的。

> [google拼音输入法](#1)
> [美化终端，安装zsh](#2)
> [安装shadowsocks](#3)
> [安装Chrome浏览器](#4)
> [Oracle JDK安装](#5)
> [Nodejs](#6)
> [Vim强化方案](#7)

<!-- more -->

----------

### <span id='1'>google拼音输入法</span>

google拼音输入法需要在fcitx框架下安装 。

1\. 打开终端，执行如下命令。
```Shell
sudo apt-get install fcitx fcitx-googlepinyin  
```

安装fcitx框架及google拼音。

2\. 打开系统设置菜单“Language Support”。
![Language Support](/images/linux-ubuntu-common-softwares/ubuntu_add_input_language_menu.PNG)  

打开“Language Support”设置窗口。
![Language Support设置](/images/linux-ubuntu-common-softwares/ubuntu_install_simple_chinese.PNG)  

其中“Keyboard input method system”项设置为上一步安装的“fcitx”项。

3\. 安装语言支持。

点击“Install/Remove Languages...”，在弹出的语言选择框中找到“Chinese(Simplified)”项，确认后，开始进行安装。

![安装语言支持](/images/linux-ubuntu-common-softwares/ubuntu_support_languages.PNG)

安装完成之后在则会在“Language Support”对话框中显示已经安装的“汉语(中国)”项。如果没有找到此项，则可以先进行重启操作。

4\. 配置google拼音。

在配置支持google拼音输入法之前，先进行Layouts添加。

选择菜单 “System > Preferences > Hardware > Keyboard”打开“Keyboard Preferences” 打开设置对话框。

![添加中文支持](/images/linux-ubuntu-common-softwares/ubuntu_add_chinese_input_method_layout.PNG)  

选择"Layouts"选项卡，点击“Add”按钮，打开添加“Chinese”布局。

最后添加Google拼音输入法，在菜单中找到并打开“Fictx Configuration”，“Add input method”对话框。

![添加输入法](/images/linux-ubuntu-common-softwares/ubuntu_input_method_configuration.PNG)

点击“+”号，打开“Add input method”对话框。

![添加google输入法](/images/linux-ubuntu-common-softwares/ubuntu_add_google_pinyin.PNG)  

找到开始时安装的“Google Pinyin”，点击OK后，添加完成。

<font color='red'>PS: 添加成功后可能会遇到一个问题，候选词区是黑色，文字看不到，可能是因为多安装了 fcitx-module-kimpanel，因此删除这个软件。</font>

```Shell
sudo apt remove fcitx-module-kimpanel
```

之后再输入的时候可以看到候选词了。

----------

### <span id='2'>美化终端，安装zsh，一款强大的Shell工具</span>

安装

```Shell
sudo apt-get install zsh
```

配置成为默认shell工具

```Shell
chsh -s /bin/zsh
```

```Shell
chsh -s /bin/bash
```

**安装oh-my-zsh**

由于zsh太强大并且复杂，因此安装on-my-zsh扩展工具。这里提前需要安装git工具，负责无法完成安装进度。

安装

*curl方式*

```Shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"  
```

*wget方式*

```Shell
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"  
```

其本质就是下载github上提供的install.sh脚本。

当然如果没有curl，wget就需要先安装这两个工具。  

----------

### <span id='3'>安装shadowsocks客户端</span>

直接执行一下三条命令即可  

```Shell
sudo add-apt-repository ppa:hzwhuang/ss-qt5  
sudo apt-get update  
sudo apt-get install shadowsocks-qt5
```

安装完成之后就可以配置了。

----------

### <span id='4'>安装Chrome浏览器</span>

执行如下命令  

```Shell
sudo wget http://www.linuxidc.com/files/repo/google-chrome.list -P /etc/apt/sources.list.d/
```

```Shell
wget -q -O - https://dl.google.com/linux/linux_signing_key.pub  | sudo apt-key add -
```

```Shell
sudo apt-get update
```

```Shell
sudo apt-get install google-chrome-stable
```

这样就安装成功了。

----------

### <span id='5'>Oracle JDK安装</span>

1\. 到Oracle官网上下载下载教稳定的JDK版本。  

![](/images/linux-ubuntu-common-softwares/ubuntu_jdk.png)  

2\. 选择自己想要将jdk安装到的目录，建立一个java文件夹，将jdk包复制进去。我自己选择的是在/usr目录下，然后使用tar命令，将安装包减压到java目录。

```Shell
sodu tar xzvf jdk-8u171-linux-x64.tar.gz
```

这样就可以完成安装了。

路径：
  
```Shell
/usr/java/jdk1.8.0_171  
```

![](/images/linux-ubuntu-common-softwares/ubuntu_jdk_install_dir.png)
 
3\. 配置环境变量。

```Shell
sudo vim /etc/profile
```

打开文件，在文件末尾添加如下几行：  

```Shell
export JAVA\_HOME=/usr/java/jdk1.8.0\_171  
export JRE\_HOME=$JAVA\_HOME/jre  
export CLASSPATH=.:$JAVA\_HOME/lib/dt.jar:$JAVA\_HOME/lib/tools.jar  
export PATH=$PATH:$JAVA_HOME/bin  
```

退出编辑器，source /etc/profile

4\. 设置系统默认JDK。  
Ubuntu系统可能有提前安装openJDK，因此需要设置默认的JDK，即使系统没有事先安装openJDK，这样设置一次也是好的。

```Shell
sudo update-alternatives --install /usr/bin/java java /usr/java/jdk1.8.0_171/bin/java 300  

sudo update-alternatives --install /usr/bin/javac javac /usr/java/jdk1.8.0_171/bin/javac 300  

sudo update-alternatives --config java  
```

这里需要注意的是路径“/usr/java/jdk1.8.0_171”替换成自己的JDK安装目录。

第三条命令是列出系统当前安装的JDK类型。

由于我安装的ubuntu并没有事先安装openJDK，因此没法罗列出openJDK版本。

如果系统有安装，那么会罗列出openJDK和自己安装的JDK版本，按照提示选择需要设为默认JDK版本需要，如果有openJDK的话，一般是2。

这样，默认的JDK安装及设置就完成了，可以在终端中

```Shell
java -version  
```

来检查安装。

----------

### <span id='6'>Nodejs</span>

**1\. 使用默认ubuntu的软件源。**

ubuntu mate 17.10默认有nodejs的源，可以直接通过命令

```Shell
sudo apt-get install nodejs  
```
  

进行安装，可以通过命令  

```Shell
node -v
```

查看版本号是 6.11.4 是比较旧的版本。

**2\. 自己安装Nodejs。**

\> 安装python依赖库。

```Shell
sudo apt-get install python-software-properties  
```
  
  \> 添加PPA源

```Shell
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -  
```

\> 安装nodejs

```Shell
sudo apt-get install nodejs  
```

**3\. 升级Nodejs。**

如果已经有安装了系统原有的版本较低的Nodejs， 那么就通过n模块对node进行升级。

```Shell
sudo npm cache clean -f  
sudo npm install -g n  
//安装官方最新版本  
sudo n latest  
//安装官方稳定版本  
sudo n stable  
//安装官方最新LTS版本  
sudo n lts  
```

\> 首先清理下缓存，不管是否有，清理下不会有错的。

\> 安装node的n模块，通过n模块来管理版本。

\> 通过n模块来安装指定版本。

----------

### <span id='7'>Vim强化方案</span>

[强化具体方案](https://github.com/techinsight/vim)  

\> 安装vim

```Shell
sudo apt-get install vim  
```

\> 安装ctags

```Shell
sudo apt-get install ctags  
```

\> 安装一些必备程序

```Shell
sudo apt-get install xclip vim-gnome astyle python-setuptools  
```

\> python代码格式化工具

```Sell
sudo easy_install -ZU autopep8  
```

\> 建立ctags软链接

```Shell
sudo ln -s /usr/bin/ctags /usr/local/bin/ctags`
```

\> clone配置文件

```Shell
cd ~/ && git clone git://github.com/ma6174/vim.git  
```

\> 重命名vim并移动配置文件

```Shell
mv ~/vim ~/.vim  
mv ~/.vim/.vimrc ~/  
```

\> clone bundle 程序

```Shell
git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle  
```

\> 打开vim并执行bundle程序

```Shell
:BundleInstall  
```

\> 退出编辑器，重新打开vim后就可以看到效果了。
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0MjQ2ODYyNywxODQ4MzAzODg3LC0xMT
QyNzQyMDYwXX0=
-->