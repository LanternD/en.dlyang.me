---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 4
description: Expectation and its theorems, Geometry distribution, Negative Binomial distribution and their examples; Theorem of linerarity, PMF of a pair of random variables, Markov's inequality; variance and its examples, uniform distribution.
permalink: /stt-861-lecture-note-4/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-09-27 20:35:32
---

# Portal to all the other notes

You would encounter a 404 error if I haven't taken the lecture. :-)

I will add this after I finished everything.

# Lecture 04 - Sept 27 2017

## Expectation

$$Avg(X_1)+Avg(X_2)+...+Avg(X_n)=\frac{n}{p}$$

**Definition**: Let $X$ be a (discrete) r.v. with PMF $p_k=P[X=k],k\in Z$. We say that the expectation of $X$ is 

$$E[X]:=\sum_{k=-\infty}^{\infty}x_kp_k$$

### Example 1

A game of dice. Throw 1 die, win \\$ 1 if outcome is even, win \\$ outcome/2 if outcome is odd.

$$E[x]=\frac{1+1+1}{6}+ \frac{0.5+1.5+2.5}{6} = \frac{7.5}{6} = 1.25$$

### Example 2

Let $X\sim Bern(p)$, thus $E(X)=p$.

### Example 3

Let $X\sim Bin(n,p)$, $E(X)=\sum_{k=0}^{n}kC_n^kp^k(1-p)^{n-k}$, this is the dumb way to solve.

Another way, use linearity, 

$$E[X]=\sum E[X_i]=n \times p$$

### Example 4

