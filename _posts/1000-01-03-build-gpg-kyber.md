---
layout: default
title: gpg后量子密码环境搭建
---

# 搭建后量子密码应用环境

适用系统: Ubuntu 24.04 LTS 物理机或安装于 win10 和 win11 的 wsl2 、Ubuntu 22.04 LTS 安装于 win10 的 wsl2

## 分区预留

在硬盘逻辑卷尾部分一个略大于内存（例如17000MB）的加密分区，用于擦除明文或在休眠时存放交换文件

## 搭建windows的linux子系统

如果运行 `wsl --install` 显示 WSL 帮助文本，请尝试运行 `wsl --list --online` 以查看可用发行版列表并运行 `wsl --install -d <DistroName>` 以安装发行版。 如果安装过程停在 0.0%，请先运行 `wsl --install --web-download -d <DistroName>` 下载发行版，然后再进行安装。若要卸载 WSL，请参阅[文档](https://learn.microsoft.com/zh-cn/windows/wsl/install)

如果可以使用 Microsoft store ，直接搜索安装即可

### 终端工具
win10建议下载[终端](https://apps.microsoft.com/detail/9n0dx20hk701?hl=zh-CN&gl=CN)

### 默认语言设置
`sudo dpkg-reconfigure locales` 之后会出现一个界面，用空格键选中 `en_US.UTF-8 和 zh_CN.UTF-8` ，然后按Tab键选择"OK"并回车。在接下来的界面中，选择 `zh_CN.UTF-8` 作为系统的默认 locale 。

## 环境搭建

### git设置
```bash
sudo echo TODO：用变量减少手动输入computer@wslORphy的麻烦

sudo apt -y update 
sudo apt -y install vim git git-lfs git-secret

git config --global core.editor vim
git config --global core.quotepath false
git config --global alias.goa 'log --graph --pretty=oneline --abbrev-commit -n 15'
git config --global alias.uiau "update-index --assume-unchanged"
git config --global alias.dt "diff --text"
git config --global user.name "computer@wslORphy"
git config --global user.email "computer@wslORphy.cn"
```

### ssh-keygen
```bash
ssh-keygen -t ed25519 -C "computer@wslORphy.work"




# 按回车3次

ssh-keygen -t ed25519 -f ~/.ssh/root -C "computer@wslORphy.root"
    # 输密码2遍

head ~/.ssh/*.pub  # 上传到git托管平台
ssh -T git@gitee.com
ssh -T git@gitee.root
vim ~/.ssh/config  # 输入以下内容

Host gitee.root
  HostName gitee.com
  User git
  IdentityFile ~/.ssh/root

ssh -vT git@gitee.root
```

### git-secret

### 编译安装gnupg

#### 官方快速构建
```bash
mkdir ~/construct
cd ~/construct
curl -O https://www.gnupg.org/ftp/gcrypt/gnupg/gnupg-w32-2.5.12_20250902.tar.xz
tar xf gnupg-*
cd gnupg-w32-2.5.12

    # Quick build method on Unix
    # 如果从不apt update会提示找不到patchelf
sudo apt -y install build-essential libusb-1.0-0-dev libsqlite3-dev libldap-dev libreadline-dev patchelf  

which pinentry
    # TODO：尝试使用这个带参数的make看能否简化对 ~/.gnupg/gpg-agent.conf 的手动配置
    # make -f build-aux/speedo.mk this-native GPG_CONFIGURE_FLAGS="--with-pinentry-program=`which pinentry`

make -f build-aux/speedo.mk this-native
    # 如果不是 gnupg-w32-n.m.n_somedate.tar.xz 这样的带有lib的包，则改为以下命令，会慢
    # make -f build-aux/speedo.mk native

sudo mkdir -p /usr/local/gnupg25
sudo make -f build-aux/speedo.mk install SYSROOT=/usr/local/gnupg25

```
  and run the binaries like

    /usr/local/gnupg25/bin/gpg

  which will also start any daemon from the same directory. Make sure to stop already running daemons or use a different GNUPGHOME.

手动编译依赖库的方式详见[README](https://github.com/gpg/gnupg/blob/master/README)

#### 环境变量与其他设置
```bash
echo 'export PATH="/usr/local/gnupg25/bin:$PATH"' | sudo tee /etc/profile.d/gnupg25.sh
echo 'alias hfm="SECRETS_GPG_ARMOR=1 git secret hide -vFPm"' >> ~/.bash_aliases
```

#### 运行时错误处理
```
ps aux | grep gpg
    # 如果显示 /usr/bin/gpg-agent --supervised 则停止预装版本
systemctl --user stop gpg-agent.socket
```

#### 配置 gpg-agent
```bash
    # 告诉 GPG Agent 使用哪个 pinentry 程序；如果 .gnupg 目录不存在，先让 gpg 创建一个
/usr/local/gnupg25/bin/gpg --list-keys
    # 编辑配置文件
echo "pinentry-program `which pinentry-curses`" >> ~/.gnupg/gpg-agent.conf 
gpg-connect-agent reloadagent /bye
```
