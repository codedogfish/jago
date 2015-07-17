+++
Categories = []
Description = ""
Tags = []
date = "2015-07-17T08:44:55+08:00"
title = "公司VPN配置"

+++

## 公司VPN配置

### 首先要生成SSH Key

这一步基本上就是按照GitHub的[这个教程](https://help.github.com/articles/generating-ssh-keys/)

Pre:

    ll ~/.ssh
    #由于之前公司的GitHub仓储需要开通两步验证，所以需要使用SSH连接GitHub，所以可以看到.ssh目录下有id_rsa.pub文件
    #其实公司VPN开通可以直接就用这个，但是我的Buddy和我说还是最好专门生成一个

1:With Terminal still open, copy and paste the text below. Make sure you substitute in your GitHub email address.

    ssh-keygen -t rsa -b 4096 -C "my work email"
    # Creates a new ssh key, using the provided email as a label
    # Generating public/private rsa key pair.

2:We strongly suggest keeping the default settings as they are, so when you're prompted to "Enter a file in which to save the key", just press Enter to continue.

    Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
    #这里我保存id_rsa_xxx

3:You'll be asked to enter a passphrase.

    Enter passphrase (empty for no passphrase): [Type a passphrase]
    Enter same passphrase again: [Type passphrase again]

4:After you enter a passphrase, you'll be given the fingerprint, or id, of your SSH key. It will look something like this:

    Your identification has been saved in /Users/you/.ssh/id_rsa_xxx.
    Your public key has been saved in /Users/you/.ssh/id_rsa_xxx.pub.
    The key fingerprint is:
    01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db [my work email]

然后将生成的id_rsa_xx.pub也就是公钥和用户名发给负责VPN的同事，让他给我开通

### 配置VPN:

按照同事发给我的压缩包里的README.md开始配置VPN:

    # XXX Office OpenVPN HOWTO

    将 xxx.conf, ca.key, jackyu.crt, jackyu.key 复制到 OpenVPN 配置目录下，让配置生效。

    连接时提示输入密码，此密码是证书的加密密码（见邮件）。

    有问题联系：xxx (xxx@xxx.com) 。

    ## Software

    #### Linux

    See https://help.ubuntu.com/12.04/serverguide/openvpn.html#openvpn-simple-client-configuration.

    #### Mac

    推荐 TunnelBlick (http://www.tunnelblick.net).

    Step 1, 安装 TunnelBlick
    Step 2, 打开设置界面，左侧点击 '+' 号添加
    Step 3, 根据向导导入配置，最后是在在一个空文件夹里，把 xxx.conf, ca.key, jackyu.crt, jackyu.key 复制进去，改名为 xxx.tblk 后，双击导入

    #### Windows

    See http://openvpn.se/.

    ## 通过 VPN 登录跳板机

    ssh -p 18022 jackyu@x.x.x.x

    ## OpenVPN in 虚拟机

    需要在虚拟机里，在添加一块网卡，重启下 openvpn 服务，执行 ifconfig 命令查看是否会多个 tun 的网卡，IP 是 x.x.x 网段的，有就可以直接登录了。

首先安装OpenVPN，我是提供过brew安装的

    brew install openvpn

第一次安装失败，提示它以来另一个软件，按照提示运行安装以来软件后，才安装成功的
至于README中的将四个文件复制到OpenVPN配置目录下，让配置生效，复制了，但是如何让配置生效就不晓得了。。。

其次是安装TunnelBlick，之前就通过brew或是brew cask装好了
首次连接时需要输入密码，坑爹，邮件里发给我的密码竟然是GUID格式的。。。

再是通过VPN登录跳板机

    ➜  ~  ssh -p 18022 jackyu@x.x.x.x
    Permission denied (publickey).

查过之后发现是没有将配置ssh使用我生成的key

### PubKeyAuthentication

#### Set up your client

1.Generate your key

  ssh-keygen

2.Configure ssh to use the key

  vim ~/.ssh/config

3.Copy your key to your server

  ssh-copy-id -i /path/to/key.pub SERVERNAME

### Your config file from step 2 should have something similar to the following:

Host SERVERNAME
Hostname ip-or-domain-of-server
User USERNAME
PubKeyAuthentication yes
IdentityFile ./path/to/key

关键就是第二步，配置完成以后，顺利登上跳板机。
