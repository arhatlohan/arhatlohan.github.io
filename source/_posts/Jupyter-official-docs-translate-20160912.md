---
title: Jupyter官方教程 翻译
date: 2016-09-12 23:07:07
tags: [Python, Jupyter]
---
**缘起**：以前用过Ipython，但是了解不深，偶然机会，想深入学习一下。翻译一下官方的docs，鄙人从来没有翻过东西，英语也忘得差不多了，以前背得GRE单词也忘得差不多了，有错误请见谅。其实算不上翻译，只是把大致的功能与提示写出来，毕竟中文的资料比较少。
从4.0版本开始，Ipython分为ipython和Jupyter。官方网站是这么说的：
> As of IPython 4.0, the language-agnostic parts of the project: the notebook format, message protocol, qtconsole, notebook web application, etc. have moved to new projects under the name **Jupyter**. **IPython itself is focused on interactive Python**, part of which is providing a Python kernel for Jupyter.

---

## 安装 Jupyter Notebook
### 必备：Python
尽管Jupyter可以运行很多的编程语言代码，**Python**是安装Jupyter Noterbook的必备条件（Python3.3以上，或Python2.7）。

### 使用Anaconda和conda安装Jupyter
对于新用户，我们强烈建议安装[Anaconda](https://www.continuum.io/downloads). Anaconda可以很方便的安装Python, Jupyter Notebook以及其它科学计算与数据科学常用的包。
使用下面的安装步骤：
1. 下载Anaconda。我们建议下载Anaconda的最新Python 3的版本。
2. 安装你下载的Anaconda。
3. 恭喜你，你已经安装好了Jupyter Notebook。运行jupyter notebook:
`jupyter notebook`

### 针对有经验的Python用户：使用pip安装Jupyter
>重要提示：Jupyter安装需要Python3.3以上，或者Python2.7. IPython 1.x是支持Python3.2和2.6的最后版本。

作为一个Python用户，你可能想使用Python包管理器pip安装Jupyter,而不是Anaconda。
首先，确保你已经安装了最新版本的pip，旧版本的可能会遇到问题。
`pip3 install --upgrade pip`
然后，安装Jupyter Notebook：
`pip3 install jupyter`
(Use `pip` if using legacy Python 2.) 注：legacy不知怎么翻，“已停产的”？

### 可选的：安装Kernels
接下来，介绍在更高的层次在不同的编程语言中使用Jupyter Notebook。
### 是否有语言是预装的：
是的。安装Jupyter Notebook将会安装[IPython](https://ipython.readthedocs.io/en/latest/) [kernel](http://jupyter.readthedocs.io/en/latest/glossary.html#term-kernel)。这使得我们在notebooks 上使用python编程语言。
### 如何同时安装Python 2 和Python 3 ?
如果要安装其它版本的Python，比如同时使用Python 2和Python 3，请参考IPython文档[安装kernel](https://ipython.readthedocs.io/en/latest/install/kernel_install.html)
### 如何安装其它编程语言，比如R或Julia ?
如要在除Python外的其它语言中使用notebooks, 比如R或者Julia，你必须安装额外的内核。更多信息请参考[可用内核](https://github.com/ipython/ipython/wiki/IPython-kernels-for-other-languages)

---

## 运行 Jupyter Notebook
**内容**
+ 基本步骤
+ 启动Notebook Server
+ 介绍Notebook Server 的命令后选项
  + 如何使用自定义的IP和端口启动Notebook？
  + 如何在不打开浏览器情况下使用Notebook server？
  + 如何获取Notebook server 选项的帮助信息？

### 基本步骤
1. 从命令行启动notebook服务器：
`jupyter notebook`
2. 你应当可以看到notebook开启了你的浏览器。

### 启动Notebook Server
在你安装Jupyter Notebook之后，你已经做好运行notebook服务器的准备。你可以从命令后启动notebook服务器:
`jupyter notebook`
运行命令之后，命令行将会显示一些关于notebook服务器的信息，包括网络应用程序的`URL`地址(默认值：`http://localhost:8888`):
```Python
$ jupyter notebook
[I 08:58:24.417 NotebookApp] Serving notebooks from local directory: /Users/catherine
[I 08:58:24.417 NotebookApp] 0 active kernels
[I 08:58:24.417 NotebookApp] The Jupyter Notebook is running at: http://localhost:8888/
[I 08:58:24.417 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
```
然后使用默认的浏览器打开`URL`地址：

浏览器打开notebook之后，你可以看到Notebook面板，Notebook面板将会显示notebook服务器启动目录中的notebook、文件、子目录列表。
**Notebook 面板**
![Notebook Dashboard](/sourcepictures/20160912/notebook_dashboard.png)

### 介绍Notebook Server 的命令后选项
#### 如何使用自定义的IP和端口启动Notebook？
默认情况下，notebook服务器使用`8888`端口。如果`8888`端口不可用或者被占用，notebook服务器将会寻找下一个可用端口。同样，你可以手动指定一个端口。在下面的例子里，我们设定服务器端口为`9999`：
`jupyter notebook --port 9999`
#### 如何在不打开浏览器情况下使用Notebook server？
启动notebook服务器而不打开浏览器，使用以下命令:
`jupyter notebook --no-browser`
#### 如何获取Notebook server 选项的帮助信息？
notebook服务器提供命令行参数的帮助信息，使用`--help`:
`jupyter notebook --help`

---

## 从IPython Notebook迁移 (Migrating from IPython Notebook)
**内容**
+ 概述
+ 了解迁移过程
  + 自动迁移文件
  + 我的配置文件去哪了？
+ 发现重要文件的位置
  + 配置文件(Configuration files)
  + 数据文件：kernelspecs和notebook扩展
+ 由于Jupyter没有配置文件(profiles)，我应当如何进行自定义设置？
  + 更改Jupyter notebook配置目录
  + 更改Jupyter notebook配置文件
  + 更改kernelspecs
+ 了解安装的变化
  + Notebook 扩展
  + 内核
+ 了解imports的变化

### 概述
[大分割计划(The Big Split)](https://blog.jupyter.org/2015/04/15/the-big-split/)将IPython中各种语言无关( language-agnostic)的组件移动到Jupyter之下。将来，Jupyter将会包含与语言无关的项目,这些项目支持(serve)多种语言。IPython将继续专注于Python和它在Jupyter上的使用。
这篇文章介绍当你从IPython 3迁移到Jupyter时，有哪些变化，以及在需要的时候如何修改代码或配置。

### 了解迁移过程
#### 自动迁移文件
当你第一次运行任何`jupyter`命令时，Jupyter将会执行一次文件自动迁移。自动迁移进程复制文件，而不是移动文件，确保原始文件不变，复制的文件到Jupyter文件目录中。如果需要的话，你可以使用命令`jupyter migrate`再次运行迁移进程.你的自定义配置将会自动迁移，在Jupyter中无需编辑即可使用。将来当你升级或者修改配置文件时，请留意配置文件的位置可能发生了变化。
#### 我的配置文件去哪了？
也被称为“为什么我的配置不起任何作用了？”
Jupyter 从IPython中分离出来，意味着一些文件的位置发生了变化，Jupyter 项目没有把以前IPython的功能全部继承下来。
当你第一次启动Jupyter程序时，相关的配置文件自动拷贝到它们在Jupyter中的新位置。在IPython中的原始配置文件不影响Jupyter的执行。如果你意外编辑了原始的IPython配置文件，那么在Jupyter中你将不会看到期望的效果。你应当检查你正在编辑Jupyter的配置文件，同时你应当重启Jupyter服务器才能看到你期望的效果。

### 发现重要文件的位置
#### 配置文件(Configuration files)
配置文件根据用户的爱好自定义Jupyter。被迁移的文件应当已经被自动拷贝到它们在Jupyter的新位置。下面是文件位置的变化：

|IPython location|Jupyter location|
|------|------|
|`~/.ipython/profile_default/static/custom`|`~/.jupyter/custom`|
|`~/.ipython/profile_default/ipython_notebook_config.py`|`~/.jupyter/jupyter_notebook_config.py`|
|`~/.ipython/profile_default/ipython_nbconvert_config.py`|`~/.jupyter/jupyter_nbconvert_config.py`|
|`~/.ipython/profile_default/ipython_qtconsole_config.py`|`~/.jupyter/jupyter_qtconsole_config.py`|
|`~/.ipython/profile_default/ipython_console_config.py`|`~/.jupyter/jupyter_console_config.py`|

如果想使用一个目录位置而不是默认的`~/.jupyter`，设置`JUPYTER_CONFIG_DIR`环境变量。在设置环境变量之后，你可能需要运行`jupyter migrate`来拷贝文件到目的目录中。
#### 数据文件：kernelspecs和notebook扩展名
数据文件(Data Files)包括用户安装的文件，除了配置文件。例如包括kernelspecs和notebook扩展。和配置文件一样，数据文件同样自动迁移到新的Jupyter目录中。
在IPython 3，数据文件在`~/.ipython`中
在Jupyter，数据文件在各平台适当的位置：
  + OS X: `~/Library/Jupyter`
  + Windows: 位置在环境变量`%APPDATA%`中指定
  + 其它，通常是`$XDG_DATA_HOME`,默认路径`~/.local/share/jupyter`
在以上所有平台，环境变量`JUPYTER_DATA_DIR`可以用来设置明确的位置。
系统层面（system-wide）安装的数据文件没有变化(e.g.`/usr/local/share/jupyter`)。每个用户(Per-user)安装的数据文件位置从`.ipython`变换到各平台适当的位置。
### 由于Jupyter没有配置文件(profiles)，我应当如何进行自定义设置？
尽管IPython有配置文件(profiles)的概念，但是Jupyter没有配置文件(profiles)。
在IPython，配置文件是配置和运行文件的集合。在IPython目录(`~/.ipython`)中，有很多像`profile_default`和`profile_demo`名字的目录。在这些目录里是配置文件(configuration file)(`ipython_config.py, ipython_notebook_config.py`)和运行文件(`history.sqlite, security/kernel-*.json`).配置文件(profiles)可以用来改变IPython的配置。
之前，我们可以使用命令`ipython notebook --profile demo`同时对notebook server和IPython kernel进行配置。但是，在Jupyter中不能同时对其进行配置，就像在IPython 3中不能对其他内核的同时配置。
#### 更改Jupyter notebook配置目录
如果你想改变Jupyter notebook的配置，你可以设置`JUPYTER_CONFIG_DIR`:
```Python
JUPYTER_CONFIG_DIR=./jupyter_config
jupyter notebook
```
#### 更改Jupyter notebook配置文件
如果你只是想改变配置文件，你可以：
```Python
jupyter notebook --config=/path/to/myconfig.py
```
#### 更改kernelspecs
如果你确实想改变IPython的内核文件，你不能通过在服务器命令行实现了。内核参数改变必须通过修改kernelspec来实现。你不用重启服务器就可以做到这一点。Kernelspec的改变在你开启一个新kenel时生效。然而，没有修改Kernelspec的好办法。一个办法是使用`jupyter kernelspec list`找到`kernel.json`文件文件，然后修改它，例如手动修改`kenels/python3/kernel.json`. 另外，[a2km](https://github.com/minrk/a2km)是一个努力使修改内核描述变得更容易的实验性项目。
### 了解安装的变化
#### Notebook 扩展
所有IPython notebook 扩展都被自动迁移到Jupyter中。
IPython Notebook 安装扩展使用：
```Python
ipython install-nbextension [--user] EXTENSION
```
现在，在Jupyter中，安装扩展使用：
```Python
jupyter nbextension install [--user] EXTENSION
```
notebook 扩展将会被安装到系统级的位置(例如：`/usr/local/share/jupyter/nbextensions`)。如果你使用`--user`安装，notebook扩展将会安装到`JUPYTER_DATA_DIR`。手动安装不能通过猜测文件应该安装到哪里来完成。(Installation SHOULD NOT be done manually by guessing where the files should go.)
#### 内核
内核的安装采用和notebook相同的方式。他们将会被自动迁移。
内核描述过去通过以下命令安装：
```Python
ipython kernelspec install [--user] KERNEL
```
现在，通过以下命令安装：
```Python
jupyter kernelspec install [--user] KERNEL
```
默认情况下，内核描述将会安装到一个系统级位置(例如:`/usr/local/jupyter/kernels`)。如果你使用`--user`安装，notebook扩展将会安装到`JUPYTER_DATA_DIR`。手动安装不能通过猜测文件应该安装到哪里来完成。(Installation SHOULD NOT be done manually by guessing where the files should go.)
### 了解imports的变化
IPython 4.0 包含shim来管理依赖(dependency)，所有在IPython 3中可用的导入（import）在IPython 4中继续可用。
一些变化包括：

|**IPython 3**|**Jupyter and IPython 4.0**|
|------|------|
|`IPython.html`|`notebook`|
|`IPython.html.widgets`|`ipywidgets`|
|`IPython.kernel`|`jupyter_client, ipykernel`|
|`IPython.parallel`|`ipyparallel`|
|`IPython.qt.console`|`qtconsole`|
|`IPython.utils.traitlets`|`traitlets`|
|`IPython.config`|`traitlets.config`|

重要变化:
IPython.kernel 变成两个包：
+ jupyter_client: Jupyter 客户端API
+ ipykernel: Jupyter的IPython内核

