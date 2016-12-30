---
title: Linux 获取进程的完整路径
date: 2016-12-30 14:28:22
tags: [Linux]
---

Linux在启动一个进程时，系统会在/proc下创建一个以PID命名的文件夹，在这个文件夹下面有进程的信息，其中名为exe的文件记录了绝对路径。
```
ps -A

ll /proc/PID
```





