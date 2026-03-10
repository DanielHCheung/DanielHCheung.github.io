---
layout: post
title: "Algo Note: Binary Search Revisited and Python bisect_left bisect_right"
date:  2026-03-10 12:06:00 -5
excerpt: "Algorithm"
mathjax: true
math: true
hidden: false
categories: [Algorithm]
tags: [Algorithm, binary search, python, c++, leetcode]
---


## bisect FUNCTIONS
```python
import bisect
testArray = [1,2,3,3,3,5,5,6,7,8]

# 1 2
print(bisect.bisect_left(testArray, 2), bisect.bisect_right(testArray, 2))

# 2 5
print(bisect.bisect_left(testArray, 3), bisect.bisect_right(testArray, 3))

# 5 5
print(bisect.bisect_left(testArray, 4), bisect.bisect_right(testArray, 4))
```

```bisect_left``` function find the left bound to insert the value, and ```bisect_right``` function find the right bound to insert the value. If you insert your value at this position, the order of array will maintain ascending. 

The implement of both ```bisect_left``` and ```bisect_right``` are binary search so the time complexity is $O(\log{n})$.

Recall the binary search:

```python
lo = 0
hi = len(a)
while lo < hi:
    mid = (lo + hi) // 2
    if a[mid] < x:
        lo = mid + 1
    elif a[mid] == x:
        return mid
    else:
        hi = mid
return -1
```

Note that, ```lo = 0``` is fine for ```a[lo]``` but ```hi = len(a)``` means you can't ```a[hi]```. Here the search area is $[lo, hi)$ and the right bound is not accessible.

There's another solution with ```lo<=hi``` will be mentioned later.

Let's see how ```bisect_left``` wrote: 

```python
lo = 0
hi = len(a)
while lo < hi:
    mid = (lo + hi) // 2
    if a[mid] < x:
        lo = mid + 1
    else:
        hi = mid
return lo
```

The difference is, it combine cases ```a[mid] == x``` and ```a[mid] > x``` together.

By doing so, it intentionally sacrifices the **early exit mechanism**. Even if the target x is found at the current mid, the algorithm cannot terminate immediately; it must continue to **squeeze the right boundary (hi) to the left** in order to guarantee locating the leftmost occurrence (or the exact insertion point).

Consequently, while its worst-case time complexity remains strictly O(logn), it is more exhaustive and will always require the full logn iterations to converge, rather than being strictly "slower".


```python
lo = 0
hi = len(a)
while lo < hi:
    mid = (lo + hi) // 2
    if x < a[mid]:
        hi = mid
    else:
        lo = mid + 1
return lo
```

It's also the same for the function ```bisect_right``` which combines ```a[mid] == x``` and ```a[mid] < x``` together. The program continue to **squeeze the left boundary (lo) to the right** in order to guarantee locating the rightmost occurrence (or the exact insertion point).

Why we always return ```lo```?

The left index indicates, when ```lo>=hi``` as we exit the loop, and we already found the position we're searching about: left of ```lo``` are elements less than x (less than or equal to x, for ```bisect_right```). Thus this position is what we're looking for. 

## Other idea of binary search.
### different search area
```python
lo = 0
hi = len(a)-1
while lo <= hi:
    mid = (lo + hi) // 2
    if a[mid] < x:
        lo = mid + 1
    elif a[mid] == x:
        return mid
    else:
        hi = mid -1
return -1
```

Now we are searching $[lo, hi]$ we need to write ```hi = mid - 1``` and ```lo <= hi``` instead, as index ```hi``` also being searched.

In this logics, we can rewrite both ```bisect_left``` and ```bisect_right```.

```python
def bisect_left(a, x):
    lo = 0
    hi = len(a)-1
    while lo <= hi:
        mid = (lo + hi) // 2
        if a[mid] < x:
            lo = mid + 1
        else:
            hi = mid -1
    return lo
```


```python
def bisect_right(a, x):
    lo = 0
    hi = len(a)-1
    while lo <= hi:
        mid = (lo + hi) // 2
        if a[mid] > x:
            hi = mid -1
        else:
            lo = mid + 1
            
    return lo
```


```cpp
    int bisect_left(vector<int>& nums, int target) {
        int lf = 0, rt = nums.size()-1, m = lf + (rt-lf)/2;
        while (lf <= rt) {
            m = lf + (rt-lf)/2;
            if (nums[m] < target){
                lf = m+1;
            }else{
                rt = m-1;
            }
        }
        return lf;

    }
```


```cpp
    int bisect_right(vector<int>& nums, int target) {
        int lf = 0, rt = nums.size()-1, m = lf + (rt-lf)/2;
        while (lf <= rt) {
            m = lf + (rt-lf)/2;
            if (nums[m] <= target){
                lf = m+1;
            }else{
                rt = m-1;
            }
        }
        return lf;

    }

```

### avoid overflow

When you have very large index number, don't write ```(lo+hi)/2``` to avoid two number added overflow, (this is very important for C++) . You should write this instead: ```mid = lo + (hi-lo)/2```


# Reference

https://docs.python.org/3/library/bisect.html