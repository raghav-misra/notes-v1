# stat400 / final

## 0.0 ~ final information.

- Not cumulative, six problems.

## 0.1 ~ relevant previous content.

Expected value of discrete rv $X$. Continuous is same with integration from $-\infty$ to $\infty$.
$$
E(x) = \mu_X = \sum_{x \in D} x \cdot p(x)
$$
$E(h(X))$ for some function $h$. Continuous, once again, with integration from $-\infty$ to $\infty$.
$$
E(h(X)) = \sum_{x \in D} h(x) \cdot p(x)
$$
In the case of a linear function $h(X) = aX + b$, we can use a shortcut formula. This is also easily derivable by manipulating the sum in the $E(x)$ definition.
$$
E(aX + b) = aE(x) + b
$$
 The **variance** is the square of the **standard deviation**.
$$
\sigma_x^2 = V(X) = E[(x - \mu_x)^2] = E(X^2) - [E(X)]^2
$$
To find the variance of a linear function $aX + b$, use the following formula:
$$
\begin{align*}
V(aX + b) &= a^2 \cdot V(x) \\
\sigma_{aX + b} &= |a| \sigma_x
\end{align*}
$$
We need the absolute value in the above: even if $a$​ is negative, the distances of possible outcomes from the mean are always positive. 

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

## 4.3 ~ the normal distribution.

A continuous random variable has a **normal distribution** with parameters $\mu$ and $\sigma$.
$$
\begin{align*}
	f(x; \mu, \sigma) 
	&= \frac{1}{\sqrt{2 \pi} \sigma} e^{-(x-\mu)^2/(2 \sigma^2)}
	&-\infty < x < \infty 
\end{align*}
$$
A normal distribution has the following properties:

- $\mu$ is the **mean** of the distribution.
- $\sigma$​ is its **standard deviation**.
- About $68\%$ of the values are within $1$ standard deviations of the mean.
- About $95\%$ of the values are within $2$​ standard deviations of the mean.
- About $99.7\%$ of the values are within $3$ standard deviations of the mean.

The **standard normal distribution**, denoted $Z$, has $\mu = 0$ and $\sigma = 1$. The function follows:
$$
P(a \leq X \leq B) = \int_{a}^b = \frac{1}{\sqrt{2 \pi}}e^{-x^2 / 2}
$$

We denote the CDF of the standard normal distribution $\Phi(z)$. If we have $X \sim N(\mu, \sigma)$, we can compute probabilities related to $X$ by "standardizing," or converting to the standard normal distribution:
$$
P(X \geq x) = P(Z \geq \frac{x - \mu}{\sigma}) = \Phi(\frac{x - \mu}{\sigma})
$$

On the graphing calculator, we can use `distr > normalcdf` to find our relevant values for $\Phi$​. For non-standardized distributions, we can use the above standardization process followed by `normalcdf` to find desired probabilities.

We can also compute **percentiles** of normal distributions. Say we have $X \sim N(\mu, \sigma)$. Given a percent $p\%$, find $x$ such that $P(X \leq x) = p\%$. (If we have $99\%$ for instance, we treat it as $0.99$).

To do this, we can use the `distr > invNorm` calculator function.
$$
\begin{align*}
	P(X \leq x) &= p &\text{given} \\
	\Phi(\frac{x - \mu}{\sigma}) &= p &\text{standardize} \\
    \frac{x - \mu}{\sigma} &= \texttt{invNorm}(p) &\text{use inverse fn}
\end{align*}
$$
Know that a **binomial distribution** If $X \sim B(n, p)$ can be approximated by a normal distribution with $\mu = np$ and $\sigma = \sqrt{np(1 - p)}$. This is a result of the **central limit theorem**. The associated normal distribution is an adequate approximation when $np \geq 10$ and $n(1 - p) \leq 10$. That is, the expected number of successes and failures are at least $10$.

## 4.4 ~ the exponential distribution.

$X$ has an **exponential distribution** with parameter $\lambda  > 0$ when its PDF:
$$
f(x) = \begin{cases}
	\lambda e^{-\lambda x} & x \geq 0 \\
	0 &\text{else}
\end{cases}
$$
It has an **expected value** of $\mu = 1/\lambda$ and a **variance** of $\sigma^2 = 1/\lambda^2$.

But what we care more about is the CDF of an exponential distribution:
$$
P(X \leq x) = \begin{cases}
	0 & x < 0 \\
	1 - e^{- \lambda x} & x \geq 0
\end{cases}
$$
Consider a **Poisson process**. We know the average number of events that occur over a time interval, but we don't know *when* they actually occur. In fact, the time interval between each event is a random variable that can be modeled by the exponential distribution!

