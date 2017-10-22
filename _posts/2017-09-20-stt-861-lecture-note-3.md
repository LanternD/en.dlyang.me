---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 3
description: Random variable, independent random variable and their examples; Bernoulli distribution, Binomial distribution.
permalink: /stt-861-lecture-note-3/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-09-20 20:35:32
---

# Portal to all the other notes

You would encounter a 404 error if I haven't taken the lecture. :-)

I will add this after I finish everything.

# Lecture 03 - Sept 20 2017

### Example 1.3.8

Chevalier de Méré.

Game \#1: throw a six-sided die 4 times. Win if get a 6 at least once.

Game \#2: throw two six-sided dice 24 times. Win if get double 6 at least one. 

Find their probabilities.

Answer:

$$\begin{align*}
	P(\textrm{win at game 1})&=1-P(\textrm{lose at game 1}) \\ 
	&= 1-(\frac{5}{6})^4 \\
	&=0.5177
\end{align*}$$

$$\begin{align*}
	P(\textrm{win at game 2})&=1-P(\textrm{lose at game 2}) \\ 
	&= 1-(\frac{35}{36})^{24} \\
	&=0.4914
\end{align*}$$

The numbers are close but different.

Blaise Pascal -- First calculator

### Example 1.3.9 

Try it at home

## Random Variables (RV or r.v.)

**Definition**: A r.v. $X$ is a function from a prob space $\Omega$ to a set of numbers $N$. If $N$ is a subset of integer $\mathbb{N}$ then we say that X is discrete; If $N$ is a subset of the real number $\mathbb{R}$, then we saythat $X$ is continuous.

### Example 1

What is the chance that it will take $k$ tries until one success (e.g. one head in coin tosses). Assume $P(1 success)=p$.

Answer:

The sequence of trials leading to this event is:

00...0001, $k-1$ fails, 1 success.

Because of the independence. The prob of that event

$$P(that~event)=(1-p)^{k-1}p$$

This shows that a great choice for our probability space is $\Omega=\{\omega_1, \omega_2, ... ,\omega_k,...\}$, where $\omega_k$ is the elementary outcome "it takes $k$ trials until the first success".

Next question: find the prob. $P(\omega_k)$ for every $k$. 

Answer: 

$$P(\omega_k)=p(1-p)^{k-1}$$

Let's check the axioms of prob. for our prob measure $P$:

$$P(A\cup B)=P(A)+P(B)$$

automatically satisfied.

$$P(A)\geq0$$

automatically satisfied, since $P(\omega_k)\geq0$.

$$P(\Omega)=1?$$

$$\begin{align*}
	\sum_{k=1}^{\infty}P[\omega_k]&=\sum_{k=1}^{\infty}p(1-p)^{k-1}\\
	&= p\sum_{k=0}^{\infty}(1-p)^{k'}\\
	&= p\frac{1}{1-(1-p)}=p\frac{1}{p}=1
\end{align*}$$

(because it is the sum of the whole geometry series with ratio $1-p$) thus the last axiom is satisfied.

Note: looking forward to Chapter 1.4, let $X$ be the \# of trails needed until the first success. Let $\Omega$ be the space of all sequence of successes and failures.

$X$ is defined on this $\Omega$ via the formula:

$X=k$ if $\omega=\omega_k$, $X(\omega_k)=k$.

$$P[X=k]=P(\omega_k)=p(1-p)^{k-1}$$

This defines the prob distribution of the r.v. $X$ be sum of all the values $P[X=k]$ is 1. We say that $p_k=P(X=k)$ is the prob mass function of $X$.

### Example from Chapter 1.3

- Disease: $P(D)=0.006$, fairly rare

- Test for this disease. $V$= a person is pos for this test.

Given $P(V\|D)=0.98$ sensitivity

Given $P(V\|D^C)=0.01$ false positive. This is e.q. to $(1-P(V^C\|D^C)=0.99)$ specificity.

Q1: find $P(V)$. 

A1: 

$$\begin{align*}
	P(V) &= P(V\cap D)+P(V\cap D^C) \\
	&=P(V|D)P(D)+P(V|D^C)P(D^C) \\
	&=0.98\times 0.006 + 0.01\times(1-0.006) \\
	&=0.00588+0.00994=0.01582
\end{align*}$$

Q2: find $P(D\|V)$

A2: Use the definition of conditional probability

$$P(D|V)=\frac{P(V\cap D)}{P(V)}=\frac{0.00588}{0.01582}=0.3717$$

### Example 2

2 dice, so makes same for $\Omega$ to have 36 elementary outcomes. Assume dice are fair & the two tosses are independence. Then let $X$ be sum of the outcome of the 2 dice. 

Possible outcome for $X$ and their prob: See Homework 1.

The notation $X=x$ is really an event & we add up the prob of the individual $\omega$'s inside that event to find $p_x$.

We also say that $p_x$ define the prob distribution of $X$.

## Independent RV

**Definition**: $X$ & $Y$ are indenpendent r.v. if 

$$P(\{X=x\}\cap \{Y=y\})=P(\{X=x\})\times P( \{Y=y\})=p_x\times p_y$$

Note: the pair $(X,Y)$ is known as a bivariate r.v. we use the notation $p_{x,y}$ for $P(X=x \& Y=y)$. The $p_{x,y}$ is the prob mass function of 

Note: if $X$ & $Y$  are not independent, then $p_{x,y}$ not always equal to $p_xp_y$.

### Example 3

Let $X$ be result of one die toss, let $Y$ be the result of another die. 

If the two tosses do not influence each other, then the two r.v.s can be legitimately be modeled as independent. 

### Special discrete distributions

#### Bernoulli Distribution 

**Definition**: A r.v. $X$ is called a Bernoulli r.v. with parameter $p$ if $X=0$ with prob $1-p$, and $X=1$ with prob $p$. 

$p$ is also called success probability. Indeed 0 & 1 can model the failure & success outcomes of a trail. The PMF of $X$ is $p_0=1-p$ and $p_1=p$.

#### Binomial Distribution 

**Definition**: A r.v. $X$ is a Binomial r.v. with parameters $n$ & $p$ if it is the number of successes in a sequence of $n$ independent Bernoulli trails.

"Exactly $x$ heads in 10 coin tosses."

Here we see that if we denote by $x_1, x_2, x_3, ..., x_n$ the corresponding sequence of Bernoulli r.v.

$$X=\sum_{i=1}^{n}x_i$$

(This is definition)

Indeed, all the failures count as 0 in the above sum and all the successes count as 1. 

Big question: It's clear that $X$ takes on the values $x=0,1,2,...,n$ and none others. But what is the PMF of $X$ for all those possible $x$'s. 

Need to think about the event $\\{X=k\\}$. We can determine each elementary outcomes in the event $\\{X=k\\}$ by choosing the position of the $k$ "ones" in a sequence of length $n$. We choose a subset of size $k$ in a set of size $n$. That's one of the outcomes in $\\{X=k\\}$. There are $C^k_n$ ways of doing so. (experiments are independence and the fact that multiplication is commutative.)

$$P(X=k)=C^k_np^k(1-p)^{n-k}$$

(This is theorem)

Note: 

$$\sum_{k=0}^{n}C_n^kp^k(1-p)^{n-k}=1$$

Formula: 

$$(a+b)^n=\sum_{k=0}^{n}a^nb^{n-k}$$

Notation: $X\sim Bernoulli(p)$, $X\sim Binom(n,p)$.