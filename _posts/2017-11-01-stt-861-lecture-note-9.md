---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 9
description: Review of the important concepts of previous section; moment generation function; Gamma distribution, chi-square distribution.
permalink: /stt-861-lecture-note-9/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-11-01 20:35:32
---

# Portal to all the other notes

- [Lecture 01 - 2017.09.06](/stt-861-lecture-note-1/) 
- [Lecture 02 - 2017.09.13](/stt-861-lecture-note-2/)
- [Lecture 03 - 2017.09.20](/stt-861-lecture-note-3/)
- [Lecture 04 - 2017.09.27](/stt-861-lecture-note-4/)
- [Lecture 05 - 2017.10.04](/stt-861-lecture-note-5/)
- [Lecture 06 - 2017.10.11](/stt-861-lecture-note-6/)
- [Lecture 07 - 2017.10.18](/stt-861-lecture-note-7/)
- [Lecture 08 - 2017.10.25](/stt-861-lecture-note-8/)
- [Lecture 09 - 2017.11.01](/stt-861-lecture-note-9/) -> This post
- [Lecture 10 - 2017.11.08](/stt-861-lecture-note-10/)
- [Lecture 11 - 2017.11.15](/stt-861-lecture-note-11/)
- [Lecture 12 - 2017.11.20](/stt-861-lecture-note-12/)
- [Lecture 13 - 2017.11.29](/stt-861-lecture-note-13/)
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/)

# Lecture 09 - Nov 01 2017


## Quick Review Session (For the mid-term exam)

### Bayes' theorem

Suppose we have data: an even $B$ that happened.

Possible outcomes: $A_1,A_2,...,A_n$.

Model for each $A_i$: $P(A_i)$ given. This is the "prior" model.

Model for each relation between $A_i$ and $B$: $P(B\|A_i)$. This is the "likelihood" model. 

**Theorem**:

$$P(A_i|B)=\frac{P(B|A_i)P(A_i)}{\sum_{j=1}^{n}P(B|A_j)P(A_j)}$$

**Quick Example** (The Chevalier de Méré example in Note 3). 

$P$(one six in 4 rolls of a die) = 1 - $P$(no six in 4 rolls of a die) = $1-(\frac{5}{6})^4\approx 0.5177$

$P$(one double-six in 24 rolls of 2 dice) = $1-(\frac{35}{36})^{24}\approx 0.4914$

### Discrete and continuous variables

Discrete r.v.'s: $P(X=x_k)=P_k$. $E(X)=\sum_{k}x_kp_k$.

Continuous Case: $P(a\leq x\leq b)=\int_{a}^{b}f(x)dx$. $E(X)=\int_{-\infty}^{\infty}xf(x)dx$.

**Linearity**

- $E(\sum a_iX_i)=\sum a_iE(X_i)$.
- If $X_i$'s are independent, then $Var(a_iX_i)=\sum (a_i)^2Var(X_i)$.

### Chebyshev and Weak law of large numbers

$X$ is a r.v. $Var(X)$ exists. Then 

$$P(|X-E(X)|>\varepsilon)\leq \frac{Var(X)}{\varepsilon^2}$$

This is true no matter how small $\varepsilon>0$ is.

Apply this to $\bar{X}=\frac{1}{n}\sum (X_i-E(X_i))$, where $X_i$'s are i.i.d. and $Var(X_i)<\infty$.

Note $E(X)=\mu=E(X)$, $Var(\bar{X})=\frac{\sigma^2}{n}$.

By Chebyshev:

$$P(|\bar{X}-\mu|>\varepsilon)\leq \frac{\sigma^2}{h\varepsilon^2}$$

As $n\rightarrow \infty$, this probability $\rightarrow0$. 

### Special discrete distributions

- Bernoulli: $X_1\sim Ber(p)$, $E(X_1)=p$, $Var(X_1)=p(1-p)$.

