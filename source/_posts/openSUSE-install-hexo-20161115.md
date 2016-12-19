---
title: openSUSE 安装Git、Node.js、Hexo
date: 2016-11-15 16:54:26
tags: [openSUSE, Hexo]
---

## 安装Git
`zypper install git`

---
## 安装Node.js
Node.js官方有很详细的帮助，特别是提供了openSUSE官方的链接[Download Node.js via openSUSE one-click](http://software.opensuse.org/download.html?project=devel%3Alanguages%3Anodejs&package=nodejs)
按照指引可以很方便的安装Node.js。
如果不可以，针对42.1版本可以root运行以下代码：
```
zypper addrepo http://download.opensuse.org/repositories/devel:languages:nodejs/openSUSE_Leap_42.1/devel:languages:nodejs.repo
zypper refresh
zypper install nodejs
```
可以通过`node -v`查看nodejs版本

针对42.2版本可以root运行以下代码：
```
zypper addrepo http://download.opensuse.org/repositories/devel:languages:nodejs/openSUSE_Leap_42.2/devel:languages:nodejs.repo
zypper refresh
zypper install nodejs
```

---
## 安装Hexo
`npm install -g hexo-cli`


如果以前有hexo工作目录，那么直接到目录`hexo g`,`hexo s`就可以
不能用`hexo init`

