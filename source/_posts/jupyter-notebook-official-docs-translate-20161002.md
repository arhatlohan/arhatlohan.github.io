---
title: Jupyter Notebook官方文档 翻译
date: 2016-10-02 12:09:25
tags: [Python, Jupyter]
---
官方文档：http://jupyter-notebook.readthedocs.io/en/latest/notebook.html

---
## Jupyter Notebook
### 介绍
notebook在一个全新的方向上拓展了基于控制台的方法到交互式计算，提供了一种基于web的应用来记录整个计算过程：开发、编辑、执行代码，同时交互式显示结果。Jupyter notebook 结合了两个部分：
**web应用程序**：一个基于浏览器的交互式文档创作工具，这种交互式文档集说明性文字、数学、计算和富媒体于一体。
**Notebook 文档**: web应用程序中的所有可见内容的表现形式，包括计算的输入输出、说明性文字、数学、图像以及富媒体对象的表示。

#### web应用程序的主要特点
+ 浏览器内部编辑代码，包括自动语法高亮、缩进、tab补全和内省。
+ 从浏览器执行代码的能力，计算的结果附加在生成他们的代码后面。
+ 使用富媒体表示方法显示计算结果，比如HTML，LaTex，PNG，SVG等。例如，[matplotlib](http://matplotlib.org/)出版级质量的图片可以包含在行内。
+ 浏览器内部编辑富文本使用markdown标记语言，可以给代码添加注释，不仅仅是纯文本。
+ 很容易的将使用LaTex的数学符号包含在markdown cell内，或则本地使用[MathJax](http://www.mathjax.org/)生成。

#### Notebook 文档
Notebook 文档包含一个交互式绘画的输入和输出，以及代码的不可执行的附加文本。这样，notebook文件可以作为一个会话完整计算的记录，将说明性文字、数学公式、计算结果的富媒体表示与可执行代码交织在一起。这些文件实质是[JSON](http://en.wikipedia.org/wiki/JSON)文件并以`.ipynb`扩展名保存。由于JSON是一种纯文本格式，因此他们可以受版本控制并与同事分享。

Notebook可以导出为一系列静态格式(static formats)，包括HTML(例如，用于博客文章）、 reStructuredText、LaTeX、PDF和silde shows, 通过[nbconvert](http://nbconvert.readthedocs.org/en/latest/)命令实现。

此外，任何公开网址可用的`.ipynb`文件可以通过Jupyter Notebook Viewer([nbviewer](http://nbviewer.jupyter.org/))共享。nbviewer从URL加载notebook文件，将其呈现为一个静态的web页面。我们可以把这个web页面与同事分享或者作为公共博客的文章，而其它用户不需要安装Jupyter notebook。实际上，[nbviewer](http://nbviewer.jupyter.org/)只是[nbconvert](http://nbconvert.readthedocs.org/en/latest/)的网络服务版本，因此你可以自己使用nbconvert进行静态转换，而不是依赖nbviewer。

### 启动notebook服务器
你可以在命令行中使用以下命令运行notebook服务器：

    jupyter notebook
运行后，控制台将会显示一些关于notebook服务器的信息，同时打开浏览器访问web应用程序的URL(默认地址：`http://127.0.0.1:8888`).

Jupyter notebook web应用程序的登录页，即主面板(dashboard)，显示notebook目录(默认情况下，notebook目录是notebook服务器启动的目录)中当前可用的notebook文件。

你可以使用主面板中`New Notebook`按钮创建新notebook文件，或者单击打开已有的文件。你还可以拖动`.ipynb`文件和Python源码文件`.py`到notebook文件区域。

当你从命令后打开notebook服务器时，你同样可以直接打开特定的notebook文件，而不是通过主面板，使用命令：`jupyter notebook my_notebook.ipynb` .如果没有指定文件扩展名，则会假定扩展名为`.ipynb`.

当你在一个打开的notebook文件里时，使用*File/Open...*菜单选项将会在新选项卡中打开主面板。这样你可以从notebook目录中打开另一notebook文件，或者创建一个新notebook文件。

> 注意：
你可以同时打开多个notebook服务器，如果你想在不同的目录操作notebook文件。默认情况下，第一个服务器使用8888端口，之后启动的服务器自动寻找距离8888最近的端口。你同样可以使用`--port`选项手动指定端口。

#### 创建新的notebook文档
可以在任何时候创建新的notebook文件，从主面板，或者在一个打开的notebook文件中使用*File/New*菜单选项。新notebook文件被放在同一个目录，并在新的浏览器选项卡中打开。在主面板notebook文件列表中可以看到新建的文件。


#### 打开notebooks
一个打开的notebook仅有一个交互式会话连接到[IPython内核](http://ipython.org/ipython-doc/dev/overview.html#ipythonzmq),此内核将会执行用户代码并返回结果。如果web浏览器窗口关闭，内核依然保持活动状态；当你从主面板重新打开同一个notebook时，web应用程序将会再次连接到同一个内核。在主面板，有活动内核的notebook文件旁边有一个`Shutdown`按钮，而没有活动内核的notebook文件旁边是`Delete`按钮。

其它客户端可能连接到相同的底层(underlying)IPython内核。notebook 服务器总是在终端显示如何连接到每一个内核的全部细节，显示如下：

    [NotebookApp] Kernel started: 87f7d2c0-13e3-43df-8bb8-1bd37aaf3373

这个长字符串就是内核的ID，此ID是连接到内核所需要的信息。你同样可以通过运行魔术函数`%connect_info`来获取连接信息。`%connect_info`将会输出相同的ID以及JSON数据结构的内容。
![connect_info_magic.jpg](/sourcepictures/20161002/connect_info_magic.jpg)

然后，你可以手动启动Qt控制台连接到同一个内核，通过传入ID的一部分：

    $ ipython qtconsole --existing 87f7d2c0

如果不输入ID，`--existing`将会连接到最近启动的内核。这也可以通过在notebook中运行魔术函数`%qtconsole`来实现。

### Notebook用户界面
当你创建一个新的notebook文件时，你将会看到notebook名称，菜单栏，工具栏和一个空的代码单元(code cell).
**notebook名称**：notebook文件名称显示在页面的最上方，紧邻`IP[y]: Notebook`标志。这个名字反映`.ipynb`notebook文件的名字。在notebook名称上单击会弹出对话框，你可以对其进行重命名操作。
例如，重命名文件`Untitled0.ipynb`为`My first notebook.ipynb`.
![new-notebook.gif](/sourcepictures/20161002/new-notebook.gif)

**菜单栏**：菜单栏提供了多个选项，可以用来修改notebook的功能。

**工具栏**：工具栏提供了一种快速使用notebook常用操作的方式，单击工具栏图标即可。

**代码单元**：单元(cell)的默认类型，read on for an explanation of cells

> 在notebook 4.1版本，用户界面允许同时选择多个单元。当多个单元被选择，菜单栏中`quick celltype selector`将会显示一个横线`-`，指示选区中的单元的类型可能不一致。`quick celltype selector`可以被用来改变选区的类型，将会改变所有选中单元的类型。

### notebook文件的结构
notebook由一系列的单元组成。单元是一个多行的文本输入区域，它的内容可以使用`Shift+Enter`来执行，或者单击工具栏`Play`按钮，或使用菜单栏*Cell/Run*运行。单元如何执行是由单元的类型决定的。共有四种类型的单元：**代码单元(code cells)**,**markdown单元(markdown cells)**,**纯文本单元(raw cells)**,**标题单元(heading cells)**.每一个单元开始都是代码单元，但它的类型可以通过工具栏下拉框(初始值为`Code`)进行修改，也可以使用键盘[快捷键](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html#keyboard-shortcuts)进行修改。

更多notebook可以实现的功能，请参考[例子](http://nbviewer.jupyter.org/github/jupyter/notebook/tree/master/docs/source/examples/Notebook/).

#### 代码单元(Code cells)
你可以在代码单元里写入或编辑代码，代码单元有语法高亮和自动补全功能。默认情况下，代码单元默认的语言是Python，但是其它语言，例如`Julia`和`R`，可以使用[单元魔术命令](http://ipython.org/ipython-doc/dev/interactive/tutorial.html#magics-explained)来处理。

当一个代码单元被执行时，代码被发送到和notebook连接的内核。计算返回的结果显示在notebook中作为单元的输出(output).输出不仅限于文字，其它很多可能格式都是可行的，包括`matplotlib`图像和HTML表格(例如`pandas`数据分析包使用的表格)。这就是著名的IPython富媒体显示能力。

> 参见：
notebook[富媒体输出(Rich Output)](https://nbviewer.jupyter.org/urls/raw.github.com/ipython/ipython/3.x/examples/IPython%20Kernel/Rich%20Output.ipynb)例子

#### Markdown单元(Markdown cells)
你可以采用方便阅读的方式记录计算过程，交替使用描述性文字(使用富文本)和代码. 在IPython中，这通过Markdown语言标记文本来说完成。相应的单元被称为Markdown单元。Markdown语言提供了一种简单的方式实现文本标记，即指定哪一部分文字应当被强调(斜体)、加粗、构成列表等。

当Markdown单元被执行，Markdown代码被转换成相应的富文本(rich text)。Markdown允许使用任意的HTML代码编辑格式。

在Markdown单元内部，你可以直接包含数学符号：行内数学符号使用标准的LateX标记:`$...$`,行间数学符号使用`$$...$$`标记。当Markdown单元被执行时，LaTeX部分自动生成高质量排版的方程式。[MathJax](http://www.mathjax.org/)使这成为可能，它支持LaTeX功能中的很大一部分。

#### 纯文本单元(Raw cells)

#### 标题单元(Heading cells)