Let $X\sim Geom(p)$, then $E[x]=\frac{1}{p}$ (prove this at home). Here is a [link](https://math.stackexchange.com/questions/605083/calculate-expectation-of-a-geometric-random-variable) to it. I don't want to type it again.

### Example 5

Let $X\sim NegBin(X)$, then

$$E[X]=\sum E[X_i]=\frac{n}{p}$$
 
### Try at home

Find the definition, PMF and expectation for the "Multinomial" distribution.

**Theorem of Linearity**: Let $X$ amd $Y$ be two r.v.'s and $\alpha,\beta\in R$ Let $Z=\alpha X+\beta Y$.

$$E[Z]=E[\alpha X+\beta Y]=\alpha E[X] + \beta E[Y]$$

Don't require $X$ and $Y$ be independent.

**Theorem** Let $X$ and $Y$ be two independent r.v.'s, then

$$E[XY]=E[X]E[Y]$$

(try to prove it at home)

### PMF of $(X,Y)$

For $(X,Y)$ a pair of r.v.s, we can define PMF of $(X,Y)$:

$$p_{x,y}=P[X=x~and~Y=y]$$

Note: if $X$ and $Y$ are independent, then $p_{x,y}=p_xp_y=P[X=x]P[Y=y]$.

### Example 6

Let $Y=X^2$ where $X$ is a r.v. Assume $P[X=k]=p_k$, then 

$$E[Y]=E[X^2]=\sum_{k=-\infty}^{\infty}(x_k)^2p_k$$

**Theorem**: Let $X$ be a r.v.with PMF $P[X=x_k]=p_k$, let $F$ be a function from $\mathbb{R}$ to $\mathbb{R}$, let $Y=F(X)$, Then 

$$E[Y]=E[F(X)]=\sum_{k=-\infty}^{\infty}F(x_k)p_k$$

**Theorem**: Let $X$ be a r.v. such that $X\geq 0$ ($P[X\geq 0]=1$). Then $E[X]\geq0$. Proven by the definition. 

**Theorem (Markov's inequality)**: Let $X$ be a non-negative r.v. Let $X$ be fixed real $>0$. Then

$$P[X>C]\leq \frac{E[X]}{C}$$

(Chebyshev inequality is related to Markov inequality).

## Variance (Chapter 1.6)

Empirically the variance is the average squared deviation from the mean. 

With data $x_1, x_2,...,x_n$, let 

$$\mu=\frac{1}{n}\sum_{i=1}^{n}x_i$$

and 

$$\sigma^2=variance=\frac{1}{n}\sum_{i=1}^{n}(x_i-\mu)^2$$

Mathematically, variance is defined as:

Let $X$ be a r.v. 

$$Var(X)=E[(X-E[X])^2]$$

(General formula)

Here we used the approximate corresponding $\frac{1}{n}\leftrightarrow X$, $\mu\leftrightarrow E[X]$.

**Proposition**: $Var(X)=E[X^2]-(E[X])^2$. This is extremely important, especially in doing homework. :-)

Proof:

$$\begin{align*}
	Var(X)&=E[(X-E[X])^2] \\
	&=E[X^2-2XE[X]+(E[X])^2] \\
	&=E[X^2]-E[2XE[X]]+E[(E[X])^2] \\
	&=E[X^2]-2E[X]^2+E[X]^2 \\
	&=E[X^2]-(E[X])^2
\end{align*}$$

Usually if PMF of $X$ is given, it is easier compute to $Var(X)$ using the 2nd formula than the original definition. 

### Usual Notation

Let $X$ be a r.v. 

- $\mu:=E[X]$  
- $\sigma^2:=Var[X]$  
- $\sigma:=\sqrt{Var[X]}$ aka "the standard deviation"

### Example 7

Let $X$ have this PMF: for $k=1,2,3,4$, $p_k=P[X=k]=\frac{k}{10}$.

Then $$\mu=E[X]=\frac{1+4+9+16}{10} = 3,$$

$$E[X^2]=\frac{1+8+27+64}{10}=10$$

Finally, $Var[X] = E[X^2]-E[X]^2 = 10-9=1$

**Properties of the variance**: Let $c\in R$, let $X$ & $Y$ be independent r.v. Then 

- $Var(cX)=c^2Var(X)$  
- $Var(X+c) = Var(X)$  
- $Var(X+Y) = Var(X)+Var(Y)$ (prove this at home)  

### Example 8

Let $X\sim Binom(n,p)$, therefore, 

$$X=\sum_{i=1}^{n}X_i$$

where $X_i$ are i.i.d $Bernoulli(p)$. Thus 

$$Var(X)=Var(X_1)+Var(X_2)+...+Var(X_n)$$

Variance of Bernoulli:

$$Var(X_i)=E[X_i^2]-E[X_i]^2=p-p^2=p(1-p)$$

Thus,

$$Var(X)=np(1-p)$$

In Ch2, we will calculate $Var(X\sim Geom(p))=\frac{1-p}{p^2}$.

Let $X\sim NegBin(n,p)$, then $Var(X)=\frac{n(1-p)}{p^2}$.

**Proposition**: Let $X$ be a r.v. Let $c\in R$, then

$$E[(X-c)^2]=Var(X)+(c-\mu)^2$$

where $\mu=E[X]$.

Proof: 

$$\begin{align*}
	E[(X-c)^2]&=E(X-\mu+\mu-c)^2 \\
	&=E[(X-\mu)^2+2(X-\mu)(\mu-c)+(\mu-c)^2] \\
	&=Var(X)+0+(\mu-c)^2 \\
	&=Var(X)+(\mu-c)^2
\end{align*}$$

Indeed, for $c=x$, we get the definition of $Var(X)$. For $c\neq\mu$ we get 

$$E[(X-c)^2]>Var(X)$$

### Example 9

Let $X$ be a uniform r.v. is the set of integers from 1 to $N$, $P[X=k]=\frac{1}{N}$ for $k=1,2,3,...,n$ (definition).

Then 

$$E[N] = \frac{N+1}{2},$$

$$Var(N)=\frac{N^2-1}{12}$$

------

## End note

Sometimes people (the professor) use different notation for expectation and variance, 

- $E[X]$ or $E(X)$  
- $Var[X]$ or $Var(X)$  

Just choose whichever you like. I prefer ( ) to [ ].