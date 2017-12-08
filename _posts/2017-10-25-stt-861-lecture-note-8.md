---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 8
description: Proof of the biased sample mean; Example 3.5.3 in the text book; Normal distribution, joint normal distribution (multivariate), Gamma distribution.
permalink: /stt-861-lecture-note-8/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-10-25 20:35:32
---

# Portal to all the other notes

- [Lecture 01 - 2017.09.06](/stt-861-lecture-note-1/) 
- [Lecture 02 - 2017.09.13](/stt-861-lecture-note-2/)
- [Lecture 03 - 2017.09.20](/stt-861-lecture-note-3/)
- [Lecture 04 - 2017.09.27](/stt-861-lecture-note-4/)
- [Lecture 05 - 2017.10.04](/stt-861-lecture-note-5/)
- [Lecture 06 - 2017.10.11](/stt-861-lecture-note-6/)
- [Lecture 07 - 2017.10.18](/stt-861-lecture-note-7/)
- [Lecture 08 - 2017.10.25](/stt-861-lecture-note-8/) -> This post
- [Lecture 09 - 2017.11.01](/stt-861-lecture-note-9/)
- [Lecture 10 - 2017.11.08](/stt-861-lecture-note-10/)
- [Lecture 11 - 2017.11.15](/stt-861-lecture-note-11/)
- [Lecture 12 - 2017.11.20](/stt-861-lecture-note-12/)
- [Lecture 13 - 2017.11.29](/stt-861-lecture-note-13/)
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/)

# Lecture 08 - Oct 25 2017

## For video record

(This part is similar to previous note. We recorded a video for it so the professor talked about it once again.)

Basically it is the prove that sample variance $\hat{\sigma}^2=\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2$ biased. 

Recall, 

$$\bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i$$

$$\hat{\sigma}^2=\frac{1}{n}\sum_{i=1}^{n}(x_i-\bar{x})^2$$

Note that $\bar{x}$ is the expectation of a r.v. $\hat{X}$ which takes the value $x_i$ with probability = $\frac{1}{n}$.

Therefore

$$\bar{x}=E(\hat{X})$$

and 

$$Var(\hat{X})=\hat{\sigma}^2$$

Now recall the formula:

$$E((X-c))^2=Var(X)+(E(X)-c)^2$$

$$\Leftrightarrow  Var(X)=E((X-c)^2)-(E(X)-c)^2$$

Use this with $X=\hat{X}$ defined above:

$$\hat{\sigma}^2=\frac{1}{n}\sum_{i=1}^{n}(x_i-c)^2-(\bar{x}-c)$$

Now the question is: what is the bias of $\hat{\sigma}^2$? For this we replace each $x_i$ by $X_i$, where $X_i$'s are i.i.d with mean $=\mu$ and variance$=\sigma^2$. The resulting expression is 

$$\hat{\sigma}^2(X)=\frac{1}{n}\sum_{i=1}^{n}(X_i-\bar{X})^2$$

We are interested in $E(\hat{\sigma}^2(X))$. We want to know if this $=\sigma^2$ or not. 

Now use formula above with $C=\mu$ and $x=X$ and we take $E$ on both side.

$$\begin{align*}
E(\hat{\sigma}^2) &=E(\frac{1}{n}\sum_{i=1}^{n}(X_i-\mu)^2) - E((\bar{X}-\mu)^2) \\
&= E(\frac{1}{n}\sum_{i=1}^{n}(X_i-\mu)^2) - Var(\bar{X})\\
&=\frac{1}{n}\sum_{i=1}^{n}Var(X_i)-\frac{1}{n}Var(x_i)\\
&=\frac{1}{n}\sum_{i=1}^{n}Var(X_i)-\frac{\sigma^2}{n}\\
&=\sigma^2-\frac{1}{n}\sigma^2
\end{align*}$$

We proved that $E(\hat{\sigma}^2)=(1-\frac{1}{n}\sigma^2)$. It is biased with $\frac{1}{n}\sigma^2$.

## Example 3.5.3, Page 100

$(X,Y)$ has density $f(x,y)$ is 2 if $0\leq y\leq y\leq1$, and 0 otherwise.

First compute the joint CDF of $(X,Y)$,

**General definition**

$$\begin{align*}
	F(u, v)&=P(X\leq u, Y\leq v)\\
	&= \int_{-\infty}^{x}(\int_{-\infty}^{y}f(x, y)dy)dx \\
	&=\int_{0}^{x}(\int_{0}^{y}f(x, y)dy)dx 
\end{align*}$$

If $u\geq v$, we integrate $y$ between 0 and $x$,

$$\int_{0}^{v}f(x,y)dy=\int_{0}^{\min(v,x)}dy=2\min(v,x)$$

Now we integrates between $0$ and $u$ with respect to $x$.

$$\begin{align*}
&\int_{0}^{u}2\min(v,x)dx \\
&=\int_{0}^{v}2\min(v,x)dx + \int_{u}^{v}2\min(v,x)dx \\
&= v^2-2v(u-v)
\end{align*}$$

