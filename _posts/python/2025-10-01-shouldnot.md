---
layout: post
title:  "Some Python Phrase you should never write"
date:  2025-10-01 19:00:00 -4
categories: python 
tags: python
excerpt: this may generate security issue
mathjax: true
---

# Example 1

Never write:
```
[[0] * 5] * 10
```

this clause you can only use once, ```[0] * 5```, like this.

But if you use ```[[0] * 5] * 10``` instead of ```[[0]*5 for _ in range(10)]```, that will make your variable sharing to others.


# Example 2

Never write:

```
def append_to(element, to=[]):
    to.append(element)
    return to
```

Instead, you should write:

```
def append_to(element, to=None):
    if to is None:
        to = []
    to.append(element)
    return to
```

This example come from, (https://docs.python-guide.org/writing/gotchas/#mutable-default-arguments)

I met this problem at: [```208. Implement Trie (Prefix Tree)```](https://leetcode.com/problems/implement-trie-prefix-tree/) from leetcode, and my code clip is,

```
class TNode:
    def __init__(self, childs = {}):
        self.childs = childs
        self.isEnd = False
```

I don't know where the element can come from an empty dictionary, that's really crazy. Then I check comments. 


> Create a new object each time the function is called, by using a default arg to signal that no argument was provided (None is often a good choice).
