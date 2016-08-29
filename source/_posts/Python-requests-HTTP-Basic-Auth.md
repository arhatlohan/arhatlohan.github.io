---
title: Python requests HTTP Basic Auth
date: 2016-01-14 15:33:54
tags: Python
---

Sample from Python scrawl book:
``` python
import requests
from requests.auth import HTTPBasicAuth
auth = HTTPBasicAuth("username", "password")
r = requests.post(url="http://pythonscraping.com/pages/auth/login.php", auth=auth)
print r.text
```

Sample From Requests Docs:
``` python
from requests.auth import HTTPBasicAuth
requests.get("http://pythonscraping.com/pages/auth/login.php", auth=HTTPBasicAuth("username", "password"))
print r.text

\# simple one
from requests.auth import HTTPBasicAuth
r = request.get("http://pythonscraping.com/pages/auth/login.php", auth=("username", "password"))
print r.text
```