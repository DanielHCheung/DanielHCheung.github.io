---
layout: post
title:  "DS Note: Trie / Prefix Tree"
date:  2025-10-02 10:00:00 -4
categories: [Data Structure, tree]  
tags: [Data Structure, tree, PrefixTree, string, python]  
excerpt: A Data Structure like search tree, that can used to save and search string.
mathjax: true
---

# LeetCode Problems

[208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree)

[211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure)

[212. Word Search II](https://leetcode.com/problems/word-search-ii)

In previous problem, you should use DFS instead of BFS, or you will TLE. But here (LeetCode 212) if you use DFS you will TLE, still.

# Basic Structure:

Define a trie node like a search tree node, however, it's not enough if you only have ```len(childs) == 0``` to indentify its the leaf node. We care about whether a string "apple" exists while we may have other words, like "app", "application", "appstore". So here we define ```self.isEnd``` for each node, where it's a node we can exit.

By the way, we don't need to storage the letter at the node, it's already saved at its parents for navigation purposes. So we need to define that children's letter here.

```
class TrieNode:
    def __init__(self):
        self.childs = {}
        self.isEnd = False
```

Then here we use insert and search method. It's very similar with binary search tree (BST). Additional step is to note the ```isEnd``` properity for the ending of a word at the node.


```
class Trie:

    def __init__(self):
        self.header = TrieNode()

    def insert(self, word: str) -> None:
        curr = self.header
        for c in word:
            curr.childs[c] = curr.childs.get(c, TrieNode())
            curr = curr.childs[c]
        curr.isEnd = True

    def search(self, word: str) -> bool:
        curr = self.header
        for c in word:
            if c not in curr.childs: return False
            curr = curr.childs.get(c)
        return curr.isEnd
        
```

If we only patch prefix, we don't need to justify if here's the end of the word. So here's the difference:

```
def startsWith(self, prefix: str) -> bool:
    curr = self.header
    for c in prefix:
        if c not in curr.childs: return False
        curr = curr.childs.get(c)
    return True
```