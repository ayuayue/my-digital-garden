---
tags: []
title: windows下使用docker+wsl2开发
date: 2023-05-28T13:40:53+08:00
lastmod: 2023-05-28T13:40:59+08:00
dg-publish: true
dg-pinned: false
dg-hide: false
dg-hide-in-graph: false
---
# 推荐阅读

[Dev on Windows with WSL](https://dowww.spencerwoo.com/)
# docker

windows 的 docker 可以去官网下载，安装后重启即可。（不推荐，性能太差）
推荐直接在 wsl 的发行版中安装 docker。

Ubuntu docker 安装文档 ：[Install Docker Engine on Ubuntu | Docker Documentation](https://docs.docker.com/engine/install/ubuntu/)

# WSL 2

官方文档 [安装 WSL | Microsoft Learn](https://learn.microsoft.com/zh-CN/windows/wsl/install)

关于最佳实践及常见问题：[设置 WSL 开发环境 | Microsoft Learn](https://learn.microsoft.com/zh-CN/windows/wsl/setup/environment#set-up-your-linux-username-and-password)

高级设置：[WSL 中的高级设置配置 | Microsoft Learn](https://learn.microsoft.com/zh-CN/windows/wsl/wsl-config#wsl-2-settings)


----


设置默认使用版本 2 ：wsl --set-default-version 2

查看可在线安装的 wsl 发行版：wsl --list --online

安装：wsl --install -d Ubuntu-22.04


# 配置 WSL 2

可以在 wsl 的发行版中做一些配置，比如自启一些服务等。需要编辑 /etc/wsl.conf 文件。

比如 docker 自启：

```
[boot]
command="service docker start" 
```

配置后需要重新启动生效，wsl --shutdown

## 安装常用软件


```
sudo apt install git curl wget zsh vim net-tools build-essential nmap lsof htop tmux tree ranger fzf -y
```

## 安装 Docker 


```
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    sudo usermod -aG docker $USER
    sudo rm -rf get-docker.sh

```

## 安装 oh-my-zsh


```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

sed -i 's/plugins=(git)/plugins=(git zsh-syntax-highlighting zsh-autosuggestions)/g' ~/.zshrc

source ~/.zshrc

```

## 设置别名简化 sudo 操作


```
code ~/.zshrc 

alias docker="sudo docker"
alias apt="sudo apt"
alias systemctl="sudo systemctl"
alias service="sudo service"
alias mkdir="sudo mmkdir"
alias cp="sudo cp"


source ~/.zshrc
```

## 关于权限  

由于使用的不是 root 用户，所以一些命令需要使用 sudo 进行权限的提升操作，但是注意对于文件或目录的操作，使用 sudo 会更改掉文件或目录的权限（包括所有者，用户组）的设置，谨慎使用。

在 wsl2 中推荐首先建立一个 `/www` 目录用来存放一些个人项目 ，或者最好放在个人的 home 目录下。
然后使用 `sudo chown caoayu: sudo /www` 来设置这个目录的所有者和用户组 
接着使用 `chmod 755 /www -R` 来进行授权。

注意：不要因为方便而设置一些命令别名，如 `cp=sudo cp` 这样的话会使你无法感知到是自己的用户操作还是提升的权限操作，以致于后来的权限出现问题。推荐不设置别名，这样对于超出权限的会提示使用 sudo 命令，这时，我们执行命令后就可以手动去修改文件或目录的权限了。

更多的关于权限介绍 [[]]
## 使用 nvm 管理 node


```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash

source ~/.zshrc 

nvm ls-remote

nvm install v18.16.0

```

## 使用 timeshift 进行系统备份、快照

sudo add-apt-repository -y ppa: teejee2008/timeshift
sudo apt-get update
sudo apt-get install timeshift

使用命令 sudo timeshift-gtk 打开界面。

## 安装 deepin-terminal 

deepin-terminal 是一个简洁美观的 terminal 终端，可以使用这个代替 windows 自带的终端，但是操作 windows 上的目录或命令还是推荐使用 windows 平台的终端，一个是跨文件系统性能问题，二十可能会不兼容导致权限或其他问题。

```
sudo apt install deepin-terminal
```

... 放弃，没有 dde 太丑了也

## 内存占用过高问题


```
sudo su
echo 3 > /proc/sys/vm/drop_caches
echo 2 > /proc/sys/vm/drop_caches
echo 1 > /proc/sys/vm/drop_caches
sync
```

## 常用命令

```bash
sudo apt-get update  更新源
sudo apt-get install package 安装包
sudo apt-get remove package 删除包
sudo apt-cache search package 搜索软件包
sudo apt-cache show package  获取包的相关信息，如说明、大小、版本等
sudo apt-get install package --reinstall  重新安装包
sudo apt-get -f install  修复安装
sudo apt-get remove package --purge 删除包，包括配置文件等
sudo apt-get build-dep package 安装相关的编译环境
sudo apt-get upgrade 更新已安装的包
sudo apt-get dist-upgrade 升级系统
sudo apt-cache depends package 了解使用该包依赖那些包
sudo apt-cache rdepends package 查看该包被哪些包依赖
sudo apt-get source package  下载该包的源代码
sudo apt-get clean && sudo apt-get autoclean 清理无用的包
sudo apt-get check 检查是否有损坏的依赖

```
## 安装常用软件

```Bash
sudo apt install -y gcc g++ vim lsof gdb autoconf automake  neofetch w3m net-tools git wget ca-certificates make zsh w3m

```
## ssh 配置远程连接

```bash
sudo apt-get purge openssh-server -y
sudo apt-get install openssh-server -y
sudo ssh-keygen -A
```

修改 `sudo vi /etc/ssh/sshd_config`

```conf
Port 222
ListenAddress 0.0.0.0
PermitRootLogin yes
PasswordAuthentication yes

```

`sudo service ssh restart`

Windows 宿主机使用 `ssh user@localhost -p 222` 即可登录连接
