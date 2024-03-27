# stat400 / exam02

## 3.3 ~ expected value (discrete rvs).

Given some discrete random variable $X$ that has pf $p(x)$ and set of possible values $D$, the **expected value** of $X$ is the weighted average of all possible values of $X$:
$$
E(x) = \mu_X = \sum_{x \in D} x \cdot p(x)
$$
Sometimes we want to find the expected value of a function of a random variable, or $E(h(X))$ for some function $h$. Deriving the following formula is pretty simple:
$$
E(h(X)) = \sum_{x \in D} h(x) \cdot p(x)
$$
In the case of a linear function $h(X) = aX + b$, we can use a shortcut formula. This is also easily derivable by manipulating the sum in the $E(x)$ definition.
$$
E(aX + b) = aE(x) + b
$$
 The **variance** of some rv $X$ is a measure of the distribution's variability. It is also the square of the **standard deviation**.
$$
\sigma_x^2 = V(X) = E[(x - \mu_x)^2] = E(X^2) - [E(X)]^2
$$
The square root of the variance is the **standard deviation**.
$$
\sigma_x = \sqrt{V(X)}
$$
To find the variance of a linear function $aX + b$, use the following formula:
$$
\begin{align*}
V(aX + b) &= a^2 \cdot V(x) \\
\sigma_{aX + b} &= |a| \sigma_x
\end{align*}
$$
We need the absolute value in the above: even if $a$ is negative, the distances of possible outcomes from the mean are always positive.

## 3.4 ~ binomial distribution.

The **binomial distribution** is used to describe a random variable that measures $n$ trials, $X$​ of which are successful. $p$ is the probability of a trial being successful. The probability function is as follows:
$$
b(X = x; n, p) = \begin{cases}
	\binom{n}{x} p^x (1 - p)^{n - x} & x \in \mathbb{N} \\
	0 & \text{else}
\end{cases}
$$
The cdf of the binomial distribution is just:
$$
\begin{align*}
P(X \leq x) &= \sum_{s = 0}^{x} b(s; n, p) &x \in \mathbb{N}
\end{align*}
$$
The mean of the binomial distribution $E(X) = np$, and the variance $V(x) = np(1 - p)$.	

## 3.6 ~ poisson distribution.

A random variable $X$ has a **poisson distribution** if its pmf is:
$$
p(x; \mu) = \frac{e^{-\mu} \mu^x}{x!}
$$
Note that while $\mu$ is the parameter of the distribution, it is also its expected value. In the poisson distribution, $E(x) = V(x) = \mu$.

Suppose we have a binomial distribution with parameters $n$ and $p$. If choose $n \rightarrow \infty$ and $p \rightarrow 0$ in such a way that $np \rightarrow \mu$, then we can say that:
$$
b(x; n, p) \rightarrow p(x; \mu)
$$
Another important use of this distribution is the **poisson process**, the occurrence of events over time. The process has a parameter $\alpha > 0$ such that the expected number of events over time $t$ is $\alpha t$. 

The below pdf demonstrates the probability that $k$ events will occur according to the poisson process:
$$
P_k(t) = \frac{e^{-\alpha t} (\alpha t)^k}{k!}
$$

## 4.1 ~ continuous pdfs.

**Continuous random variables** are those that can take on an infinite number of values. For instance, the height of all American men.

If $X$ is a continuous random variable with pdf $f(x)$, the probability that $X$ lies between $a$ and $b$ can be determined by:
$$
P(a \leq X \leq b) = \int_a^b f(x) dx
$$
For $f(x)$ to be a legitimate pdf, it must meet two conditions.

1. $f(x) \leq 0, \forall x$. No negative probabilities.
2. $\int_{-\infty}^{\infty} f(x) dx = 1$. Probabilities of all outcomes sum up to 1.

If a continuous random variable has a **uniform distribution** on the interval $[A, B]$, it has the following pdf:
$$
f(x; A, B) = \begin{cases}
	\frac{1}{B - A} & A \leq x \leq B \\
	0 & \text{otherwise}
\end{cases}
$$
 Note that the probability of a continuous random variable taking on an exact value is zero:
$$
\forall c, P(X = c) = 0
$$

## 4.2 ~ continuous cdfs and evs.

The **cumulative distribution function (cdf)** of a continuous random variable $X$ is the probability that $X \leq x$, where $x$ is a parameter of the function:
$$
\text{cdf of $X$} = F(x) = P(X \leq x) = \int_{-\infty}^{x} f(y) dy
$$
The reason we use $y$ inside the integral is because $x$ is already a parameter of the function; the choice of $y$ is arbitrary but probably convention or something.

We can use the cdf to compute various probabilities:
$$
\begin{align*}
P(X > x) &= 1 - F(x) \\
P(a \leq X \leq b) &= F(b) - F(a) 
\end{align*}
$$
Since $F(x)$, the cdf by definition computes the integral of $f(x)$, the pdf, we can determine $f(x)$ by taking the derivative of $F(x)$.
$$
F'(x) = f(x) \text{ at every $x$ where $F'(x)$ exists}
$$
The **expected value** of a continuous rv $X$ is found with the following:
$$
E(X) = \int_{-\infty}^{\infty} x \cdot f(x) dx
$$
If we want to find the expected value of some function $h(X)$, we compute:
$$
E(h(X)) = \int_{-\infty}^{\infty} h(x) \cdot f(x) dx
$$
To find the the variance of some continuous rv $X$. (Standard deviation $\sigma = \sqrt{V(x)}$.)
$$
V(x) = \int_{\infty}^{\infty} (x - \mu)^2 \cdot f(x) dx = E((x - \mu)^2)
$$
Shorthand to calculate the variance:
$$
V(x) = E(X^2) - (E(X))^2
$$

## 4.3 ~ normal distribution.