So we have proved that when $u>v$, 

$$F(u,v)=v^2+2v(u-v)$$

If $u<v$, we still compute the same integral

$$\begin{align*}
	&\int_{0}^{u}2\min(v,x)dx\\
	&= u^2
\end{align*}$$

($0<u<v$)

This proven $F(u,v)=u^2$ when $u<v$.

Compute the marginal density of $x$ and $y$.

In general, marginal density $f_X(x)=\frac{\partial }{\partial x}F(x,y)$ when fixing $y$. Similarly, $f_Y(y)=\frac{\partial}{\partial x}F(x,y)$ where $x$ is fixed.

If $x>y$,

$$f_X(x)=2y (constant)$$

If $x<y$, then $f_X(x)=2x$.

$$f_X(x)=2x $$

## Special continuous distributions - Chapter 4

**Definition**: $X$ is a normal with parameters $0$ and $1$ if it has this density

$$f(x)=\frac{1}{\sqrt{2\pi}}e^{-x^2/2}$$

Facts: 

- $E(X)=0$, because the density is 0; 
- $Var(X)=1$ (prove this using one integration by parts)

Notation: $X\sim N(0,1)$.

**Definition**: $X$ is normal with parameters $\mu$ and $\sigma^2$ if it has the density

$$f(x)=\frac{1}{\sqrt{2\pi\sigma^2}}\exp(-\frac{1}{2\sigma^2}(x-\mu)^2)$$

Facts:

- $E(x)=\mu$
- $Var(x)=\sigma^2$

Notation: $X\sim N(\mu,\sigma)$

Proof: comes from the case $N(0,1)$ by using change of variables.

Fact: let $X\sim N(0,1)$, let $\mu$ and $\sigma$ be fixed. Let $Y=\mu + \sigma X$. Then $Y\sim N(\mu, \sigma^2)$.

Fact: let $X$ and $X'$ be two independent r.v.'s respectively, $N(\mu,\sigma^2)$, $N(\mu', \sigma'^2)$, then

$$Y=X+X'\sim N(\mu+\mu',\sigma^2+\sigma'^2)$$

Moral of the story: the class of normal r.v.'s is stable by linear combination. 

## Example 1

let $X\sim N(1,1)$, $Y\sim N(0,4)$, $Z\sim N(-2,1)$. Assume they are independent. $V=2X+3+Y-4Z$. Find $E(V)$, $Var(V)$.

A: By the above moral, $V$ should be normal.

$E(V)=13$, $Var(V)=24$

## Example 2

Let $X\sim N(\mu, \sigma^2)$, let 

$$Z=\frac{x-\mu}{\sigma}$$

so $E(Z)=0$, $Var(Z)=1$. Because $Z$ is a linear transformation of $X$. 

### Joint normal distribution (multivariate normal)

**Definition**: The vector $(X_1,X_2,...,X_n)$ is normal with mean $\mu\in\mathbb{R}^n$ and covariance matrix $C$. (here $\vec{\mu}=\\{\mu_i\\},i=1,2,...,n$, 
$C={c_{ij}}\_{i,j=1}^n$, and $E(x_i)=\mu_i$, $cov(x_i,x_j)=c_{ij}$ and sometimes people use the letter $Q$ or $\Sigma$ instead of $C$), if its joint density is 

$$\begin{align*}
	f(x_1,x_2,...,x_n)&=\frac{1}{(2\pi)^{n/2}}\frac{1}{\sqrt{\det C}}\exp(-\frac{1}{2}(x-\mu)^TC^{-1}(x-\mu))	
\end{align*}$$

(Notice: $x$ and $\mu$ are column vectors)

The stuff in $\exp()$ is 

$$(x-\mu)^TC^{-1}(x-\mu)=\sum_{j=1}^{n}\sum_{i=1}^{n}(x_i-\mu_i)C^{-1}_{ij}(x_j-\mu_j)$$

Sample case, $n=1$, $C=(\sigma^2)$, so $\det(C)=\sigma^2$ and $\frac{1}{\det (C)}=\frac{1}{\sqrt{\sigma^2}}$

So 

$$(x-\mu)^TC^{-1}(x-\mu)=\frac{(x-\mu)^2}{\sigma^2}$$

This matches $f(x)$.

when $n=2$ with independent $x_1$ and $x_2$.

$$\det(C)=\sigma_1^2\cdot \sigma_2^2$$

$$\begin{align*}
	f(x_1,x_2)&=\frac{1}{2\pi\sqrt{\sigma_1^2\sigma_2^2}}\exp\Big(\sum_{j=1}^{2}\sum_{i=1}^{2}(x_i-\mu_i)C_{ij}(x_j-\mu_j)\Big)\\
	&=\frac{1}{2\pi\sqrt{\sigma_1^2\sigma_2^2}}\exp\Big(-\frac{1}{2}\sum_{i=j=1}^{2}(x_i-\mu_i)\frac{1}{\sigma_i^2}(x_i-\mu_i)\Big) \\
	&= \frac{1}{2\pi\sqrt{\sigma_1^2\sigma_2^2}}\exp\Big(-\frac{1}{2}(\frac{(x_1-\mu_1)^2}{\sigma_1^2}+\frac{(x_2-\mu_2)^2}{\sigma_2^2})\Big) 