Recall the Poisson distribution with parameter $\alpha t$, where $\alpha$ is the average number of events in a unit of time (could be seconds, minutes, ...). The probability that the time between two events is at most $t$ is then the CDF of the exponential distribution with parameter $\lambda = \alpha$.
$$
P(X \leq t) = \begin{cases}
	0 & t < 0 \\
	1 - e^{-\alpha t} & t \geq 0
\end{cases}
$$

## 5.1 ~ jointly distributed random variables.

Let $X$ and $Y$ be two **discrete random variables** defined on sample space $\mathcal{S}$. We let the **joint pmf** of $X$ and $Y$ be the function:
$$
p(x, y) = P(X = x \text{ and } Y = y) 
$$
Logically, $p(x, y) \geq 0$ (no negative probabilities) and $\sum_{x \in X} \sum_{y \in Y} p(x, y) = 1$ (total probability must be $1$). 

Loosely, the **marginal pmf** of $X$, denoted $p_X(x)$, is the probability that $X = x$, and $Y$ can take on any value. $p_Y(y)$ is the same concept, but obviously flipped.
$$
\begin{align*}
	p_X(x) &= \sum_{y \in Y} p(x, y) &\text{marginal pmf of $X$} \\
	p_Y(y) &= \sum_{x \in X} p(x, y) &\text{marginal pmf of $Y$}
\end{align*}
$$
Now consider the **joint pdf** $f(x, y)$ of two **continuous random variables** $X$ and $Y$. Consider their **marginal pdfs**:
$$
\begin{align*}
    f_X(x) &= \int_{- \infty}^{\infty} f(x, y) dy &\text{marginal pdf of $X$} \\
    f_Y(y) &= \int_{- \infty}^{\infty} f(x, y) dx &\text{marginal pdf of $Y$}
\end{align*}
$$
$X$ and $Y$ are said to be **independent** of each other if, for each pair $(x, y) \in X \times Y$:
$$
\begin{align*}
	p(x, y) &= p_X(x) \cdot p_Y(y) &\text{for discrete $X$ and $Y$} \\
	f(x, y) &= f_X(x) \cdot f_Y(y) &\text{for continuous $X$ and $Y$}
\end{align*}
$$
If the above is not true for all $(x, y)$, then $X$ and $Y$​ are **dependent variables**. More intuitively, if the outcome of one variable is not influenced by the outcome of another, they are independent.
$$
meow.
$$
The joint pf of $n$ random variables $X_1, X_2, \dots, X_n$:
$$
p(x_1, x_2, \dots, x_n) = P(X_1 = x_1, X_2 = x_2, \dots, X_n = x_n)
$$
The marginal pfs of each of the $n$​​ random variables extend in a similar fashion: hold one variable constant and sum over all probabilities of the other variables.

We use **conditional distributions** to determine how the outcome of one variable impacts that of another variable. Let $X$ and $Y$ be two random variables with joint pf $f(x, y)$ and marginal pfs $f_X(x)$ and $f_Y(y)$. We then have:
$$
f_{Y|X}(y|x) = \frac{f(x, y)}{f_X(x)}
$$
Out of the total probability that $X = x$, what is the probability that $Y = y$? 

## 5.2 ~ expected values, covariance, correlation.

The **expected value** of some function of jointly distributed random variables $X$ and $Y$:
$$
\begin{align*}
	E[h(X, Y)] &= \sum_{x \in X} \sum_{y \in Y} h(x, y) \cdot p(x, y) &\text{discrete} \\
	E[h(X, Y)] &= \int_{- \infty}^{\infty} h(x, y) \cdot p(x, y) dx dy &\text{continuous}
\end{align*}
$$
The **covariance** of two dependent variables is how strongly related they are to each other. To compute covariance, we use the previously mentioned expected value functions.
$$
\text{Cov}(X, Y) = E[(X - \mu_X)(Y - \mu_Y)] = E(XY) - (\mu_X) (\mu_Y)
$$
The covariance of $X$ with itself is just the variance of $X$.
$$
\text{Cov}(X, X) = E[(X - \mu_X)^2] = V(X)
$$
The **correlation coefficient** of $X$ and $Y$ is denoted $\text{Corr}(X, Y)$ or $\rho_{X, Y}$.
$$
\text{Corr}(X, Y) = \rho_{X, Y} = \frac{\text{Cov}(X, Y)}{\sigma_X \cdot \sigma_Y}
$$
If $X$ and $Y$ are independent, the $\rho = 0$, but $\rho = 0$ is not enough to assume independence. $\rho \in \{-1, 1\}$ if and only if $Y = aX + b$ and $a \neq 0$.

