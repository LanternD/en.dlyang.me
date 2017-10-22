---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 5
description: Sample mean and sample variance, biased and unbiased estimation; covariance, Hypergeometric distribution and its example; correlation coefficients; discrete distribution, Poisson distribution, Poisson approximation for the Binomial distribution.
permalink: /stt-861-lecture-note-5/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-10-04 20:35:32
---

# Portal to all the other notes

You would encounter a 404 error if I haven't taken the lecture. :-)

I will add this after I finished everything.

# Lecture 05 - Oct 05 2017

## Sample mean and sample variance 

**Recall**： The proposition $E((X-c)^2)$.

Now consider some data $x_i$, $i=1,2,3,...,n$. We imagine that this data comes from an experiment which is repeated $n$ times independently. This means that $x_i$ represents a r.v. $x_i$, where the $x_i$s are i.i.d.

We are accustomed to using the notation

$$\bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i$$

This is called "sample mean".

$$\hat{\sigma}^2=\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2$$

This is called "sample variance".

Now investigate the statistical properties of the two "estimators". Replace $x_i$ by $X_i$ and try this. 

**Notation**: $\bar{x}$ is for data points, while $\bar{X}$ is for the model notation. 

Find the $E(\bar{X})$. If $E(\bar{X})=\mu$, then we say $\bar{X}$ is unbiased. 

Find $E(\hat{\sigma}^2)$. Is it $Var(X)$? It might be biased. 

$$E(\bar{X})=E(\frac{1}{n}\sum_{i=1}^{n}X_i)=\frac{1}{n}\sum_{i=1}^{n}E(X_i)=\mu$$

$$E(\hat{\sigma}^2)=E(\frac{1}{n}\sum_{i=1}^{n}(X_i-\bar{X})^2)$$

The left-hand side of the formula in the previous proposition applied to a r.v. $X$, which is equal to $X_i$ with prob $=\frac{1}{n}$.

The stuff inside the parenthesis is actually the expectation of a r.v. equal to $X_i-\bar{X}$. 

$$\begin{align*}
	\frac{1}{n}\sum_{i=1}^{n}(X_i-\bar{X})^2 &= \frac{1}{n}\sum_{i=1}^{n}(X_i-c)^2-(\bar{X}-c)^2\\
	&=\frac{1}{n}\sum_{i=1}^{n}(X_i-\mu)^2-(\bar{X}-\mu)^2\\
	\Rightarrow E[\hat{\sigma}^2]&= \frac{1}{n}\sum E(X_i-\mu)-E((\bar{X}-\mu)^2) \\
	&=\frac{1}{n}nVar(X)-E((\frac{1}{n}\sum x_i-\mu)^2) \\
	&=Var(X)-E(\frac{1}{n}\sum(x_i-\mu)^2) \\
	&= -E((\sum x_i-\mu)^2)\\
	&= Var(X)- \frac{1}{n}Var(X) \\
	&= (1-\frac{1}{n})Var(X)
\end{align*}$$

As a result, this is not exactly $=Var(X)$. Thus, $\hat{\sigma}^2$ is biased. 

Let's define an unbiased estimator for $Var(X)$, We just need to take 

$$S^2=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\bar{X})^2$$

It is unbiased estimation of $Var(X)$.

------

## Covariance (Chapter 1.7)

**Definition**: Let $X$ & $Y$ be two r.v.s living on the same prob space.

