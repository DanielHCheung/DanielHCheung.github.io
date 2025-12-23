---
layout: post
title: "Some of My Probability Notes"
date: 2025-12-22 21:00:00 -0500
categories: [math, probability]
tags: [math, probability]
excerpt: Probability notes (continuous distributions).
---

# Continuous Distributions

## Basic Definitions

**Probability Density Function (PDF)**  
\[
P(X \in B) = \int_B f(x)\,dx, \qquad
P(a \le X \le b) = \int_a^b f(x)\,dx
\]

Properties:
\[
f(x) \ge 0, \qquad \int_{-\infty}^{\infty} f(x)\,dx = 1
\]

---

**Cumulative Distribution Function (CDF)**  
\[
F(x) = P(X \le x) = \int_{-\infty}^{x} f(y)\,dy
\]

If $F$ is differentiable:
\[
f(x) = F'(x)
\]

---

**Expectation and Variance**

\[
E[X] = \int_{-\infty}^{\infty} x f(x)\,dx
\]

More generally,
\[
E[g(X)] = \int_{-\infty}^{\infty} g(x) f(x)\,dx
\]

\[
Var(X) = E[(X-\mu)^2] = E[X^2] - (E[X])^2
\]

Linearity:
\[
E[aX+b] = aE[X] + b
\]
\[
Var(aX+b) = a^2 Var(X)
\]

---

> **Expectation Theorem (Tail Integral Formula)**  
>
> For a nonnegative continuous random variable $X$,
> \[
> E[X] = \int_0^{\infty} P(X > x)\,dx
> \]

***

## Uniform Distribution

Let $X \sim Unif(a,b)$.

\[
f(x) =
\begin{cases}
\frac{1}{b-a}, & a < x < b \\
0, & \text{otherwise}
\end{cases}
\]

\[
F(x) =
\begin{cases}
0, & x \le a \\
\frac{x-a}{b-a}, & a < x < b \\
1, & x \ge b
\end{cases}
\]

Moments:
\[
E[X] = \frac{a+b}{2}, \qquad
Var(X) = \frac{(b-a)^2}{12}
\]

***

## Normal Distribution

Let $X \sim N(\mu,\sigma^2)$.

\[
f(x) =
\frac{1}{\sqrt{2\pi}\sigma}
\exp\!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right),
\quad -\infty < x < \infty
\]

---

**Standard Normal Distribution**

Define
\[
Z = \frac{X-\mu}{\sigma}
\]

Then $Z \sim N(0,1)$ with PDF
\[
f(z) = \frac{1}{\sqrt{2\pi}} e^{-z^2/2}
\]

---

**Properties**

1. Symmetry:
\[
\Phi(-z) = 1 - \Phi(z)
\]

2. Probability calculation:
\[
P(a \le X \le b)
=
\Phi\!\left(\frac{b-\mu}{\sigma}\right)
-
\Phi\!\left(\frac{a-\mu}{\sigma}\right)
\]

3. Linear transformation:
\[
aX+b \sim N(a\mu+b, a^2\sigma^2)
\]

***

## Exponential Distribution

Let $X \sim Exp(\lambda)$ with $\lambda > 0$.

\[
f(x) = \lambda e^{-\lambda x}, \quad x > 0
\]

\[
F(x) = 1 - e^{-\lambda x}, \quad x > 0
\]

Moments:
\[
E[X] = \frac{1}{\lambda}, \qquad
Var(X) = \frac{1}{\lambda^2}
\]

---

**Memoryless Property**
\[
P(X > s+t \mid X > t) = P(X > s) = e^{-\lambda s}
\]

---

**Hazard Rate**
\[
\lambda(t) = \frac{f(t)}{1-F(t)} = \lambda
\]
# Continuous Distributions II

*All PDFs in this section are not required to be memorized.  
Focus on understanding the relationships between distributions.*

## Gamma Distribution

Let $X \sim \Gamma(\alpha,\lambda)$ with $\alpha>0$, $\lambda>0$.

---

**Gamma Function**
\[
\Gamma(\alpha) = \int_0^\infty t^{\alpha-1} e^{-t}\,dt
\]

Special values:
\[
\Gamma(1/2) = \sqrt{\pi}
\]

For positive integers $n$:
\[
\Gamma(n) = (n-1)!
\]

---

**PDF**
\[
f(x) =
\frac{\lambda^\alpha x^{\alpha-1} e^{-\lambda x}}
{\Gamma(\alpha)},
\quad x>0
\]

---

**Moments**
\[
E[X] = \frac{\alpha}{\lambda}, \qquad
Var(X) = \frac{\alpha}{\lambda^2}
\]

Moment generating function:
\[
M_X(t) = \left(1-\frac{t}{\lambda}\right)^{-\alpha},
\quad t<\lambda
\]