- Binomial: $X_2=X_{11}+X_{12}+...+X_{1n}\sim Bin(n,p)$, $E(X_2)=np$, $Var(X_2)=np(1-p)$.

- Geometric: $X_3\sim Geom(p)$, $E(X_3)=\frac{1}{p}$, $Var(X_3)=\frac{1-p}{p^2}$.
	
- HyperGeometric: pass.
	
- Multinomial: pass.
	
- Negative binomial: $X_6\sim NB(r,p)$, each of them is i.i.d Geometric. $E(X_6)=\frac{r}{p}$, $Var(X_6)=\frac{r(1-p)}{p^2}$.
	
- Poisson: $X_7\sim Poi(\lambda)=e^{-\lambda}\frac{\lambda^k}{k!}$, $E(X_7)=\lambda$, $Var(X_7)=\lambda$. \# of arrivals in a fixed interval of time, where $\lambda$ is the average frequency of arrival. 
	
	- Property: let $N_1\sim Poi(\lambda_1)$, $N_2\sim Poi(\lambda_2)$, $N_1$ and $N_2$ are independent. then $N=N_1+N_2\sim Poi(\lambda_1+\lambda_2)$.
	
	- Property 2: Assume arrivals fall in one of $k$ different categories. It turns out that if the total \# of arrivals $N\sim Poi(\lambda)$ and the category of each arrival is independent of $N$ and $P$(arrivals is category $i$)$=p_i$.Then with $N_i=$ \# arrivals of category $i$ is $N_i\sim Poi(\lambda p_i)$.
	
	- More: relation between Poisson and Exponential.

Let $X\sim Exp(\lambda)$, the density is $f(x)=\lambda e^{-\lambda x}$ for $x\geq 0$.

Let $X_i$ be i.i.d $Exp(\lambda)$. Let $N(t)$ be the \# of arrivals in time interval $[0,t]$. Assume $N=$ Poisson process. Then $X_i$ is a model for the amount of time between $i-1$th and the $i$th arrivals.

[Use step functions to illustrate.]

**Theorem**: if $N(t)$ is Poisson($\lambda$) process, and $T_i$'s are its jump times (arrival times) and $X_i=T_i-T{i-1}$, then $X_i\sim Exp(\lambda)$ (i.i.d).

What about the distribution of $T_i$? $T_i\sim \Gamma(i,\theta=\frac{1}{\lambda})$.

Here recall $\lambda$ is a rate parameter, so $\theta$ is a scale parameter. 

The density of $T_n$ is 

$$f(x)=\frac{\lambda}{\Gamma(n)}(\lambda x)^{n-1}e^{-\lambda x}$$

where $x\geq 1$.

## Moment generation function

Method for doing problem 2.2.5. 

> Let $X$ have the binomial distribution with parameters $n$ and $p$. Conditionally on $X = k$, let $Y$ have the binomial distribution with parameters $k$ and $r$ . What is the marginal distribution of $Y$? 

There are lots of way to solve this problem, here we use moment generate functions (mgf).

**Definition**: Let $X$ be a r.v. Let 

$$M_X(t)=E(e^{tX})$$

where $t$ is fixed. $M_X(t)$ is the moment generation function of $X$.

It turns out, the function usually characterizes the distribution of $X$.

Example: let $X\sim Bin(n,p)$. we know $X=X_1+X_2+\cdots+X_n$ (i.i.d Bernoulli($p$)).

Now, 

$$\begin{align*}
	M_X(t) &= E(e^{tX})\\
	&=E(e^{X_1+X_2+\cdots+X_n}) \\
	&= E(e^{tX_1})E(e^{tX_2})\cdots E(e^{tX_n})\\
	&= (E(e^{tX_1}))^n
\end{align*}$$

and 

$$E(e^{tX_1})=p(e^t)+(1-p)\times 1=1+p(e^t-1)$$

Therefore, 

$$M_X(t)=(1+p(e^t-1))^n$$

