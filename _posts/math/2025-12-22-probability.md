---
layout: post
title:  "Some of my Probability Notes"
date:  2025-12-22 21:00:00 -0500
categories: [math, probability]
tags: [math, probability]
excerpt: Really amazing!
math: true
---

# Continuous Distributions

## Basic Definitions

**PDF ($f(x)$):**
$$
P(X \in B) = \int_B f(x)dx, \quad P(a \le X \le b) = \int_a^b f(x)dx
$$
Properties: $f(x) \ge 0$ and $\int_{-\infty}^{\infty} f(x)dx = 1$.

**CDF ($F(x)$):**
$$
F(x) = P(X \le x) = \int_{-\infty}^x f(y)dy
$$
Relationship: $f(x) = F'(x)$ (if differentiable).

**Expectation & Variance:**
$$
E[X] = \int_{-\infty}^{\infty} x f(x) dx, \qquad E[g(X)] = \int_{-\infty}^{\infty} g(x) f(x) dx
$$
$$
Var(X) = E[(X-\mu)^2] = E[X^2] - (E[X])^2
$$
Linearity: $E[aX+b] = aE[X]+b$, \quad $Var(aX+b) = a^2 Var(X)$.

**Expectation Theorem**
> **Theorem:** For a nonnegative continuous RV ($X \geq 0$):
> $$
> E[X] = \int_0^{\infty} {P(X>x)} dx
> $$

## Uniform Distribution: $X \sim Unif(a, b)$

Definition:
$$
f(x) = \frac{1}{b-a}, \quad a < x < b \quad \text{(0 otherwise)}
$$
CDF:
$$
F(x) = \begin{cases} 
0 & x \le a \\
\frac{x-a}{b-a} & a < x < b \\
1 & x \ge b
\end{cases}
$$
Moments:
$$
E[X] = \frac{a+b}{2}, \qquad Var(X) = \frac{(b-a)^2}{12}
$$

## Normal Distribution: $X \sim N(\mu, \sigma^2)$

Definition:
$$
f(x) = \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(x-\mu)^2}{2\sigma^2}}, \quad -\infty < x < \infty
$$
Standard Normal ($Z \sim N(0,1)$):
$$
Z = \frac{X-\mu}{\sigma}, \quad f(z) = \frac{1}{\sqrt{2\pi}} e^{-z^2/2}
$$

**Properties:**
1. **Symmetry:** $\Phi(-z) = 1 - \Phi(z)$ where $\Phi(z) = P(Z \le z)$.
2. **Probability:** $P(a \le X \le b) = P\left(\frac{a-\mu}{\sigma} \le Z \le \frac{b-\mu}{\sigma}\right) = \Phi(z_b) - \Phi(z_a)$.
3. **Linear Combination:** If $X \sim N(\mu, \sigma^2)$, then $Y = aX+b \sim N(a\mu+b, a^2\sigma^2)$.

## Exponential Distribution: $X \sim Exp(\lambda)$

Definition ($\lambda > 0$):
$$
f(x) = \lambda e^{-\lambda x}, \quad x > 0
$$
CDF:
$$
F(x) = 1 - e^{-\lambda x}, \quad x > 0 \quad (\text{Survival } S(x) = e^{-\lambda x})
$$
Moments:
$$
E[X] = \frac{1}{\lambda}, \qquad Var(X) = \frac{1}{\lambda^2}
$$

**Properties:**
1. **Memoryless:** $P(X > s+t | X > t) = P(X > s) = e^{-\lambda s}$.
2. **Hazard Rate:** $\lambda(t) = \frac{f(t)}{S(t)} = \lambda$ (Constant).

---

# Continuous Distributions 2
*All PDF in this section is not required to remember. You just need to understand and know the relationship between them.*

## Gamma($\alpha,\lambda$)

**Gamma Function:**
$$
\Gamma(\alpha) = \int_0^\infty {t^{\alpha-1}e^{-t}}dt
$$
1. $\Gamma(\frac{1}{2}) = \sqrt{\pi}$
2. $\Gamma(\alpha) = (\alpha-1)!$

Definition:
$$
f(x)=\frac{\lambda^\alpha x^{\alpha-1}e^{-\lambda x}}{\Gamma(\alpha)}, \qquad x>0
$$
Moments:
$$
E[X]=\frac{\alpha}{\lambda},\qquad Var[X]=\frac{\alpha}{\lambda^2},\qquad M_X(t) = (1-\frac{t}{\lambda})^{-\alpha}
$$