---

**Special Cases**
- $Exp(\lambda) = \Gamma(1,\lambda)$
- $\chi^2_\nu = \Gamma(\nu/2, 1/2)$

---

**Additivity**
If $X_i \sim \Gamma(\alpha_i,\lambda)$ are independent, then
\[
\sum_i X_i \sim \Gamma\!\left(\sum_i \alpha_i, \lambda\right)
\]

***

## Beta Distribution

Let $X \sim Beta(\alpha,\beta)$ with $\alpha,\beta>0$.

---

**Beta Function**
\[
B(\alpha,\beta) = \int_0^1 t^{\alpha-1}(1-t)^{\beta-1}\,dt
\]

Relationships:
\[
B(\alpha,\beta)
=
\frac{\Gamma(\alpha)\Gamma(\beta)}
{\Gamma(\alpha+\beta)}
\]

\[
B(\alpha,\beta) = B(\beta,\alpha)
\]

---

**PDF**
\[
f(x) =
\frac{1}{B(\alpha,\beta)}
x^{\alpha-1}(1-x)^{\beta-1},
\quad 0<x<1
\]

---

**Moments**
\[
E[X] = \frac{\alpha}{\alpha+\beta}
\]

\[
Var(X) =
\frac{\alpha\beta}
{(\alpha+\beta)^2(\alpha+\beta+1)}
\]

---

**Special Cases and Relationships**
- $Beta(1,1) \sim Unif(0,1)$
- If $Z \sim Beta(p/2,q/2)$, then
\[
F = \frac{(Z/p)}{(1-Z)/q} \sim F(p,q)
\]
- If $X_1 \sim \Gamma(\alpha_1,\lambda)$ and
  $X_2 \sim \Gamma(\alpha_2,\lambda)$,
\[
\frac{X_1}{X_1+X_2} \sim Beta(\alpha_1,\alpha_2)
\]

***

## Chi-square Distribution

Let $X \sim \chi^2_\nu$.

---

**PDF**
\[
f(x) =
\frac{1}{2^{\nu/2}\Gamma(\nu/2)}
x^{\nu/2-1} e^{-x/2},
\quad x>0
\]

---

**Moments**
\[
E[X] = \nu, \qquad
Var(X) = 2\nu
\]

---

**Relationship**
\[
\chi^2_\nu
\equiv
\Gamma\!\left(\frac{\nu}{2}, \frac{1}{2}\right)
\]

***

## Student-$t$ Distribution

Let $U \sim N(0,1)$ and $V \sim \chi^2_\nu$, independent.

---

**Definition**
\[
t_\nu = \frac{U}{\sqrt{V/\nu}}
\]

---

**PDF**
\[
f_{t_\nu}(x) =
\frac{\Gamma((\nu+1)/2)}
{\sqrt{\pi\nu}\Gamma(\nu/2)}
\left(1+\frac{x^2}{\nu}\right)^{-(\nu+1)/2}
\]

---

**Properties**
- Symmetric with heavy tails
- As $\nu \to \infty$, $t_\nu \to N(0,1)$
- Finite moments exist only up to order $\nu-1$

***

## Cauchy Distribution

Let $X \sim Cauchy(\theta)$.

---

**PDF**
\[
f(x) =
\frac{1}{\pi\,[1+(x-\theta)^2]},
\quad x \in \mathbb{R}
\]

---

**Properties**
- Mean does not exist
- Variance does not exist
- $t_1$ distribution is a standard Cauchy distribution

***

## Log-normal Distribution

Let
\[
X = \log Y \sim N(\mu,\sigma^2)
\]

Then $Y$ follows a log-normal distribution.

---

**Moments**
For any real $t$,
\[
E[Y^t]
=
E[e^{tX}]
=
\exp\!\left(
\mu t + \frac{1}{2}\sigma^2 t^2
\right)
\]


# PDF, CDF, and Transformations

## Transformation: $Y = g(X)$ (Continuous, One-to-One)

Let $X$ be a continuous random variable with PDF $f_X(x)$.

---

### Monotone Transformation

If $Y = g(X)$ and $g$ is strictly monotone, then

\[
f_Y(y)
=
f_X(g^{-1}(y))
\left|
\frac{d}{dy} g^{-1}(y)
\right|
\]

The CDF can be obtained via
\[
F_Y(y) = P(Y \le y) = P(X \le g^{-1}(y))
\]

Examples:
- $Y = X^2$ (handle branches)
- $Y = 1/X$
- $Y = e^X$

---

### Multivariate Transformation (Jacobian Method)

For a transformation
\[
(X_1,X_2) \mapsto (Y_1,Y_2)
\]

the joint PDF is
\[
f_{Y_1,Y_2}(y_1,y_2)
=
f_{X_1,X_2}(x_1,x_2)
\left|
\det
\frac{\partial(x_1,x_2)}{\partial(y_1,y_2)}
\right|
\]

