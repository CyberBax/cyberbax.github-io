---
title: "My First Post"
date: 2023-10-13
categories: [Hacking, Windows]
tags: [OSEP, Active Directory]
---

## Welcome to My First Blog Post

Hello, world! This is my first post on my new blog.


```python
#!/usr/bin/python3

import requests
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('-u','--user', help='Username to target', required=True)
parser.add_argument('-p','--password', help='Password value to set', required=True)
args = parser.parse_args()

```