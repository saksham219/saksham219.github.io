---
layout: post
title: "Where does the t-distribution come from"
date: 2023-10-31
featured-image:
---

In an introductory statistics course, the t-test, which relies on the t-distribution is used as the main method to do hypothesis testing for population models and two-sample studies. In this article, I try to explain how this distribution arises for normally distributed samples based on population models. We consider single-sample studies for this article. However, the same can be extended to two-sample studies.

We start by considering i.i.d observations from a population with distribution $P$ with mean $\mu$ and variance $\sigma^2$ (not necessarily normal):

$$
\begin{align}
X_1, X_2, \dots, X_n \sim P \text{ with mean } \mu \text{ and variance } \sigma^2.
\end{align}
$$

We formulate the null hypothesis($H_0$) that the population mean $\mu$ is a fixed number $\mu_0$, and the alternate hypothesis ($H_1$):

$$
\begin{align}
H_0: \mu = \mu_0\\
H_1: \mu \neq \mu_0
\end{align}
$$

Then, the mean $\bar{X}$ is also a random variable and due to the central limit theorem, it is normally distributed with $E(\bar{X}) = \mu$ and variance $\sigma^2/n$ (due to linearity of expectation and properties of variance).

Therefore, the null hypothesis tests whether $E(\bar{X}) = \mu_0$, and under the null hypothesis,

$$
\begin{align}
& \bar{X} \sim \mathcal{N}(\mu_0, \dfrac{\sigma}{\sqrt{n}})\\
\implies & \dfrac{\sqrt{n}}{\sigma} (\bar{X} - \mu_0)\sim \mathcal{N}(0,1).
\end{align}
$$

Now we can use this distribution as null distribution to perform a t-test and get a p-value. The test statistic is

$$
t(X) = \dfrac{\bar{X} - \mu_0}{\sigma/\sqrt{n}} \approx  \dfrac{\bar{X} - \mu_0}{s/\sqrt{n}}
$$

where $s$ is the sample standard deviation. The motivation for this statistic comes from computing the difference in sample and population means, and correcting for "noise" in the sample by dividing by the sample standard deviation.

**However, the population standard deviation $\sigma$ is unknown. A solution to this is approximating $\sigma$ with the sample standard deviation $s$. This approach works if the $n$ is large as $s$ converges to $\sigma$ in the large data limit. However, if $n$ is small, the approximation is not good and we need a diffferent way of getting the null distribution. This is where the t-distribution comes in.**

We start with a new distribution called the "Chi-squared"($\chi^2$) distribution which is defined using the normal distribution,

$$
Y_1, \dots, Y_n \sim \text{ i.i.d }  \mathcal{N}(0, 1) \implies \sum_{i=0}^n (Y_i - \bar{Y})^2 \sim \chi_{n-1}^2 \text { with n degrees of freedom }.
$$

This also implies that,

$$
Y_1, \dots, Y_n \sim \text{ i.i.d } \mathcal{N}(\mu, \sigma) \implies \dfrac{1}{\sigma^2} \sum_{i=0}^n (Y_i - \bar{Y})^2 \sim \chi_{n-1}^2 \text { with n degrees of freedom },
$$

We use the following proposition:

> If $X \sim \mathcal{N}(0,1)$ and $Z \sim \chi_m^2$, and X and Z are statistically independent, then
> $\dfrac{X}{\sqrt{Z/m}} \sim t_m$ where $t_m$ is the t-distribution with $m$ degrees of freedom.

The proof of the proposition is given [here](http://amath2.nchu.edu.tw/honda/605Lecture/Lecture%2005_addendum_Chisquare,t%20and%20F%20distributions.PDF).

To apply this proposition, we need the **assumption that the observations $X_1, X_2, \dots, X_n$ are normally distributed with $\mathcal{N}(\mu, \sigma)$**.

Therefore, if we define $X \sim \dfrac{\bar{X} - \mu}{\sigma/\sqrt{n}}$ and $Z = \dfrac{n-1}{\sigma^2}s^2$. Then $X \sim \mathcal{N}(0,1)$ and

$$
Z = \dfrac{n-1}{\sigma^2} \dfrac{\sum_{i=0}^n (X_i - \bar{X})^2}{n-1} \sim \chi_{n-1}^2
$$

which means that

$$
\dfrac{X}{\sqrt{Z/n-1}} = \dfrac{\sqrt{n}(\bar{X} - \mu)/\sigma}{\sqrt{\frac{n-1}{\sigma^2}s^2/n-1}} = \dfrac{\bar{X}-\mu}{s/\sqrt{n}} \sim t_{n-1}.
$$

This means if we define the test-statstic (under $H_0: \mu = \mu_0$) as

$$
  t(X) = \dfrac{\bar{X}-\mu_0}{s/\sqrt{n}},
$$

the null distribution is $t_{n-1}$ and can be used to calculate the p-value. Using this, the large $n$ assumption is not needed, and the t-test can be applied to samples with low number of observations.

To summarise, if we assume our observations to be normally distributed, we get a quantity $\dfrac{n-1}{\sigma^2}s^2$ that has a $\chi^2$ distribution by definition, and using the resulting statistic as defined above follows a t-distribution that can be used for calculating the p-value.
