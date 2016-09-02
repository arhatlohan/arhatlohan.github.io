---
title: Linux 温习(二)
date: 2016-09-01 20:36:23
tags: Linux
---

## 环境变量
echo $variabename  读取变量的值，$表示引用一个变量的值
环境变量三种，涉及三个命令:set env export

|命令|说明|
|----|----|
|set |显示当前shell的变量，包括当前用户的变量|
|env |显示当前用户的变量|
|export|显示当前导出成用户变量的shell变量|

**添加自定义路径到环境变量**
    PATH=$PATH:/home/test
注意要使用绝对路径

在每个用户的home目录中有一个Shell每次启动都会默认执行的一个配置脚本，以初始化环境，包括添加一些用户自定义环境变量。zsh的配置文件是<font color="Crimsom" size=3>.zshrc</font>, 相应BASH的配置文件是<font color="Crimsom" size=3>.bashrc</font>。可以使用下面的方式添加环境变量：
    echo "PATH=$PATH:/home/test" >> .zshrc

**环境变量删除：**
   unset varname

**source命令：**
source命令也称为“点命令”，也就是一个点符号（.）,是bash的内部命令。
功能：使Shell读入指定的Shell程序文件并依次执行文件中的所有语句
source命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录。
用法：
    source filename 或 . filename


## 文件搜索

whereis　查看文件的位置
which　　查看可执行文件的位置
locate　 配合数据库查看文件位置
find　　 实际搜索硬盘查询文件名称


*whereis*查找的速度非常快，这是因为*linux*系统会将所有文件都记录在一个数据库文件中，当使用*whereis*和*locate*时，会从数据库中查找数据，而不是像find命令那样，通 过遍历硬盘来查找，效率自然会很高。 
但是该数据库文件并不是实时更新，默认情况下时一星期更新一次，因此，我们在用*whereis*和*locate*查找文件时，有时会找到已经被删除的数据，或者刚刚建立文件，却无法查找到，原因就是因为数据库文件没有被更新。

*which*是通过*PATH*环境变量到该路径内查找可执行文件，所以基本的功能是寻找可执行文件

find
find [path] [option] [action]
时间参数：

|参数|说明|
|----|----|
|-atime |最后的访问时间|
|-ctime |创建时间|
|-mtime|最后修改时间|
e.g:
- -mtime n: n 为数字，表示为在n天之前的”一天之内“修改过的文件
- -mtime +n: 列出在n天之前（不包含n天本身）被修改过的文件
- -mtime -n: 列出在n天之内（包含n天本身）被修改过的文件
- newer file: file为一个已存在的文件，列出比file还要新的文件名

注意：数字位置表示过去的天数，数字为负表示将来的天数，0表示今天
