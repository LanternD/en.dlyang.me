---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 6
description: Hypergeometric distribution; Poisson Law; Brownian motion; continous random variables, exponential distribution, cumulative distribution function, uniform distribution; expectation and variance of continuous random variable.
permalink: /stt-861-lecture-note-6/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-10-11 20:35:32
---

# Portal to all the other notes

You would encounter a 404 error if I haven't taken the lecture. :-)

I will add this after I finished everything.

# Lecture 06 - Oct 11 2017

## Hypergeometric distribution (continued)

(See Page 66)

A hypergeometric r.v. $X$ with parameters $n,N,R$:

Have a set of size $N$, a subset of size $R$ ('red'). Pick a sample of size $n$ without replacement. Then $X$ is the number of elements of type $R$ ('red') in the sample.

Then for $k=0,...,n$, 

$$P(X=k)=C_n^k\frac{C_{N-n}^{R-k}}{C_N^R}$$

Important: let $p=\frac{R}{N}$

$$E[X]=np$$

$$Var[X]=np(1-p)\frac{N-n}{N-1}$$

The correction factor $\frac{N-n}{N-1}$ is called the **finite sample correction factor**.

## Poisson Law

Let $N$ and $M$ be $Poi(\lambda)$ and $Poi(\mu)$ and independent. Then $N+M$ is $Pos(\lambda+\mu)$.

(Think of it as arrivals in a store on 2 different days.)

Therefore, $N(1)$ is $Poi(\lambda)$. By the same construction $N(t)$ is $Poi(\lambda t)$.

Now as $t$ funs from 0 to 1, we have a collection or r.v's $\\{N(t):t\in[0,1]\\}$. This is the Poisson process with parameter $\lambda$.

These are the properties of this $Poi(\lambda)$ process. [a stochastic process, like $N$, is a random function where the rules of randomness are specified.]

The word stochastic comes from the Greek word "stochos" ($\sigma\tau o\chi o \sigma$). It means "target".

It comes from the stroy of Aristotle and target distribution. 

Let $0<s<t$, then, 

1. $N(t)-N(s)\sim Poi(\lambda(t-s))$
2. $N(s)$ and $N(t)-N(s)$ are independent. 

Vocabulary: (2) is called **independence of increments**. And (1) is usually called **stationarity**.

**Remark**: $N(t)+N(s)$ does not $\sim P(\lambda (t+s))$.

What is $N(t)+N(s)$? $=N(t)+N(s)\sim Poi(\lambda(t-s))+2Poi(\lambda s)$

$2Poi(\lambda s)$ is not $Poi(2\lambda s)$. They might have different variance.

**Remark:** (1) and (2) define the prob distribution of the $Poi(\lambda)$ process uniquely.

### Example 2.5.2 (Page 77)

Murder rate $540/year$. Assume \# murders in the interval $[0, t]$ where $t=\textrm{proportion of a 360-day year}$ is a Poisson process $N(t)$. 

Q1: What is prob of two or more murders with in 1 day $P(N(1~day) \geq 2)$.

A1: $\lambda=\frac{540}{360}=1.5$

$$P_1=1-\sum_{k=0}^{1}e^{-\lambda}\frac{\lambda^k}{k!}=1-(e^{-1.5}+e^{-1.5}\times 1.5)=0.4422$$

Q2: What is prob of "2 or more murders for each of 3 consecutive days"?

A2: $P_2=P_1^3=0.4422^3=0.0865$

Q3: What is the prob of "No murder for 5 days"?

A3: $P_3 = P(N(5~days)=0)=P(Poi(\frac{15}{2})=0)=e^{-\frac{15}{2}}$

Q4: Rate during weekdays is 1.2/day, during weekends is 2.5/day. What is the prob of "10 or more murders in 1 week?

A4: 

$$\begin{align*}
	P_4 &=P(N(weekdays)+N(weekend)\geq 10)\\
	&=P(Poi(6)+Poi(5)\geq 10) \\
	&= P(Poi(11)\geq10) 
\end{align*}$$

$$P_4=1-\sum_{k=0}^{10-1}e^{-11}\frac{(11)^k}{k!}=0.6595$$

### HW discussion (Problem 2.4.4 (a))

$X\sim NegBin(r_1,p)$, $Y\sim NegBin(r_2,p)$. $W=X+Y$. Find the distribution of $W$.

We know that $X=X_1+X_2+\cdots+X_{r_1}$, where the $X_i$'s are i.i.d. $Geom(p)$. Similarly we have $Y_i$s are i.i.d. $Geom(p)$.

Now if we assume $X$ and $Y$ are independent. Then all the $X_i$s and $Y_i$s are independent. Then $W=X_1+\cdots+X_{r_1}+Y_1+\cdots+Y_{r_2}$ are $r_1+r_2$ i.i.d. $Geom(p)$. Therefore by definition $W$ is $NegBin(r_1+r_2, p)$.

## Preview to Chapter 3 and Brownian motion

Let $X_1,X_2,...,X_n$ be a sequence of i.i.d. r.v.s with $E[X_i]=0$ and $Var[X_i]=\sigma^2>0$.

Let $S_n=\bar{X}_{n}=\frac{X_1+X_2+...+X_n}{n}$, then $E(S_n)=0$ and it turns out $S_n$ gets really small as $n\rightarrow \infty$. 

$$Var[S_n]=\frac{n\sigma^2}{n^2}=\frac{\sigma^2}{n}\rightarrow 0$$

as $n\rightarrow \infty$.

In fact we have **the weak law of large numbers**:

