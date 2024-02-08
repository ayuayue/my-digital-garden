---
{"dg-publish":true,"permalink":"/blog//multipass/","title":"MultiPass使用","tags":["IT/Linux"],"noteIcon":"1","created":"2023-05-28T13:40:53+08:00"}
---

# Multipass

https://multipass.run/

## 安装


```

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All

multipass launch docker --name=docker-dev

multipass set client.primary-name=docker-dev

multipass set local.privileged-mounts=true

```

## 设置|重置密码

sudo passwd ubuntu 

sudo passwd root

## 设置中文

在 Ubuntu 系统中，确保系统能够正确显示中文字符集通常涉及以下几个步骤：

安装中文语言包：
打开终端，输入以下命令来安装中文语言包：

sudo apt-get update
sudo apt-get install language-pack-zh-hans
这将安装简体中文语言包。如果你需要繁体中文，可以使用：

sudo apt-get install language-pack-zh-hant
配置系统语言：
安装语言包后，你可以使用以下命令来配置系统语言：

sudo dpkg-reconfigure locales
在弹出的界面中，选择 zh_CN.UTF-8 或 zh_TW.UTF-8（根据你的需求选择简体中文或繁体中文），然后按 Tab 键选择 Ok，再按 Enter 键确认。

设置环境变量：
编辑 /etc/environment 文件，确保以下行存在（如果不存在，你可以添加它们）：

LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN:zh"
这将设置系统默认的语言环境为简体中文。对于繁体中文，相应的设置应该是：

LANG="zh_TW.UTF-8"
LANGUAGE="zh_TW:zh"
保存并关闭文件后，你可以使用以下命令使更改立即生效：

source /etc/environment
安装中文字体：
为了确保中文能够正确显示，你可能还需要安装中文字体。可以使用以下命令安装常用的中文字体：

sudo apt-get install fonts-wqy-microhei fonts-wqy-zenhei
这将安装文泉驿的微米黑和文泉驿正黑字体。

重启系统：
完成以上步骤后，重启你的系统以确保所有更改生效。

测试中文显示：
重启后，你可以尝试打开一个文本编辑器，输入中文字符，或者查看系统菜单和提示信息，确认中文是否能够正常显示。

请注意，如果你在图形界面下遇到中文显示问题，可能还需要检查桌面环境的设置，确保它支持中文显示。如果你使用的是 GNOME 桌面环境，可以在“设置”中找到“区域与语言”设置，确保系统语言和输入法设置正确。

## 挂载目录


```
multipass mount E:\project docker-dev:/mnt/
```

## 共享目录 smb


```
New-SmbShare -Name "share_name" -Path "C:\my_path"

```

## zplug


```
apt install zsh gawk git -y
chsh -s =zsh

curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh

sudo apt install fonts-font-awesome

git clone --depth=1 https://github.com/romkatv/nerd-fonts.git
cd nerd-fonts
./build 'Meslo/S/*'


vim ~/.zshrc

source ~/.zplug/init.zsh

# History config
HISTSIZE=10000
SAVEHIST=10000
HISTFILE=~/.zsh_history

# zplug plugins
zplug "romkatv/powerlevel10k", as:theme, depth:1
zplug 'zplug/zplug', hook-build:'zplug --self-manage'
zplug "zsh-users/zsh-completions"
zplug "zsh-users/zsh-history-substring-search"
zplug "zsh-users/zsh-autosuggestions"
zplug "zdharma/fast-syntax-highlighting"
zplug "zpm-zsh/ls"
zplug "plugins/docker", from:oh-my-zsh
zplug "plugins/composer", from:oh-my-zsh
zplug "plugins/extract", from:oh-my-zsh
zplug "lib/completion", from:oh-my-zsh
zplug "plugins/sudo", from:oh-my-zsh
zplug "b4b4r07/enhancd", use:init.sh

# Install packages that have not been installed yet
if ! zplug check --verbose; then
    printf "Install? [y/N]: "
    if read -q; then
        echo; zplug install
    else
        echo
    fi
fi
zplug load
```


## 1panel 共享目录

在 ubuntu 中

ln -s /opt/1panel/apps/openresty/openresty/ www/sites/ / www/wwwroot

在 windows 中

multipass mount D:\thinks docker-dev:/www/wwwroot


## 固定 IP

默认会在 `hosts.ics` 文件中添加一个 `*.mshome.net` 的域名。但是 ip 是动态的。如果需要映射多个自定义域名，就需要静态的 ip 了。
打开 hyperv 虚拟机管理器，添加一个虚拟交换机。

![](https://i0.hdslb.com/bfs/article/899137d59b0ef5faeb0b3da5b9fc3710109011082.png)
![](https://i0.hdslb.com/bfs/article/31220e87607b54d8800b18c175692221109011082.png)

给虚拟机添加网络驱动器
![](https://i0.hdslb.com/bfs/article/60c7745ee8052daacc5898ec200e7948109011082.png)
![../../Attachment/Multipass-20240208115713056.png](/img/user/Attachment/Multipass-20240208115713056.png)

应用，确定后进入虚拟机 shell

修改网络配置文件

sudo vi /etc/netplan/50-cloud-init.yaml

新增一个 `eth1`，`eth0` 不要改动。

文件内容如下：


```
# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    ethernets:
        eth0:
            dhcp4: true
            match:
                macaddress: 52:54:00:6e:f4:47
            set-name: eth0
        eth1:
            addresses:
                - 192.168.2.128/24  # 希望固定的ip地址，需要跟虚拟交换机在一个网关内
            nameservers:
                addresses: [8.8.8.8,8.8.4.4]  # 谷歌的dns解析服务器
            routes:
                - to: default
                  via: 192.168.2.1  # 网关，也就是添加的那个虚拟交换机的网关地址
    version: 2

```

虚拟交换机的 ip 及网关可以在 windows 的终端中，使用 `ipconfig` 命令输出。

`sudo netplan --debug apply` 检查配置是否成功。
如果没有 error 出现，那么重新进入 shell 执行 `ifconfig` 即可看到 `eth1` 的网卡信息。
在 windows 上也可以在 hosts 文件中进行映射固定的 ip -> 自定义域名
