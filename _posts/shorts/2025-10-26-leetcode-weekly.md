---
layout:     post
title:      "Leetcode contests: Biweekly 168 + Weekly 473"
date:       2025-10-26 11:10:00   -0800
author:     "Daniel"
hidden:     false
tags:
    - shorts
---

## Leetcode contest

![LeetCode Stats](https://leetcard.jacoblin.cool/DanielHCheung?theme=light&font=Esteban&ext=contest)

I took Leetcode contest yesterday, Biweekly 168 and Weekly 473. I solve 3 in Biweekly and 2 in Weekly, and I get TLE/MLE on rest questions. At least, I got bad idea, it's much better than weeks before, I never got idea on hard questions!

<!-- ![img](/img/anything/leetcode251026.png) -->

### Biweekly 168

#### 3722. Lexicographically Smallest String After Reverse

brute force! very easy

#### 3723. Maximize Sum of Squares of Digits

still very easy, just allow part of digits to be as higher as possible!

#### 3724. Minimum Operations to Transform Array

not hard, the number of operations is, the number diff of all elements from two arrays, 1 append, and the minimal diff of ```nums2[-1]``` with previous elements.

```
class Solution:
    def minOperations(self, nums1: List[int], nums2: List[int]) -> int:
        mindiff = min((0 if min(x,y)<= nums2[-1]<=max(x,y) else min(
            abs(x-nums2[-1]), abs(y-nums2[-1])
        )) for x,y in zip(nums1, nums2[:-1]))

        return sum(abs(x-y) for x,y in zip(nums1,nums2[:-1])) +1 + mindiff
```


#### 3725. Count Ways to Choose Coprime Integers from Rows

This problem looks simple at first glance but is actually quite tricky.  
The task is: given a matrix ```mat``` of size ```n × m```, you must count how many ways to choose one element from each row such that the **GCD of all chosen numbers equals 1**.



##### My First Attempt: DFS + Pruning
Since `n` and `m` are both ≤ 150, my first idea was to use DFS.  
During the DFS, if the current GCD becomes 1, we can immediately stop searching deeper — because no matter what we choose in the remaining rows, the final GCD will stay 1.  
So we can directly add

(\text{elements in each row})^{\text{remaining rows}}

to the answer.

This approach works conceptually, but it still **TLEs** because the search space is exponential — up to \(150^{150}\) combinations — even with pruning.

---

##### Step 2: Transforming into DP
After the contest, I asked ChatGPT for help, and the discussion led to a **Dynamic Programming** (DP) approach.

Let’s define the state:

dp[row][g] = number of ways to reach row i with gcd g

Then the transition looks like this:

$$dp[i][new_g] += dp[i-1][g]$$

where

$$new_g = gcd(g, mat[i][j])$$

This means: from every GCD value `g` in the previous row, we combine it with the current element `x = mat[i][j]` to get a new GCD.  
At the end, all ways where `g = 1` are counted as valid.

---

##### Step 3: Optimization
The first DP version still got TLE because it iterated over all 150 possible GCDs even when most of them were zero.  
To speed up, we can store only the **existing GCD states** using a dictionary (`defaultdict(int)` in Python).

The optimized version becomes:

from math import gcd
from collections import defaultdict

class Solution:
    def countCoprime(self, mat):
        MOD = 10**9 + 7
        n, m = len(mat), len(mat[0])
        
        dp = defaultdict(int)
        for x in mat[0]:
            dp[x] += 1

        for i in range(1, n):
            newdp = defaultdict(int)
            for g, cnt in dp.items():
                for x in mat[i]:
                    newdp[gcd(g, x)] = (newdp[gcd(g, x)] + cnt) % MOD
            dp = newdp

        return dp[1] % MOD

---

##### Step 4: Time and Space Complexity

- **Time Complexity:**  
  On each row, we iterate through at most `m × k` pairs,  
  where `k` is the number of distinct GCD states (usually ≤ 60).  
  So total complexity ≈ **O(n × m × k)**,  
  which is roughly **O(10⁶)** in the worst case — easily fast enough.

- **Space Complexity:**  
  Each `dp` stores at most `k` GCD states per row,  
  so **O(k)** ≈ **O(150)**, which is negligible.

---

##### Step 5: Key Insights
1. When `gcd == 1`, you can stop early — that’s the intuition behind the DFS pruning idea.
2. Converting to DP allows us to reuse intermediate results instead of exploring the same paths repeatedly.
3. Storing only non-zero states (via dictionary) gives a big performance boost.

---

##### Final Thoughts
This problem is a great example of how **number theory** and **DP optimization** come together.  
You start with a brute-force search, realize the structure, then compress it into a manageable state space using GCD transitions.

Even though it’s a “150×150” problem, it’s not about the matrix size — it’s about recognizing that **the number of distinct GCDs is small**.


### Weekly 473

#### 3726. Remove Zeros in Decimal Representation

very easy and in 1 sentence
```
class Solution:
    def removeZeros(self, n: int) -> int:
        return int(str(n).replace('0',''))
```
#### 3727. Maximum Alternating Sum of Squares

also very easy, just sort and search from two sides, use left and right index.


#### 3728. Stable Subarrays With Equal Boundary and Interior Sum



#### 3729. Count Distinct Subarrays Divisible by K in Sorted Array


## Further ideas

Work hard and practice every day! You can learn a lot from it!