**Special cases:**
1. Exponential $exp(\lambda) = \Gamma(1,\lambda)$
2. Chi-square $\chi^2 = \Gamma(\nu/2, 1/2)$

**Properties:**
1. Additive: $X_i \sim \Gamma(\alpha_i, \lambda) \implies \sum X_i \sim \Gamma(\sum \alpha_i, \lambda)$

## Beta($\alpha,\beta$)

**Beta Function:**
$$
Beta(\alpha, \beta) = \int_0^1{t^{\alpha-1} (1-t)^{\beta-1}}dt
$$
1. $Beta(\alpha,\beta) = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$
2. $Beta(\alpha,\beta) = Beta(\beta,\alpha)$ (Symmetry applies to Beta Function, not Beta Distribution)
3. $\int_0^{\frac{\pi}{2}}{2\sin^{2\alpha-1}\cos^{2\beta-1}}dt = {Beta(\alpha,\beta)}$

Definition:
$$
f(x)=\frac{1}{B(\alpha,\beta)}x^{\alpha-1}(1-x)^{\beta-1} ,\qquad 0<x<1
$$
Moments:
$$
E[X]=\frac{\alpha}{\alpha+\beta},\qquad Var[X]=\frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}
$$

**Special cases:**
1. $Beta(1,1) \implies Unif(0,1)$.
2. $Z \sim Beta(p/2,q/2) \implies F = \frac{Z/p}{(1-Z)/q} \sim F(p,q)$
3. $X_1 \sim \Gamma(\alpha_1,\lambda), X_2 \sim \Gamma(\alpha_2,\lambda)\implies \frac{X_1}{X_1+X_2}\sim Beta(\alpha_1,\alpha_2)$
4. iid series $X_i \sim \Gamma(\alpha_i,\lambda) \implies \frac{\sum_{k=1}^{i}X_k}{\sum_{k=1}^{i+1}X_k}\sim Beta(\sum_{k=1}^{i}\alpha_k,\alpha_{i+1})$ and $\sum_{k=1}^{n}X_k \sim \Gamma(\sum_{i=1}^{n} \alpha_i,\lambda)$ independent.

## Chi-squared $\chi^2(\nu)$

Definition:
$$
f(x)=\frac{1}{2^{\nu/2}\Gamma(\nu/2)}x^{\frac{\nu}{2}-1}e^{-\frac{x}{2}} , \qquad x>0
$$
Moments:
$$
E[X]=\nu,\qquad Var[X]=2\nu
$$
Relationship:
$$
\chi^2_\nu \equiv \text{Gamma}\!\left(\tfrac{\nu}{2},\,\tfrac{1}{2}\right)
$$

## Student-$t(\nu)$

Definition via normal and chi–square:
$$
t_\nu=\frac{U}{\sqrt{V/\nu}},\qquad U\sim N(0,1),\; V\sim \chi^2_\nu,\; U\perp V
$$
$$
f_{t_\nu} (x) = \frac{\Gamma(\frac{\nu+1}{2})}{\sqrt{\pi\nu}\Gamma(\frac{\nu}{2})} (1+\frac{x^2}{\nu})^{-\frac{\nu+1}{2}}
$$
Property: Symmetric, heavy tails; as $\nu\to\infty$, $t_\nu\to N(0,1)$. Note that $t_\nu$ has at most $\nu-1$ order moments.

## Cauchy($\theta$)

Definition:
$$
f(x)=\frac{1}{\pi\,[1+(x-\theta)^2]}, \qquad x\in\mathbb{R}
$$
Note: Mean and variance do not exist; $t_1$ is Cauchy$(0)$.

## Log-Normal

$$
X = \log{Y} \sim N(\mu,\sigma^2) \implies Y \sim logNormal
$$
The moments of $Y$ can be derived from the MGF of $X$ (Normal distribution):
$$
E[Y^t] = E[e^{t\log{Y}}] = E[e^{tX}] = e^{\mu t+\frac{1}{2}\sigma^2t^2}
$$

---

# PDF, CDF and Transformation

## Transformation $Y=g(X)$ (continuous, 1–1)

Examples: $Y=X^2$, $Y=1/X$, $Y=e^X$ (handle branches as needed).

