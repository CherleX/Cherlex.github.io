---
layout: post
title:  "尝试挑战 Python Challenge"
date:   2016-09-28 18:12:26
categories: Python
tags: Python Challenge
---

* content
{:toc}
Python Challenge 前三关。


# The Python Challenge



## Level 0

```python
2**38
```

## Level 1

```python
import string

l = string.ascii_lowercase

m = """g fmnc wms bgblr rpylqjyrc gr zw fylb. rfyrq ufyr amknsrcpq ypc dmp.
bmgle gr gl zw fylb gq glcddgagclr ylb rfyr'q ufw rfgq rcvr gq qm jmle.
sqgle qrpgle.kyicrpylq() gq pcamkkclbcb. lmu ynnjw ml rfc spj."""
t = m.maketrans(l, l[2:] + l[:2])
print(m.translate(t))

print("map".translate(t))

```



## Level 2

```python
text = ''
pattern = re.compile('[a-zA-Z]')
result = pattern.findall(text)
print(''.join(result))
```



## Level 3

```python
import re
import urllib.request


def next_page(p):
    url = 'http://www.pythonchallenge.com/pc/def/linkedlist.php?nothing=%s' % p
    with urllib.request.urlopen(url) as url:
        text = url.read()
        m = re.match(r'.*and the next nothing is ([0-9]+)', text.decode("utf-8"))
        if not m: print(text,p)
        return m.group(1)

p = 12345
next_page(p)
for i in range(400):
    p = next_page(p)
```