## 5.3 ~ statistics and their distributions.

A **statistic** is any quantity whose value can be calculated from sample data. It is a random variable, denoted by an uppercase letter, say $\overline{X}$. A lowercase $\overline{x}$ represents a observed value of the statistic.

A **sample mean** is the random variable $\overline{X}$, where any observation/measurement of it is $\overline{x}$. Similarly, $\overline{S}$ is the **sample standard deviation** and any measurement of it is $\overline{s}$​.

The probability distribution of a statistic is called the **sampling distribution**. The shape of the sampling distribution depends on the population distribution and the sample size $n$. 

The random variables $X_1, X_2, \dots, X_n$ form a **simple random sample** of size $n$ if for all distinct $i$ and $j$ between $1$ and $n$:

1. $X_i$ and $X_j$ are independent.
2. $X_i$ and $X_j$​ have the same probability distribution.

## 5.4 ~ distribution of the sample mean.

The sample mean $\overline{X}$ can allow us to draw conclusions about the population mean $\mu$.
$$
\begin{align*}
	E(\overline{X}) &= \mu &\text{expected sample mean} \\
	\sigma_{\overline{X}} &= \frac{\sigma}{\sqrt{n}} &\text{expected sample std. dev.} \\
\end{align*}
$$
Let $T_o$ be the **sample total** (for a sample of size $n$, $T_o = X_1 + \dots + X_n$​).
$$
\begin{align*}
	E(T_o) &= n \mu &\text{$\mu$ is population mean, $E(T_o)$ is expected total} \\
	V(T_o) &= n \sigma^2 &\text{$\sigma^2$ is population variance, $V(T_o)$ is variance of total}
\end{align*}
$$
Consider the random sample of size $n$ from a *normal distribution*. For any $n$, $\overline{X}$ is normally distributed with mean $\mu$ and standard deviation $\frac{\sigma}{\sqrt{n}}$.

 Consider a random sample of size $n$ with mean $\mu$ and standard deviation $\sigma$. The **central limit theorem** states that, for sufficiently large $n$, $\overline{X} \sim N(\mu, \sigma)$. That is, the distribution of the sample mean is approximately normal, regardless of the population distribution.

Realistically, this means we can just pretend the distribution is normal, standardize it according to its $\mu$ and $\sigma$ (refer to section 4.3), and calculate probabilities with $\Phi$​/`normalcdf`.

**Sufficiently large $n$?** Generally, as long as $n$ is greater than $30$, the CLT will apply.

## 1.3 ~ measures of location.

The **sample mean** $\overline{x}$ of observations $x_1, x_2, \dots, x_n$ is:
$$
\frac{\sum_{i = 1}^{n} x_i}{n}
$$
**Population mean** is denoted by $\mu$​. $\overline{x}$ might be used as a **point estimate** (single number, best guess) of $\mu$. Sample mean can be a weak measure due to **outliers** (unusually large/small observation).

The **sample median $\tilde{x}$** is obtained by ordering the observations $x_1$ through $x_n$ from least to greatest, and choosing the center element. In the event that there are two center elements ($n$​ is event), we take the average of the two. **Population median** is denoted by $\tilde{\mu}$.

Median is a more outlier resistant metric and may be used in distributions with large outliers.

The **lower quartile $q_1$** is the median of all observations before $\tilde{x}$ when ordered. The **upper quartile $q_3$** is the median of all observations after $\tilde{x}$ when ordered.

A **trimmed mean** is a compromise between the mean and median, in the event of reducing outliers from the mean. A $10\%$ trimmed mean computes the mean after removing $10\%$ of the smallest and largest observations. If we had $10$ values, this would be the average of the middle $8$ numbers.

## 1.4 ~ measures of variability.

The simplest measure of spread is the **range**, which is the distance between the largest and smallest observations (quite literally subtract them). However, it might not be effective when there are significant outliers present (think about why).

The **sample standard deviation**, loosely, measures an observation's expected distance from the mean.
$$
\begin{align*}
	s^2 &= \frac{\sum (x_i - \overline{x})^2}{n - 1} &\text{luh variance} \\
	s &= \sqrt{s^2} &\text{standard deviation}
\end{align*}
$$
Probably Google a **box plot** and **stem and leaf plot** if you don't know what they are.

## 0.2 ~ practice exam.

Let $X$ be a random variable and let $a \in \mathbb{R}$. 