* If $Y = g(X)$ and $g$ is monotone:
    $$
    f_Y(y) = f_X(g^{-1}(y)) \left| \frac{d}{dy} g^{-1}(y) \right|, \quad F_Y(y) = P(Y \le y) = P(X \le g^{-1}(y)).
    $$
* For multivariate transformations $(X_1, X_2) \mapsto (Y_1, Y_2)$:
    $$
    f_{Y_1,Y_2}(y_1,y_2) = f_{X_1,X_2}(x_1,x_2) \left| \det \frac{\partial(x_1,x_2)}{\partial(y_1,y_2)} \right|.
    $$
    (Jacobian method applies to multivariate transformations).

## Joint PDF and Marginals

Normalization:
$$
\iint_{\mathbb{R}^2} f(x,y)\,dx\,dy=1
$$
Marginals:
$$
f_X(x)=\int_{-\infty}^{\infty} f(x,y)\,dy,\qquad f_Y(y)=\int_{-\infty}^{\infty} f(x,y)\,dx
$$

## Independence and Correlation

Equivalent conditions:
$$
f(x,y)=f_X(x)f_Y(y)
$$
$$
F(x,y)=F_X(x)F_Y(y)
$$
Conditional PDF under independence:
$$
f_{X|Y}(x|y)=f_X(x)
$$
If independent $\Rightarrow$ uncorrelated. Converse false (except in the Normal case).
$$
\rho(X,Y) = \frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}}
$$

## Conditional PDF (continuous)

Definition:
$$
f_{X|Y}(x|y)=\frac{f(x,y)}{f_Y(y)}
$$
If $X,Y$ are independent then $f_{X|Y}(x|y)=f_X(x)$.

> **Theorem: Poisson Thinning**
> $$Y|X=x \sim Bin(x,p)\quad X\sim Poisson(\lambda) \Rightarrow Y\sim Poisson(\lambda p)$$

## Convolution (sum of independent r.v.s)

If $Z=X+Y$ and $X,Y$ are independent:
$$
f_Z(z)=\int_{-\infty}^{\infty} f_X(x)\,f_Y(z-x)\,dx
$$

---

# Sample and IID Cases
*Assume: without special clarification, $X_1, X_2, \ldots, X_n$ are i.i.d. copies of $X$. $Y$ is a linear combination (e.g. $Y = aX$ or $Y = a_1X_1 + a_2X_2 + \cdots$).*

## Order Statistics

For i.i.d. continuous random variables $X_1, X_2, \ldots, X_n$ with PDF $f(x)$ and CDF $F(x)$:

1.  **Minimum:** $X_{(1)} = \min(X_1, \ldots, X_n)$
    $$
    F_{X_{(1)}}(x) = 1 - [1 - F(x)]^n, \qquad f_{X_{(1)}}(x) = n[1 - F(x)]^{n-1} f(x)
    $$

2.  **Maximum:** $X_{(n)} = \max(X_1, \ldots, X_n)$
    $$
    F_{X_{(n)}}(x) = [F(x)]^n, \qquad f_{X_{(n)}}(x) = n[F(x)]^{n-1} f(x)
    $$

3.  **General order statistic:** for any $1 \le i \le n$
    $$
    f_{X_{(i)}}(x) = \frac{n!}{(i-1)!(n-i)!} [F(x)]^{i-1}[1-F(x)]^{n-i} f(x)
    $$

4.  **Joint order statistic:** for any $1 \le i < j \le n$
    $$
    f_{X_{(i)},X_{(j)}}(x_{(i)}, x_{(j)}) = \frac{n!}{(i-1)!(j-i-1)!(n-j)!} f(x_{(i)})f(x_{(j)}) [F(x_{(i)})]^{i-1}[F(x_{(i)})-F(x_{(j)})]^{j-i-1}[1-F(x_{(j)})]^{n-i-j}
    $$

5.  **Uniform Order Stats $\to$ Beta**
    $$
    U_{(j)}-U_{(i)} \sim Beta(j-i, n-(j-i)+1)
    $$

## Expectation and Variance of Sums

Consider $X_i$ not independent.
$$
E(Y) = \sum a_i E(X_i), \quad Var(Y) = \sum a_i^2 Var(X_i) + 2\sum_{i<j} a_i a_j Cov(X_i, X_j)
$$

---

# Properties of Expectation (Chapter 7)

## Sums and Covariance