---

## Joint PDF and Marginal Distributions

Let $(X,Y)$ be a pair of continuous random variables with joint PDF $f(x,y)$.

---

**Normalization**
\[
\iint_{\mathbb{R}^2} f(x,y)\,dx\,dy = 1
\]

---

**Marginal PDFs**
\[
f_X(x) = \int_{-\infty}^{\infty} f(x,y)\,dy
\]

\[
f_Y(y) = \int_{-\infty}^{\infty} f(x,y)\,dx
\]

---

## Independence and Correlation

### Independence

$X$ and $Y$ are independent if and only if

\[
f(x,y) = f_X(x) f_Y(y)
\]

Equivalently,
\[
F(x,y) = F_X(x) F_Y(y)
\]

---

**Conditional PDF under Independence**
\[
f_{X|Y}(x|y) = f_X(x)
\]

---

### Correlation

If $X$ and $Y$ are independent, then they are uncorrelated.
(The converse is false except for the multivariate normal case.)

\[
\rho(X,Y)
=
\frac{Cov(X,Y)}
{\sqrt{Var(X)Var(Y)}}
\]

---

## Conditional PDF (Continuous)

\[
f_{X|Y}(x|y)
=
\frac{f(x,y)}{f_Y(y)}
\]

If $X$ and $Y$ are independent, then
\[
f_{X|Y}(x|y) = f_X(x)
\]

---

> **Poisson Thinning Theorem**
>
> If
> \[
> Y|X=x \sim Bin(x,p),
> \qquad
> X \sim Poisson(\lambda),
> \]
> then
> \[
> Y \sim Poisson(\lambda p)
> \]

---

## Convolution (Sum of Independent Random Variables)

Let $Z = X + Y$, where $X$ and $Y$ are independent continuous random variables.

\[
f_Z(z)
=
\int_{-\infty}^{\infty}
f_X(x) f_Y(z-x)\,dx
\]

This formula is known as the convolution of $f_X$ and $f_Y$.

---

## Sample and IID Assumption

Unless stated otherwise, assume:
\[
X_1, X_2, \ldots, X_n
\quad \text{are i.i.d. copies of } X
\]

Let $Y$ be a linear combination:
\[
Y = a_1 X_1 + a_2 X_2 + \cdots + a_n X_n
\]
# Sample and IID Cases

*Unless otherwise stated, assume  
$X_1, X_2, \ldots, X_n$ are i.i.d. continuous random variables with PDF $f(x)$ and CDF $F(x)$.*

---

## Order Statistics

Let
\[
X_{(1)} \le X_{(2)} \le \cdots \le X_{(n)}
\]
denote the ordered sample.

---

### Minimum

\[
X_{(1)} = \min(X_1,\ldots,X_n)
\]

\[
F_{X_{(1)}}(x)
=
1 - [1-F(x)]^n
\]

\[
f_{X_{(1)}}(x)
=
n[1-F(x)]^{n-1} f(x)
\]

---

### Maximum

\[
X_{(n)} = \max(X_1,\ldots,X_n)
\]

\[
F_{X_{(n)}}(x)
=
[F(x)]^n
\]

\[
f_{X_{(n)}}(x)
=
n[F(x)]^{n-1} f(x)
\]

---

### General Order Statistic

For $1 \le i \le n$,
\[
f_{X_{(i)}}(x)
=
\frac{n!}{(i-1)!(n-i)!}
[F(x)]^{i-1}
[1-F(x)]^{n-i}
f(x)
\]

---

### Joint Distribution of Order Statistics

For $1 \le i < j \le n$,
\[
f_{X_{(i)},X_{(j)}}(x_i,x_j)
=
\frac{n!}{(i-1)!(j-i-1)!(n-j)!}
\]

\[
\cdot
f(x_i) f(x_j)
[F(x_i)]^{i-1}
[F(x_j)-F(x_i)]^{j-i-1}
[1-F(x_j)]^{n-j}
\]

---

### Uniform Order Statistics and Beta Distribution

If $U_1,\ldots,U_n \sim Unif(0,1)$, then

\[
U_{(i)} \sim Beta(i,n-i+1)
\]

and

\[
U_{(j)} - U_{(i)} \sim Beta(j-i, n-j+i+1)
\]

---

## Expectation and Variance of Sums

Let
\[
Y = \sum_{i=1}^n a_i X_i
\]

---

**Expectation**
\[
E[Y] = \sum_{i=1}^n a_i E[X_i]
\]

(This always holds, regardless of dependence.)

---

**Variance**
\[
Var(Y)
=
\sum_{i=1}^n a_i^2 Var(X_i)
+
2 \sum_{i<j} a_i a_j Cov(X_i,X_j)
\]

