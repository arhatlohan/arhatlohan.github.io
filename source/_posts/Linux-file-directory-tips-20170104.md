---
title: Linux 文件与目录使用技巧
date: 2017-01-04 11:43:10
tags: [Linux, Tips]
---

### Linux多个文件中查找指定字符串
```
# find <directory> -type f -name "*.c" | xargs grep "<strings>"

<directory>是你要找的文件夹；如果是当前文件夹可以省略
-type f 意思是只找文件
-name "*.c"  表示只找C语言写的代码，从而避免去查binary；也可以不写，表示找所有文件
<strings>是你要找的某个字符串
```

---

### Linux 在多个文件中批量替换字符串
```
sed -i "s/OldString/NewString/g"  `grep OldString -rl Dir`
```
例如：
将当前目录文件中含有的“unpacked”字符串替换为“mathjax27”
```
sed -i "s/unpacked/mathjax27/g" `grep unpacked -rl `
```