**Expectation of Sums:**
$$
E\left[\sum a_i X_i\right] = \sum a_i E[X_i] \quad (\text{Always holds})
$$
**Variance of Sums:**
$$
Var\left(\sum_{i=1}^n a_i X_i\right) = \sum_{i=1}^n a_i^2 Var(X_i) + 2 \sum_{i<j} a_i a_j Cov(X_i, X_j)
$$
If $X_i$ are independent, $Cov(X_i, X_j)=0$, so $Var(\sum X_i) = \sum Var(X_i)$.

**Covariance:**
$$
Cov(X,Y) = E[(X-\mu_X)(Y-\mu_Y)] = E[XY] - E[X]E[Y]
$$
Properties:
1. $Cov(X,Y) = Cov(Y,X)$
2. $Cov(X,X) = Var(X)$
3. $Cov(aX+b, cY+d) = ac Cov(X,Y)$
4. Independence $\implies Cov(X,Y)=0$ (Converse not true unless Multivariate Normal)

**Correlation ($\rho$):**
$$
\rho = \frac{Cov(X,Y)}{\sigma_X \sigma_Y}, \quad -1 \le \rho \le 1
$$

## Conditional Expectation & Variance

**Formulas:**
$$
E[X] = E[E[X|Y]] \quad (\text{Law of Total Expectation})
$$
$$
Var(X) = E[Var(X|Y)] + Var(E[X|Y])
$$
Useful for random sums (e.g., $X = \sum_{i=1}^N X_i$ where $N$ is random).

## Moment Generating Functions (MGF)

Definition: $M_X(t) = E[e^{tX}]$.

1. **Moments:** $E[X^n] = M_X^{(n)}(0)$ ($n$-th derivative at $t=0$).
2. **Uniqueness:** MGF uniquely determines the distribution.
3. **Independence:** If $X, Y$ indep., $M_{X+Y}(t) = M_X(t) M_Y(t)$.

**Common MGFs:**
* Binomial$(n,p)$: $(pe^t + 1-p)^n$
* Poisson$(\lambda)$: $\exp\{\lambda(e^t - 1)\}$
* Uniform $(a,b)$: $\frac{e^{tb}-e^{ta}}{t(b-a)}$ for $t \neq 0$
* Exponential$(\lambda)$: $\frac{\lambda}{\lambda - t}$ for $t < \lambda$
* Normal$(\mu, \sigma^2)$: $\exp\{\mu t + \frac{1}{2}\sigma^2 t^2\}$
* Gamma$(\alpha, \lambda)$: $(\frac{\lambda}{\lambda-t})^\alpha$

---

# Limit Theorems (Chapter 8)

## Inequalities

**Markov's Inequality:** If $X \ge 0$ and $a > 0$:
$$
P(X \ge a) \le \frac{E[X]}{a}
$$

**Chebyshev's Inequality:** For any $k > 0$ (or $\epsilon = k\sigma$):
$$
P(|X - \mu| \ge k) \le \frac{\sigma^2}{k^2} \quad \text{or} \quad P(|X - \mu| \ge k\sigma) \le \frac{1}{k^2}
$$

**Jensen's Inequality:** If $g(x)$ is convex ($g''(x) \ge 0$):
$$
g(E[X]) \le E[g(X)]
$$
Example: $(E[X])^2 \le E[X^2]$ since $g(x)=x^2$ is convex.

## Laws of Large Numbers

Let $X_1, \dots, X_n$ be i.i.d with mean $\mu$.

* **Weak Law (WLLN):** $\overline{X}_n \xrightarrow{P} \mu$ (Convergence in Probability).
    $$\lim_{n \to \infty} P(|\overline{X}_n - \mu| \ge \epsilon) = 0$$
* **Strong Law (SLLN):** $\overline{X}_n \xrightarrow{a.s.} \mu$ (Convergence Almost Surely).
    $$P(\lim_{n \to \infty} \overline{X}_n = \mu) = 1$$

## Central Limit Theorem (CLT)

Let $X_1, \dots, X_n$ be i.i.d with mean $\mu$ and variance $\sigma^2$.
As $n \to \infty$, the sum $S_n$ and mean $\overline{X}_n$ approach Normality.
$$
\frac{\sum X_i - n\mu}{\sigma\sqrt{n}} = \frac{\overline{X}_n - \mu}{\sigma/\sqrt{n}} \sim N(0,1)
$$
Continuity Correction (for Binomial): $P(X \le k) \approx P(Z \le \frac{k+0.5 - np}{\sqrt{npq}})$.