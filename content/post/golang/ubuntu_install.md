+++
Categories = []
Description = ""
Tags = []
date = "2015-07-19T16:45:57+08:00"
title = "7 Easy Steps to Install Go (Golang) on Ubuntu"

+++

## 7 Easy Steps to Install Go (Golang) on Ubuntu

Installing Go (Golang) can be tricky on Ubuntu. The repositories for version 12.04 and 14.04 are dated and install older version of Go.

在Ubuntu上安装Go语言需要一些黑科技。在12.04和14.04版本的仓储中Go的版本是已经过时的而且默认安装的是老版本的。

Luckily there is a tool called the Go Version Manager (gvm) to help install, maintain and even switch Go versions. I know it can be a little scary not using ‘apt-get’ or ‘aptitude’, but in this case, it is worth it.

幸运的是有一个叫做Go Version Manager(gvm)的工具可以帮助安装和维护甚至用来切换Go语言的版本。我知道如果不使用‘apt-get’或‘aptitude’可能有点可怕，但是在这个例子里，这是值得的。

The installation is just a clone of a GitHub repo and a single line in your .bashrc.

安装仅需要克隆一个GitHub仓储和在你的.bashrc中加入一行代码即可。

### 1.Clone the Repo and Add to User Directory

    bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)

This command uses cURL to grab the GitHub repo and install it into your user directory. The file that this repo is placed in is ~/.gvm.
