+++
Categories = []
Description = ""
Tags = ["brew","launchctl","mac","mongo"]
date = "2015-08-05T22:07:25+08:00"
title = "Mac开机启动"

+++

这个话题是由于每次重启以后，总是要通过mongod启动mongo

次数多了就觉得很傻（想偷懒，偷懒是程序员的美德），所以去查了如何让mongo开机自启动

首先查到说，如果brew安装的mongo会有option来设置其开机启动

于是运行brew info mongo来查看mongo的安装情况

果然除了看到mongo的安装信息以外，还有额外的提示

说到这里，因为我已经按照提示运行相关命令来使得mongo开机启动

所以，现在的brew info mongo也就没有了关于添加mongo开机启动的提示

但是活学活用，这几天才学到可以通过history查看历史执行过的命令

前几天Buddy教我如何发布demo环境，在我电脑上一顿命令敲完，虽然我已经很用心在一边看了

但难免还是会忘，于是也是查的History来学习

就在写这篇博客的时候又学了关于（Ctrl+R redo），本来想通过u来undo一个操作的

结果把文章直接清空了，赶紧查了vim下如何redo，吓出一身冷汗


