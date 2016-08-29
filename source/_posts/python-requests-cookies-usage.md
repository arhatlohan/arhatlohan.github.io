---
title: python requests 模块中cookies 的使用方法
date: 2016-01-14 15:37:00
tags: Python
---

Simple One:适用cookie 不会变化的情形
``` python
import requests

params = {'username': 'Ryan',\
           'password': 'password'}
r = requests.post("http://pythonscraping.com/pages/cookies/welcome.php", data=params)
print "Cookie is set to:"
print r.cookies.get_dict()
print "-----------------"
print "Going to profile page..."
r = requests.get("http://pythonscraping.com/pages/cookies/profile.php", cookies = r.cookies)
print r.text
```


Complex One:适用于cookie可能会被修改的情况下, 使用request.Session
``` python
import requests

sess = requests.Session()
params = {'username': 'Ryan',\
           'password': 'password'}
s = sess.post("http://pythonscraping.com/pages/cookies/welcome.php", data=params)
print "Cookie is set to:"
print s.cookies.get_dict()
print "----------------"
print "Going to profile page..."
s = sess.get("http://pythonscraping.com/pages/cookies/profile.php")
print s.text
```