$\forall \epsilon>0$, $P(\|S_n\|>\epsilon)\rightarrow0$ as $n\rightarrow\infty$.

Proof: By Chebyshev's inequality:

$$P(|S_n|>\epsilon)|\leq\frac{E[|S_n|^2]}{\epsilon^2}=\frac{\sigma^2/n}{\epsilon^2}\rightarrow0$$

What about dividing $X_1+X_2+\cdots+X_n$ by something much smaller than $n$?

Let $W_n=\frac{X_1+X_2+\cdots+X_n}{\sqrt{n}}$, then $E[W_n]=0$ when $n$ is large. $Var[W_n]=\sigma^2$.

So we has a maybe limiting behavior? Yes. Distribution of $W_n$ tends to bell curve (Normal distribution with $\sigma^2$ variance). 

Pick $t\in[0,1]$. Roughly speaking $m\approx nt$.

Let 

$$W_n(t)=\frac{X_1+X_2+\cdots+X_{m(t)}}{\sqrt{n}}$$

we find, $E[W_n]=0$, $Var[W_n]=t\sigma^2$.

The distribution $W_n(t)$ converges to Bell curve with variance $=t\sigma^2$.

The whole entire collection of $\\{W_n(t):t\in[0,1]\\}$ converges to a stochastic process called Brownian motion $W$. It has these properties:

1. $E[W(t)]=0$;
2. $Var[W(t)-W(s)]=\sigma^2(t-s)$;
3. $W(t)-W(s)$ and $W(s)$ are independent;
4. $W(t)-W(s)$ is Normal (bell curve).

------

## Continuous Random Variables (Chapter 3)

**Definition**: A r.v. $X$ is said to be continuous with density $f$ is: $\forall a<b$,

$$P[a\leq x\leq b]=\int_{a}^{b}f(x)dx$$

Properties of densities:

1. $f(x)\geq  0, \forall x$
2. $\int_{-\infty}^{\infty}f(x)d=1$

### Example 1

let $f(x)=ce^{-\lambda x}$, where $x\geq 0$, $c$ and $\lambda$ are positive constants. How should we define $f(x)$ for $x<0$?

Let's say $f(x)=0,\forall x<0$. Do the integration. 

$$\int_{-\infty}^{\infty}ce^{-\lambda x} = -[-\frac{c}{\lambda}] =\frac{c}{\lambda}=1\Rightarrow c=\lambda$$

### Exponential distribution

**Definition**: The r.v. whose density is

$f(x)=0~\forall x<0,\lambda e^{-\lambda x}~\forall x\geq0$ is called Exponential with parameter $\lambda$.

**Notation**: $X\sim Exp(\lambda)$

### Cumulative distribution function (CDF)

**Definition**: The cumulative distribution function (CDF) of $X$ with density is defined as before:

$$F(x)=P(X\leq x)=P(-\infty\leq X\leq x)=\int_{-\infty}^{\infty}f(x)dx$$

- The fundamental theorem of calculus (Leibniz) says $F$ has a derivative, it is $f$.
- Also we see:  $F\in[0,1]$
- $F$ is non-decreasing
- $\lim\limits_{x\rightarrow-\infty}F(x)=0$ 
- $\lim\limits_{x\rightarrow\infty}F(x)=1$

### Example 2

If $X\sim Exp(\lambda)$, then we find $F(x)=0$ for $x\leq0$. 

$$F(x)=\int_{0}^{x}\lambda e^{-\lambda y}dy=1-e^{-\lambda x}$$

Note: the tail of $X$ is defined as $G(x)=P(X>x)=1-F(x)$.

For Exponential, $G(x)=e^{-\lambda}$.

**Remark**: If $X$ has density $f$ and $a\in \mathbb{R}$, then $P(x=a)=\int_{a}^{a}f(x)dx=0$.

### Uniform distribution

The r.v. $X$ is said to be uniform between 2 fixed values $a$ and $b$ if its density is a constant $\frac{1}{b-a}$.

What about the CDF? It has 0 at $x=a$ and 1 at $x\geq b$.

------

## Expectation and variance of continuous random variable (Chapter 3.3)

**Definition**: let $X$ have density $f$, then its expectation is 
$$\int_{-\infty}^{\infty}xf(x)dx$$

### Example 3

$X\sim Exp(\lambda)$, $E[X] = \int_{-\infty}^{\infty}xf(x)dx$. 

Integration by parts:

$$\int_{0}^{\infty}udv=[uv]|_0^\infty-\int_{0}^{\infty}vdu$$

Best choice: use a $dv$ whose $d$ is known, and if $u$ is a polynomial that's good because $du$ has a degree one less than $u$. Choice: $dv=\lambda e^{-\lambda x}dx$, $v=-e^{-\lambda x}$, $u=x$, $du=dx$.

$$\begin{align*}
	E[X] &= [x(-e^{-\lambda x})]_0^\infty - \int_{0}^{\infty}-e^{\lambda x}dx \\
	&= \frac{1}{\lambda}
\end{align*}$$

**Exercise**: $X\sim Unif[a,b]$, find $E(X)=\frac{a+b}{2}$.

**Definition**: the variance of $X$ with density $f$ is defined the same as before:

$$Var[X]=E[(X-E[X])^2]=E[X^2]-E[X]^2$$

where $E[X^2]=\int x^2f(x)dx$.

**Exercise**: Verify that $E[X^2]=\frac{2}{\lambda^2}$ for $X\sim Exp(\lambda)$, and $Var[X]=\frac{1}{\lambda^2}$.

$Var[X]=\frac{(a-b)^2}{12}$ for $X\sim Unif(a,b)$.