\end{align*}$$

In general, if $x_1,x_2,...,x_n$ are independent normals, $N(\mu_i,\sigma_i^2), i=1,2,...,n$, then

$$\begin{align*}
f(x_1,x_2,...,x_n)&=\frac{1}{(2\pi)^{n/2}\prod_{i=1}^{n}\sqrt{\sigma_i}}\exp\Big(-\frac{1}{2}||(\frac{x_i-\mu_i}{\sigma_i})_{vector}||_{eucli}^2 \Big)\\
&=\frac{1}{(2\pi)^{n/2}\prod_{i=1}^{n}\sqrt{\sigma_i}}\exp\Big(-\frac{1}{2}\sum_{i=1}^{n}(\frac{x_i-\mu_i}{\sigma_i})^2 \Big)
\end{align*}$$

We recognize that if $Cov(x_i,x_j)=0$ and $(x_i,x_j)$ are bivariate normal, then $x_i$ and $x_j$ are independent.

Normally, $Cov(x_i,x_j)\nRightarrow$ (can not infer) $x_i$ and $x_j$ are independent. But it does when $(x_i,x_j)$ is bivariate normal.

**Question**: let's create a multivariate normal vector $Y$ with covariance matrix $C$ to create a vector $X=(x_1,x_2,...,x_n)$, where all $x_i$'s are i.i.d $N(0,1)$ (``standard normals'').

(It's easy to use Box-Mueller transformation to do so).

How to create a $Y$ from this $X$?

**Answer**: Recall the notion of square-root of a matrix ($C$ is positive definite).

(Linear algebra: $M^TM = MM^T = C$)

There exists a matrix $M$ which is ``$\sqrt{C}$''.

Consider 

$$Z=MX$$

We know (by stability by linear combinations) that $Z$ is multivariate normal. 

Note 

$$E(Z)=ME(X)=0$$

What about $Cov(Z)$?

$$\begin{align*}
Q_{ij}&=Cov(Z_i,Z_j) \\
&= E[Z_iZ_j] \\
&= E\big((\sum_{k=i}^{n}M_{ik}x_k)\cdot(\sum_{l=1}^{n}M_{jl}x_l)\big)\\
&= \sum_{k=1}^{n}\sum_{l=1}^{n}M_{ik}M_{jl}E(x_kx_l)\\
&= \sum_{k=1}^{n}M_{ik}M_{jl} (*** E(x_kx_l)=1~where~i=j)\\
&=(MM^T)_{ij}
\end{align*}$$

So we see that $Y=Z=``\sqrt{X}"$.

**Exercise**: For $n=2$, find a square-root for a $2\times 2$ matrix. There should be a place in the book where the author does that in hiding for the purpose of creating a bivariate normal.

## Gamma distribution - Chapter 4.3

**Definition**: A r.v. $X$ is Gamma with shape parameter $\alpha$ and scale parameter $\theta$ if it has this density

$$f(x)=c (\frac{x}{\theta})^{\alpha-1}\theta^{-1} \exp(-\frac{x}{\theta})$$

where the constant $c=\Gamma(\alpha)$, if $\alpha=n$ is an integer, $\Gamma=(n-1)!$

Notation: $X\sim \Gamma(\alpha,\theta)$.

Fact:

- when $\alpha=1$: $X\sim Gamma(1,\theta)=\exp(\lambda=\frac{1}{\theta})$. 
- Consider a sequence $X_1, X_2,..., X_n$, which are $\sim \Gamma(\alpha_1, \theta), \Gamma(\alpha_2, \theta), ..., \Gamma(\alpha_n, \theta)$. Assume they are independent. Then, with $X= X_1+X_2+\cdots+X_n$, we get 

$$X\sim\Gamma(\alpha_1+\alpha_2+\cdots+\alpha_n, \theta)$$

Consequently, apply the above with $\alpha_1=\alpha_2=\cdots=\alpha_n=1$, the sum of $n$ i.i.d r.v.'s $\sim\exp(\lambda=\frac{1}{\theta})$ is a r.v. $\sim \Gamma(n, \theta)$.

Specifically, this proves exactly that the $n$th ``arrival'' time of a $Pos(\lambda)$ process is a $\Gamma(n,\frac{1}{\lambda})$ r.v.

- $E(X)=n\theta$, because $E(X_i)\frac{1}{\lambda}=\theta$
- $Var(X)=n\theta^2$
- When $\alpha$ is not an integer, $\alpha\notin \mathbb{N}$, let $X\sim\Gamma(\alpha, \theta)$, $E(X)=\alpha\theta$, $Var(X)=\alpha\theta^2$. (Exercise: prove this at home).

