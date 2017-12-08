---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 7
description: Survival function and its example; transformation of random variables, scale and rate parameters and their examples; Joint probability density and its example; independent continuous random variables.
permalink: /stt-861-lecture-note-7/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-10-18 20:35:32
---

# Portal to all the other notes

- [Lecture 01 - 2017.09.06](/stt-861-lecture-note-1/) 
- [Lecture 02 - 2017.09.13](/stt-861-lecture-note-2/)
- [Lecture 03 - 2017.09.20](/stt-861-lecture-note-3/)
- [Lecture 04 - 2017.09.27](/stt-861-lecture-note-4/)
- [Lecture 05 - 2017.10.04](/stt-861-lecture-note-5/)
- [Lecture 06 - 2017.10.11](/stt-861-lecture-note-6/)
- [Lecture 07 - 2017.10.18](/stt-861-lecture-note-7/) -> This post
- [Lecture 08 - 2017.10.25](/stt-861-lecture-note-8/)
- [Lecture 09 - 2017.11.01](/stt-861-lecture-note-9/)
- [Lecture 10 - 2017.11.08](/stt-861-lecture-note-10/)
- [Lecture 11 - 2017.11.15](/stt-861-lecture-note-11/)
- [Lecture 12 - 2017.11.20](/stt-861-lecture-note-12/)
- [Lecture 13 - 2017.11.29](/stt-861-lecture-note-13/)
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/)

# Lecture 07 - Oct 18 2017

## Survival function

**Definition**: Survival function $S$ of a r.v. $X$ is 1-CDF.

$$S(x)=1-F(x)=P(X>x)$$

if $F$ is the CDF of $X$.

This is meaningful especially if $X$ is a waiting time. Indeed $S(x)$ is the chance of survival to "age" $x$.

### Example 1

Memoryless property of the exponential distribution. Let $X\sim Exp(\lambda)$. We know the CDF $F(x)=1-e^{-\lambda x}$. Then 

$$S(x)=1-F(x)=e^{-\lambda x}$$

Important: this characterizes the exponential distribution. 

Q: What is $P(X+h\|X>x)$ (P(Given X survival to age $x$, what is the chance of survival $h$ units of time longer))?

A: 

$$\begin{align*}
	P&=\frac{P(\{X>x\}\cap\{X>x+h\} )}{P(X>x)}\\
	&=\frac{P(X>x+h)}{P(X>x)} \\
	&=\frac{S(x+h)}{S(x)} \\
	&= e^{-\lambda h}
\end{align*}$$

This proves that for $X\sim exp(\lambda)$, the information of how long we have survived tells us nothing about the likelihood of surviving $h$ units of time longer (Nothing to do with $x$, the current "age").

**FACT**: in a Poisson($\lambda$) process, the waiting time between two jumpers (arrivals) are i.i.d. $Exp(\lambda)$ r.v.'s.

Sketch of proof: Let's prove first that $X_1\sim Exp(\lambda)$.

This $X_1$ is the first time that $N$ reaches 1. 

The event $\\{X_1<t\\}$ is the same as $\{N_t\geq 1\}$.

Therefore,

$$\begin{align*}
	P(X_1<t) &= P(N_t\geq 1) \\
	&= 1-P(N_t=0) \\
	&= 1-e^{\lambda t}
\end{align*}$$

We also see this is the cdf of $X_1$ . We recognize the formula as $F_{X_1}(t)=1-e^{-\lambda t}$.

Now, let's convince ourselves that $X_2\sim Exp(\lambda)$ and $X_1$ and $X_2$ are independent. This is true because $N$ has independent increments. This is related to the memoryless property of $X_i$'s.

### Example of transformation of r.v.'s

Let $X\sim Exp(1)$, let $\lambda>0$ be fixed (not random). Let $Y=\frac{1}{\lambda}X$. Let's find the distribution of $Y$ via its CDF.

$$S_Y(y)=P(Y>y)=P(\frac{x}{\lambda})=P(x>\lambda y)$$