Now look at Problem 2.2.5.

$$Y\sim Bin(Bin(n,p),r)$$

Therefore 

$$Y=Y_1+Y_2+\cdots+Y_X$$

where $Y_i$ are i.i.d Bernoulli$(r)$.

Hunch: $Y$ is $Binomial(a, b)$. To prove it: compute $M_Y(t)=(1+b(e^t-1))^a$

$$\begin{align*}
	M_Y(t) &=E(e^{tY})\\
	&=E(e^{t(Y_1+Y_2+\cdots+Y_X)})\\
	&= \sum_{k=0}^{n}(E(...|X=k))P(X=k)\\
	&= \sum_{k=0}^{n}E(e^{t\cdot Bin(k,r)})P(X=k)\\
	&= \sum_{k=0}^{n}(1+r(e^t-1))^kP(X=k)\\
	&= \sum_{k=0}^{n}e^{k\ln(1+r(e^t-1))} \\
	&= \sum_{k=0}^{n}e^{ku}P_k \\
\end{align*}$$

This is the defeinition of $E(e^{uX})\triangleq M_X(u)$.

$$\begin{align*}
	M_X(u) &= (1+p(e^u-1))^n \\
	&= (1+p(e^{\ln(1+r(e^t-1))})-1)^n \\
	&=(1+p(1+r(e^t-1)-1))^n \\
	&=(1+pr(e^t-1))^n 
\end{align*}$$

Therefore we recognize that $Y\sim Binom(n,pr)$. 

## Gamma Distribution

Go back to Gamma distribution.

### Example

let $Z\sim N(0,1)$ (standard normal). the $f_Z(z)=\frac{1}{\sqrt{2\pi}}\exp(\frac{z^2}{2})$. Find the density of $Y=Z^2$.

$$\begin{align*}
	F_Y(y) &= P(Y\leq y) = P(Z^2\leq y)\\
	&= P(-\sqrt{y}\leq Z \leq \sqrt{y}) \\
	&=F_Z(\sqrt{y})-F_Z(-\sqrt{y})
\end{align*}$$

Use chain rule to compute $f_Y(y)$.

$$\begin{align*}
	f_Y(y)&=\frac{dF_Y}{dy}=\frac{d}{dy}F(\sqrt{y})-\frac{d}{dy}F_Z(-\sqrt{y}) \\
	&= f_Z(\sqrt{y})\frac{1}{2\sqrt{y}} - f_Z(-\sqrt{y})\frac{-1}{2\sqrt{y}}\\
	&=\frac{1}{\sqrt{2\pi}}y^{\frac{1}{2}}e^{-\frac{y}{2}}
\end{align*}$$

We recognize this is the density of $\Gamma(\alpha=\frac{1}{2},\theta = 2)$.

### Chi-square distribution and degree of freedom

This Gamma and every Gamma for which $\alpha=\frac{n}{2}$, where $n$ is an integer, is called $\chi^2(n)$ ("Chi-squared" with $n$ degrees of freedom).

We see $\chi^2(n)\sim Z_1^2+Z_2+6+\cdots +Z_n^2$. where $Z_i\sim i.i.d~N(0,1)$.

$$\chi^2(n)\equiv \Gamma(\frac{n}{2},2)$$

Q: What about $\chi^2(2)$? 

A: $\sim Gamma(1,2)$, which is exponential distribution with parameter $\lambda=\frac{1}{2}$. 

Q: Now to create $X\sim Exp(\lambda=1)$ using only i.i.d normals $N(0,1)$.

Try this: $X=Z_1^2+Z_2^2\sim Exp(\frac{1}{2})$.

$$X=\frac{1}{2}(Z_1^2+Z_2^2)\sim Exp(1)$$

When we need to multiply a scale parameter $\theta$ by a constant $c$, we multiply the random variable by $c$. 

Equivalently, when we need to multiply a rate parameter $\lambda$ by $c$, just divide the random variable by $c$.