$$cov(X,Y)=E((X-E(X))(Y-E(Y))$$

**Property**: If $X$ & $Y$ are independent, then $cov(X,Y)=0$. Be aware, The statement is usually false, i.e. $cov(X,Y)\neq0$.

Note: if $X=Y$, $cov(X,Y)=Var(X)$.

**Property**: Let $X_i$, $i=1,2,...,n$ be r.v.'s.

$$\begin{align*}
	Var(\sum_{i=1}^{n}X_i) &= \sum_{i=1}^{n}\sum_{j=1}^{n}cov(X_i,X_j) \\
	&=\sum_{i=1}^{n}Var(X_i)+\sum_{i=1}^{n}\sum_{j=1\neq i}^{n}cov(X_i,X_j) \\
\end{align*}$$

## Hypergeometric distribution

Application of the previous formula: The variance of the Hypergeometric distribution (no details here, see the book).

**Definition**: The hypergeometric distribution with parameter $(n, N)$ is the distribution of the r.v. $X$ of the number of elements from a distinguish subset of size $n$, when one picks a sample of size $k$ without replacement from the $N$ elements.

### Example 1

The number $X$ of women in a sample of size $k=5$ taken without replacement from a group with 8 women & 12 men has this hypergeometric distribution with $N=8+12=20$ and $n=8$.

It turns out that

$$Var(X)=kn\frac{N-n}{N-1}$$

**Comments**: use notation $p=n/N$, then 

$$Var(X)=kNp\frac{1-p}{1-\frac{1}{N}}$$

Notice: If $N$ is large, the $\frac{N}{N-1}$ is almost $=1$. So this variance is almost the variance of a binomial with success parameter $p$. This is because if $k$ is much smaller than $N$, sampling without replacement is almost like sampling with replacement. 

This "binomial approximation to the hypergeometric law" works well if $k\ll N$, except if $p=n/N$ is too close to 1 or 1. 

## Correlation coefficients

Let $X$ and $Y$ be two r.v.'s. We standardize them let 

$$Z_X=(X-\mu_X)/\sigma_X$$

$$Z_Y=(Y-\mu_Y)/\sigma_Y$$

where $\mu_X=E(X)$, $\mu_Y=E(Y)$, $\sigma_X=\sqrt{Var(X)}$, $\sigma_Y=\sqrt{Var(Y)}$. 

Notice that $E(Z_X)=E(Z_Y)=0$, $Var(Z_X)=Var(Z_Y)=1$.

**Definition**: The correlation coefficient between $X$ and $Y$ is

$$Corr(X,Y)=Cov(Z_X,Z_Y)$$

Note: The correlation between $X$ and $Y$ is a value $\in[-1,1]$.

### Example 2

Let $X=Y$, then $Corr(X,Y)=1$.

What if $Y=aX+b$, where $a$ and $b$ are constants?

$Corr(X,Y)=1$ if $a>0$, and $=-1$ if $a<0$. 

If $X$ and $Y$ are independent, $Corr(X,Y) = 0$. 

In general, $Corr(X,Y)$ measures the linear relationship between $X$ and $Y$. 

**Main idea**: If we have a scatter plot of $x$ and $y$ data, which lines up very well along a straight line,  then $Corr(X,Y)\triangleq\rho$ will be close to 1 if the line slope up and close to -1 if slop down.

**Property**: Because $Corr(X,Y)$ is defined using the standardized $Z_X$ and $Z_Y$, then 

$$Corr(aX+b, cY+d)=Corr(X,Y)$$

------

## Discrete Distributions (Chapter 2)

Some distributions: $Binom(n,p)$, $Geom(p)$

Important expression: 

- $E(Ber(p))=p$, $Var(Ber(p))=p(1-p)$.  
- $E(Binom(n,p))=np$, $Var(Binom(n,p))=np(1-p)$.
- $E(Geom(p))=\frac{1}{p}$, $Var(Geom(p))=\frac{1-p}{p^2}$.  
- $E(NB(r,p))=\frac{r}{p}$, $Var(NB(r,p))=r\frac{1-p}{p^2}$.

**Recall**: the intuition behind the formula $E(Geom(p))=1/p$: For example, if $p=1/20$ for a success and we should expect wo wait 20 units of time until the first success.

### Exercise at home

Prove the $E$ and $Var$ for $Geom(p)$.

## Poisson Distribution 

**Definition**: $X$ is Poisson distribution distributed with parameter $\lambda$ if $X$ takes the values $k=0,1,2,...$ and

$$P(X=k)=e^{-\lambda}\frac{\lambda^k}{k!}$$

Compute the expectation,

$$\begin{align*}
	E(X)&=\sum_{k=0}^{\infty}ke^{-\lambda}\frac{\lambda^k}{k!} \\
	&=e^{-\lambda}\sum_{k=1}^{\infty}\lambda^k\frac{1}{(k-1)!}\\
	&= \lambda e^{-\lambda}\sum_{k=0}^{\infty}\lambda^k\frac{1}{k!}\\
	&=\lambda e^{-\lambda}\times e^\lambda = \lambda
\end{align*}$$

(Recall: $e^x=\sum_{k=0}^{\infty}x^k\frac{1}{k!}$, Taylor series)

It turns out $Var(X)=\lambda$ [Prove it at home, easier to calculate $E(X(X-1))$].

**Quick question**: What is $E(X^2)$? $=\lambda+\lambda^2$.

### Poisson approximation for the Binomial distribution

Idea: if events are **rare**, they usually follow a Poisson law.

**Fact**: Let $X$ be $Bin(n,p)$ and assume $p$ is proportional to $1/n$: $p=\lambda/n$.

Then PMF of $Binom(n, p)$ is almost the same as for $Poi(\lambda)$. Specifically we mean this:

$$\lim\limits_{n\rightarrow\infty}C_n^k(\frac{\lambda}{n})^k(1-\frac{\lambda}{n})^{n-k}=e^{-\lambda}\frac{\lambda^k}{k!}$$

If $p$ is small (of order of $1/n$), then $\\#success\sim Bin(n,p)\approx Por(\lambda)$, $\lambda=E(\\#success)=np$.

Because of this, Poisson distribution is a good model for number of arrival (of some phenomenon) in a fixed interval of time. 

This interpreted as successive units of time (e.g. minutes) in an interval of time, also explains the next property:

**Fact**: let $n$ and $M$ be two independent Poisson r.v.'s with parameters $\lambda$ and $\mu$, then $X=N+M$ is Poisson too, with parameter $(\lambda+\mu)$. 

Because $E(X)=E(N)+E(M)=\lambda+\mu$.

We can use Binomial distribution visualization to prove the fact that $X$ is Poisson. 

### Exercise

Try to prove $X$ is Poisson using only PMF.