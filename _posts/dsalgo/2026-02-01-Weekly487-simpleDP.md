---
layout: post
title: "LeetCode 3830 | Weekly 478.4 Hard | Longest Alternating Subarray After Removing At Most One Element"
date:  2026-02-01 12:06:00 -5
excerpt: "Simple DP"
mathjax: true
math: true
hidden: false
categories: [Algorithm, DP]
tags: [Algorithm, DP, python, leetcode]
---

[LeetCode 3830 Longest Alternating Subarray After Removing At Most One Element](https://leetcode.com/problems/longest-alternating-subarray-after-removing-at-most-one-element/description/)

# Intuition & Approach

## Step 1: Subproblem

What is the purpose of this problem? increase, decrease, increase, decrease...

At a certain $i \in [0,n)$, we consider the left and right add together. If 1 is allowed to remove, then compare $nums[i-1]$ with $nums[i+1]$

We are trying to label such subarray by using 4 1-d array: to label increase or decrease from left or right.

## Step 2: DP equation

Here we define, $Li$ means Left Increase, as 1 increased if $nums[i]>nums[i-1]$: 
$$
Li[i] = \left\{ \begin{array}{cl}
Ld[i-1]+1 & : \ nums[i]>nums[i-1] \\
1 & : \ otherwise
\end{array} \right.
$$
we can also define:
$$
Ld[i] = \left\{ \begin{array}{cl}
Li[i-1]+1 & : \ nums[i]<nums[i-1] \\
1 & : \ otherwise
\end{array} \right.
$$


Also define from right side: (here I use, observe from right side $i$ to $i-1$)

$$
Ri[i-1] = \left\{ \begin{array}{cl}
Rd[i]+1 & : \ nums[i-1]>nums[i] \\
1 & : \ otherwise
\end{array} \right.
$$

$$
Rd[i-1] = \left\{ \begin{array}{cl}
Ri[i]+1 & : \ nums[i-1]<nums[i] \\
1 & : \ otherwise
\end{array} \right.
$$

## Step3: to answer

1. Consider no element removed, that is

$$max(Ld[i]+Rd[i], Li[i]+Ri[i]) -1$$
since there's always one repeatly counted at $i$

2. Consider 1 element removed, that is a little bit completed: max of these two answer.

$$ max(Li[i-1]+Rd[i+1] \text{ if } nums[i-1] > nums[i+1])  $$ 

Also for another case:

$$ max(Ld[i-1]+Ri[i+1] \text{ if } nums[i-1] < nums[i+1])  $$ 

without -1 since no repeat counted.


Why? consider a series 1,2,3, from $i-1$ to $i+1$. 2 should be removed. Hence, we have 1,3 as an increase subsequence. From left hand, we must have decrease; from right hand, we must have increase, that's how second formular comes. The first equation comes from an opposite case.


# Complexity
- Time complexity: $\Theta(n) $ since we only operate on 1d dimention.

- Space complexity: $\Theta(n) $ since we only create 1d array.

# Code
```python3 []
class Solution:
    def longestAlternating(self, nums: List[int]) -> int:
        n = len(nums)
        Ld = [1] * n
        Li = [1] * n
        Rd = [1] * n
        Ri = [1] * n

        for i in range(1, n):
            Li[i] = (Ld[i-1]+1) if nums[i]>nums[i-1] else 1
            Ld[i] = (Li[i-1]+1) if nums[i]<nums[i-1] else 1
            
        for i in range(n-1, 0, -1):
            Ri[i-1] = (Rd[i]+1) if nums[i-1]>nums[i] else 1
            Rd[i-1] = (Ri[i]+1) if nums[i-1]<nums[i] else 1   

        ans = 0
        for i in range(n):
            ans = max(ans, Li[i]+Ri[i]-1, Rd[i]+Ld[i]-1)

        for i in range(1, n-1):
            ans = max(ans, 
                      Li[i-1]+Rd[i+1] if nums[i-1] > nums[i+1] else 0,
                      Ld[i-1]+Ri[i+1] if nums[i-1] < nums[i+1] else 0,
                      
                     )

        return ans
```