**(2 points)** What is $\text{Cov}(X, a)$, the covariance of $X$ and $a$?

> Recall the formula for covariance: $\text{Cov}(X, a) = E(XY) - (\mu_X) (\mu_Y)$.
>
> Plug in $X$ and $a$:
> $$
> \begin{align*}
> 	\text{Cov}(X, a) 
> 		&= E(aX) - (\mu_a)(\mu_X) \\
>         &= a(\mu_X) - a(\mu_X) = 0
> \end{align*}
> $$
> **Answer:** The covariance is $0$.

Suppose there are two factories, factory A and factory B, producing a certain type of product. Let us denote the number of defective products produced by factory A as $X$ and by factory B as $Y$. The joint probability (mass) function of $X$ and $Y$ is given in the accompanying table:

|         | $Y = 0$ | $Y = 1$ | $Y = 2$ | $Y = 3$ |
| ------- | ------- | ------- | ------- | ------- |
| $X = 0$ | $0.1$   | $0.2$   | $0.1$   | $0.05$  |
| $X = 1$ | $0.1$   | $0.15$  | $0.1$   | $0.05$  |
| $X = 2$ | $0.05$  | $0.05$  | $0.05$  | $0$     |

**(6 points)** If the total number of defective products recorded in the quality report is the sum of defective products from both factories (i.e., $X + Y$​), calculate the expected total defective products recorded.

> Let $h(X, Y) = X + Y$. We want to determine $E[h(X, Y)]$:
> $$
> \begin{align*}
> 	E[h(X, Y)] 
> 		&= \sum_{x \in X} \sum_{y \in Y} h(x, y) \cdot p(x, y) \\
> 		&= 0(0.1) + 1(0.2) + 2(0.1) + 3(0.05) \\
> 		&+ 1(0.1) + 2(0.15) + 3(0.1) + 4(0.05) \\
> 		&+ 2(0.05) + 3(0.05) + 4(0.05) + 5(0) \\
>     E(X + Y) &= 1.9
> \end{align*}
> $$
> The expected total defective products is $1.9$.

**(5 points)** If only the maximum number of defective products between the two factories is recorded, calculate the expected number of defective products recorded.

> Let $h(X, Y) = \max(X, Y)$. We want  	to determine $E[h(X, Y)]$:
> $$
> \begin{align*}
> 	E[h(X, Y)] 
> 		&= \sum_{x \in X} \sum_{y \in Y} h(x, y) \cdot p(x, y) \\
> 		&= 0(0.1) + 1(0.2) + 2(0.1) + 3(0.05) \\
> 		&+ 1(0.1) + 1(0.15) + 2(0.1) + 3(0.05) \\
> 		&+ 2(0.05) + 2(0.05) + 2(0.05) + 3(0) = 1.45
> \end{align*}
> $$
> The expected maximum recorded is $1.45$.

Let $X$ have the exponential distribution with parameter $\lambda > 0$. 

**(2 points)** What is the variance of $X$?

> Recall (from the formula sheet:rofl:) the variance of $X$ is $\frac{1}{\lambda^2}$.

A consumer is trying to decide between two long-distance calling plans. The first one charges a flat rate of $10$ cents per minute, whereas the second charges a flat rate of $99$ cents for calls up to $20$ minutes in duration and then 10 cents for each additional minute exceeding $20$ (assume that calls lasting a non-integer number of minutes are charged proportionately to a whole minute’s charge). Suppose the consumer's distribution of call duration is exponential with parameter $\lambda$​.

**(2 points)** Explain intuitively how the choice of calling plan should depend on what the expected call duration is.

> The expected call duration is $1/\lambda$. If this value is under $10$ minutes, it makes sense to go with the $10$​ cents per minute plan. For calls greater than $10$ minutes, the second plan ($99$ cents until $20$ minutes and then $10$/min after) makes more sense, as it will always be lesser than the $10$/min plan.

**(9 points)** Which plan is better if expected call duration is $10$ minutes? $15$ minutes?