If $X_i$ are independent, then
\[
Var(Y) = \sum_{i=1}^n a_i^2 Var(X_i)
\]

---

## Covariance and Correlation

\[
Cov(X,Y)
=
E[(X-\mu_X)(Y-\mu_Y)]
=
E[XY] - E[X]E[Y]
\]

Properties:
- $Cov(X,Y) = Cov(Y,X)$
- $Cov(X,X) = Var(X)$
- $Cov(aX+b,cY+d) = ac\,Cov(X,Y)$
- Independence implies zero covariance

---

\[
\rho(X,Y)
=
\frac{Cov(X,Y)}{\sigma_X \sigma_Y},
\qquad -1 \le \rho \le 1
\]

---

## Moment Generating Functions (MGF)

The MGF of $X$ is
\[
M_X(t) = E[e^{tX}]
\]

---

**Properties**
1. $E[X^n] = M_X^{(n)}(0)$  
2. The MGF uniquely determines the distribution  
3. If $X,Y$ are independent:
\[
M_{X+Y}(t) = M_X(t) M_Y(t)
\]

---

### Common MGFs

| Distribution | MGF $M_X(t)$ | Domain |
|---|---|---|
| Binomial $(n,p)$ | $(pe^t + 1-p)^n$ | $t \in \mathbb{R}$ |
| Poisson $(\lambda)$ | $\exp\{\lambda(e^t-1)\}$ | $t \in \mathbb{R}$ |
| Uniform $(a,b)$ | $\frac{e^{tb}-e^{ta}}{t(b-a)}$ | $t \ne 0$ |
| Exponential $(\lambda)$ | $\frac{\lambda}{\lambda-t}$ | $t<\lambda$ |
| Normal $(\mu,\sigma^2)$ | $\exp\{\mu t + \frac{1}{2}\sigma^2 t^2\}$ | $t \in \mathbb{R}$ |
| Gamma $(\alpha,\lambda)$ | $\left(\frac{\lambda}{\lambda-t}\right)^\alpha$ | $t<\lambda$ |
# Inequalities

## Markov Inequality

Let $X \ge 0$ be a random variable and $a>0$. Then
\[
P(X \ge a) \le \frac{E[X]}{a}
\]

---

## Chebyshev Inequality

Let $X$ have mean $\mu$ and variance $\sigma^2$. Then for any $k>0$,
\[
P(|X-\mu| \ge k)
\le
\frac{\sigma^2}{k^2}
\]

Equivalently,
\[
P(|X-\mu| < k)
\ge
1 - \frac{\sigma^2}{k^2}
\]

---

## Jensen's Inequality

If $g$ is convex, then
\[
g(E[X]) \le E[g(X)]
\]

If $g$ is concave, the inequality reverses.

---

## Weak Law of Large Numbers (WLLN)

Let $X_1, X_2, \ldots$ be i.i.d. with
\[
E[X_i] = \mu,
\qquad
Var(X_i) = \sigma^2 < \infty
\]

Define the sample mean
\[
\bar X_n = \frac{1}{n} \sum_{i=1}^n X_i
\]

Then for any $\epsilon > 0$,
\[
\lim_{n\to\infty}
P(|\bar X_n - \mu| > \epsilon) = 0
\]

---

## Strong Law of Large Numbers (SLLN)

\[
P\left(
\lim_{n\to\infty} \bar X_n = \mu
\right) = 1
\]

Strong convergence implies weak convergence.

---

## Central Limit Theorem (CLT)

Let $X_1, \ldots, X_n$ be i.i.d. with
\[
E[X_i] = \mu,
\qquad
Var(X_i) = \sigma^2 < \infty
\]

Then
\[
\frac{\sum_{i=1}^n X_i - n\mu}{\sigma \sqrt{n}}
\;\xrightarrow{d}\;
N(0,1)
\]

Equivalently,
\[
\bar X_n
\approx
N\left(\mu,\frac{\sigma^2}{n}\right)
\quad \text{for large } n
\]

---

## Continuity Correction

For discrete sums approximated by a normal distribution:

\[
P(a \le S_n \le b)
\approx
P(a - 0.5 \le Y \le b + 0.5)
\]

where $Y \sim N(n\mu,n\sigma^2)$.

---

## When CLT Does NOT Apply

CLT may fail when:
- Variance is infinite
- Strong dependence exists
- Heavy-tailed distributions (e.g. Pareto with $\alpha \le 2$)

---

## Law of the Iterated Logarithm (LIL)

If $X_i$ are i.i.d. with mean 0 and variance $\sigma^2$,
\[
\limsup_{n\to\infty}
\frac{\sum_{i=1}^n X_i}
{\sigma\sqrt{2n\log\log n}}
=
1
\quad \text{a.s.}
\]
