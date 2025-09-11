---
layout: post
title:  "Amazing proof methods on Permutations"
date:  2025-09-10 21:00:00 -4
categories: math probability
tags: math probability
excerpt: Really amazing proof!
mathjax: true
---

The problems come from the book ```A First Course in Probability``` by Sheldon Ross. But I am really sorry since I forgot where the solution I saw, maybe another book, Wikipedia, or maybe some other online resources.

Okay, let's turn back to the permutations.


## Formula 1
**Statement** (for $n \geq 1$):

$$ \sum_{k=0}^{n} (-1)^k \binom{n}{k} = 0 $$ 

**Proof**: By the Binomial Theorem,

$$ (1 + x)^n = \sum_{k=0}^{n} \binom{n}{k} x^k $$

Let $x = -1$:

$$ (1 - 1)^n = 0^n = \sum_{k=0}^{n} \binom{n}{k} (-1)^k $$

For $n \geq 1$, the left-hand side is $0$. Hence the formula holds.


## Formula 2
**Statement** (for $ n\geq 0$):

$$ \sum_{k=0}^{n} k \binom{n}{k} = n \cdot 2^{\,n-1} $$

**Proof**: Starting from the Binomial Theorem,

$$
(1 + x)^n = \sum_{k=0}^{n} \binom{n}{k} x^k
$$

Differentiate both sides with respect to $x$:

$$
n(1 + x)^{n-1} = \sum_{k=0}^{n} k \binom{n}{k} x^{k-1}
$$


Set $x = 1$:

$$
n \cdot (1 + 1)^{n-1} = \sum_{k=0}^{n} k \binom{n}{k}
$$

Thus, the formula is proven.

Of course, you can start from this formular:

$$
(x + y)^n = \sum_{k=0}^{n} \binom{n}{k} x^{k} y^{n-k}
$$

Differentiate both sides with respect to $x$:

$$
n(x + y)^{n-1} = \sum_{k=0}^{n} k \binom{n}{k} x^{k-1} y^{n-k}
$$

Then let $x=y=1$, that also make sense.


## Formula 3
**Statement** (for $n \geq$ 2):

$$
\sum_{k=0}^{n} (-1)^{k+1} k \binom{n}{k} = 0
$$

**Proof**: Using the same idea as Formula 2,

$$
\sum_{k=0}^{n} k \binom{n}{k} x^{k-1} = n (1 + x)^{n-1}
$$

Substitute $x = -1$:

$$
\sum_{k=0}^{n} k \binom{n}{k} (-1)^{k-1} = n \cdot (1 - 1)^{n-1} = 0
$$

for $n \geq 2$. Therefore, we have

$$
\sum_{k=0}^{n} (-1)^{k+1} k \binom{n}{k} = 0
$$