> Let $h_1(x) = 10x$, where $x$ is minutes called, this is the first plan. Also, let the second plan be $h_2(x) = 99 + [10\cdot\min(0, x - 20)]$​. Both functions are on $x \in [0, \infty)$ and zero outside of these bounds.
>
> For the expected call duration $10$, we have $\lambda = \frac{1}{10}$​. We want to compare the expected values of the above two functions:
> $$
> \begin{align*}
> 	E[h_1(x)] 
> 		&= E(10x) = 10E(x) = 10 \cdot 10 = 100 \\
> 	E[h_2(x)] 
> 		&= \int_{-\infty}^{\infty} h_2(x) \cdot \frac{1}{10}e^{-\frac{1}{10}x} dx \\
> 		&= \int_{0}^{20} 99 \cdot \frac{1}{10}e^{-\frac{1}{10}x} dx 
> 		+ \int_{20}^{\infty} [99 + 10(x - 20)] \cdot\frac{1}{10}e^{-\frac{1}{10}x} dx \\
> 		&= 112.5335
> \end{align*}
> $$
> **Answer:** Clearly, $h_1$ has a lower expected value, so we recommend plan $1$ in this case.
>
> Now we consider expected call duration $15$, we have $\lambda = \frac{1}{15}$. We want to compare the expected values once again:
> $$
> \begin{align*}
> 	E[h_1(x)] 
> 		&= E(10x) = 10E(x) = 10 \cdot 15 = 150 \\
> 	E[h_2(x)] 
> 		&= \int_{-\infty}^{\infty} h_2(x) \cdot \frac{1}{15} e^{-\frac{1}{15} x} dx \\
> 		&= \int_{0}^{20} 99 \cdot \frac{1}{15} e^{-\frac{1}{15} x} dx 
> 		+ \int_{20}^{\infty} [99 + 10(x-20)] \cdot \frac{1}{15} e^{-\frac{1}{15}x} dx \\
> 		&= 138.5396
> \end{align*}
> $$
> **Answer:** In this case, $h_2$ has a lower expected value, so we recommend plan $2$.

Let $(X_i)_{i = 1}^{n}$ be iid random variables with mean $\mu \in \mathbb{R}$ and standard deviation $\sigma > 0$. 

**(2 points)** If $n = 10000$, what is the probability that the sample mean $\overline{X}$ is within a hundredth of $\sigma$ of its mean?

> By the central limit theorem, we can assume that the sampling distribution is normal. Consider the standard deviation of the sampling distribution $\frac{\sigma}{100}$​.
>
> We want to find the probability that $\overline{X}$ is within $\frac{\sigma}{100}$ of $\mu$. Since that is just one standard deviation of the sampling distribution, which we can assume is normal, there's approximately a $68\%$ chance of this.

A binary communication channel transmits a sequence of bits ($0$s and $1$s). Suppose that for any particular bit transmitted, there is a $10\%$ chance of a transmission error (a $0$ becoming a $1$ or a $1$ becoming a $0$). Assume that bit errors occur independently of one another.

**(2 points)** Consider transmitting $1000$ bits. What is the probability that at most $125$ transmission errors occur?

> Consider the distribution for random variable $X$, the number of errors. Clearly it is binomial, with $n = 1000$ and $p = 0.1$. We want to find $P(X \leq 125)$, using `binomcdf` calculator function:
> $$
> P(X \leq 125) = \texttt{binomcdf}(X \leq 125; 1000, 0.1) \approx 0.9955
> $$

**(3 points)** Use the normal distribution to approximate your answer to (a).

> We can approximate the above binomial distribution using a normal distribution with mean $\mu = np = 1000(0.1) = 100$ and $\sigma^2 = np(1 - p) = 1000(0.1)(0.9) = 90$.
>
> We can standardize $125$ using $\mu$ and $\sigma$ and use `normalcdf` aka $\Phi$:
> $$
> \Phi(\frac{125 - 100}{\sqrt{90}}) = 0.9958
> $$

**(6 points)** Suppose the same $1000$-bit message is sent two different times independently of one another. Use the normal distribution to approximate the probability that the total number of errors in the two transmissions is within $50$ of its mean.

> Let $X_1$ and $X_2$ be the binomial distributions for number of errors in the two messages. We assume these to be approximately normal, with $\mu = np = 100$ and $\sigma = np(1 - p) = 90$.
>
> Consider the expected value of the sum of both messages' errors:
> $$
> E(X_1 + X_2) = E(X_1) + E(X_2) = 100 + 100 = 200
> $$
> Consider the variance of the sum of both messages' errors:
> $$
> V(X_1) + V(X_2) = 90 + 90 = 180
> $$
> 
>
> We want to find the probability that the total number of errors across both messages is within $50$ of that expected value:
> $$
> \begin{align*}
> 	E(200 - 50 \leq X_1 + X_2 \leq 200 + 50) 
> 		&= E(X_1 + X_2 \leq 250) - E(X_1 + X_2 \leq 150) \\
> 		&= \Phi(\frac{250 - 200}{\sqrt{180}}) - \Phi(\frac{150 - 200}{\sqrt{180}}) \\
> 		&= 0.9998
> \end{align*}
> $$