$$=\left\{~{\begin{array}{*{20}{c}}
	{\mathop e^{-\lambda y}} & y\geq 0 \\
	{\mathop 1} & y<0
	\end{array}~}\right.$$

We recognize, via this survival function, that $Y$ has the same CDF as $Exp(\lambda)$.

### Example 2

Let $U\sim Uniform(0,1)$. Let $Y=-\ln U$. Find $Y$'s law (distribution) via the survival function. (Note: when $\ln U<0$, $Y>0$)

A: 

$$\begin{align*}
	P(Y>y) &= P(-\ln U >y) \\
	&= P(\frac{1}{U}>e^y) \\
	&= P(U<e^{-y}) \\
	&= e^{-y} \textrm{ (F(U)=u)}
\end{align*}$$

(Because the exp function is strictly increasing)

We recognize that $Y\sim Exp(1)$.

Note: if we have $U\sim Uniform(0,1)$, and we want to create a r.v. $Z\sim Exp(\lambda)$, we can take $Z=-\frac{1}{\lambda}\ln(U)$.

### Example of scale and rate parameters

We saw that if we multiply an $Exp$ r.v., with parameter $\lambda$ by a constant $c$, we get $Exp$ with parameter $\frac{\lambda}{c}$.

For instance,

$$Y\sim Exp(\lambda), Y=\frac{1}{\lambda X}$$

$$Z=cY=\frac{c}{\lambda X}\sim Exp(\frac{\lambda}{c})$$

This shows that $\frac{1}{\lambda}$ is a scale parameter.

We also say $\lambda$ is a rate parameter when $X$ is multiplied by $c$. 

For instance, $\lambda$ is the rate of arrivals of the Poisson r.v. (or process) in a time interval of length 1. But $\frac{1}{\lambda}$ is the average waiting time for the next arrival. It is the scale of the waiting time. 

Generally speaking, a r.v. $X$ (or its law) has a scale parameter $\alpha$ if the CDF of $X$ has this form 

$$F_X(x)=\bar{F}(\frac{x}{\alpha})$$

We also say $X$ has a rate parameter $\lambda$ if the CDF of $X$ has this form 

$$F_X(x)=\tilde{F}(\lambda x)$$

### Example 3

We just saw, for $X\sim Exp(\lambda)$,

$$F_X(x)=1-e^{-\lambda x}$$

so 

$$\tilde{F}(y)=1-e^{-y}$$

Also 

$$F_X(x)=1-e^{-\frac{x}{1/\lambda}}$$

$$\bar{F}(y)=1-e^{-y}$$

and $\frac{1}{\lambda}$ is the scale paremeter $\alpha$.

**Theorems**: if $\alpha$ is a **scale parameter** for $X$, then 

$$f_X(x)=\frac{1}{\alpha}f(\frac{x}{\alpha})$$

($\alpha=1$ is the special case)

If $\lambda$ is a **rate parameter** for $X$, then 

$$f_X(x)=\lambda f(\lambda x)$$

($\lambda=1$ is the special case)

Then, let $X_\alpha$ have scale parameter $\alpha$, then 

$$E(X_\alpha)=\alpha E(X_1)$$

$X_1$ is $X_\alpha$ with $\alpha=1$.

$$Var(X_\alpha)=\alpha^2Var(X_1)$$

let $X_\lambda$ have rate parameter $\lambda$, then

$$E(X_\lambda)=\frac{1}{\lambda}E(X_1)$$

$$Var(X_\lambda)=\frac{1}{\lambda^2}Var(X_1)$$

**Theorem**: Arbitrary function of random variables.

Let $X$ have density $f_X$. Let $\Psi$ be a strictly monotone function (increasing or decreasing). So $\Psi$' the derivative basically exists, and the inverse function $\Psi^{-1}$ exists. Let $Y=\Psi(X)$. Then $Y$ has this density. 

$$f_Y(y)=f_X(\Psi^{-1}(y))\frac{1}{\Psi'(\Psi^{-1}(y))}$$

Idea of proof:

Start from CDF, of $Y$ and use chain rule.

**Exercise**: Use this theorem to check the $-\ln U \sim Exp(1)$ when $U\sim Uniform(0,1)$.

**Definition**: (Joint probability density) A pair of r.v. $(X,Y)$ has a joint probability density $f_{X,Y}(x,y)$ (a function on $R^2$) if 

$$P(X\in[a,b]~and~Y\in[c,d])=\int_{c}^{d}\Big(\int_{a}^{b}f_{X,Y}(x,y)dx\Big)dy$$

**Definition** (More like a theorem): if $f_{X,Y}(x,y)$ as above is really $=f_X(x)f_Y(y)$, then $X$ and $Y$ are independent.

Proof: 

$$\begin{align*}
	P(X\in dx\cap Y\in dy)&=f_{X,Y}(x,y)dxdy\\
	&=f_X(x)f_Y(y)dxdy\\
	&=f_X(x)dxf_Y(y)dy \\
	&=P(X\in dx)P(Y\in dy)
\end{align*}$$

It also proves that $f_x$ is the density of $X$ and $f_Y$ is the density of $Y$. 

### Example 4

Let $f_{X,Y}(x,y)=15e^{-5x-3y}$ if $x\geq0,y\geq0$, and 0 otherwise. We see 

$$f_{X,Y}(x,y)=5e^{-5x}\times 3e^{-3y}=f_X(x)\times f_Y(y)$$

(the places where $f_X$, $f_Y$ and $f_{X,Y}=0$, do match up)
See $X$ and $Y$ independent and $X\sim Exp(5)$ and $Y\sim Exp(3)$.

### Example 5

Let $f_{X,Y}(x,y)=1$ when $x\in[0,1]$and $y\in[0,1]$, =0 otherwise. 
Then $f_{X,Y}(x,y)=f_X(x)\times f_Y(y)$, each of them is i.i.d $Uniform(0,1)$.

### Example 6

Let $f_{X,Y}(x,y)=const$ if $0\leq x\leq y\leq 1$, =0 otherwise. Then the area in a 2D surface is a triangle. The constant is 2. We say that $(X,Y)$ is uniform in that triangle. However, $X$ and $Y$ are not independent. Because we have 

$$X\leq Y$$

This is a non-random relation, so $X$ and $Y$ are dependent.

**General theorem**: For most shapes in $\mathbb{R}^2$ we can define the uniform density on that shape if its area is finite, with parameter of $\frac{1}{area}$. Moreover, if the shape has a center of symmetric then $X$ and $Y$ are independent. When the shape is the rectangle $[a,b]\times [c,d]$. Then $X$ independent $Y$ and $X\sim Uniform [a,b]$, $Y\sim [c,d]$

For a circle shape, $X$ and $Y$ are not independent, but $\rho$ and $\theta$ are independent. 

$$X_1=\rho\cos\theta, Y_1=\rho\sin\theta, (\rho, \theta)$$

are independent.

$$\theta\sim Uniform[0,2\pi]$$

Exercise: find the density of $\rho$.
