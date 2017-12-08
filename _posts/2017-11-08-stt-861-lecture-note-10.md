---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 10
description: Solving a problem in midterm exam; conditional distribution, definition, example and its expectation and variance.
permalink: /stt-861-lecture-note-10/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-11-08 20:45:32
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
- [Lecture 09 - 2017.11.01](/stt-861-lecture-note-9/)
- [Lecture 10 - 2017.11.08](/stt-861-lecture-note-10/) -> This post
- [Lecture 11 - 2017.11.15](/stt-861-lecture-note-11/)
- [Lecture 12 - 2017.11.20](/stt-861-lecture-note-12/)
- [Lecture 13 - 2017.11.29](/stt-861-lecture-note-13/)
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/)

# Lecture 10 - Nov 08 2017

## Exam question

Let $X\sim U(50,90)$, $Z\sim U(70,90)$, $Law(Z) = Law(X\|X\geq 70)$.

Q: Let $X\sim U(a,b)$, $c\in (a,b)$, find law ($X\|X>c$).

A: let $F$ be the CDF of $X\|X>c$. Let $x\in [c,b]$.

$$F(x)=P(X\leq x|x>c)=\frac{P(X\leq x, X|c)}{P(X>c)}=\frac{\frac{x-c}{b-a}}{\frac{b-c}{b-a}}=\frac{x-c}{b-c}$$

It is uniform in $(c, b)$.

------

## Conditional distribution - Chapter 5

Recall joint density of a vector $(X,Y)$ is $f_{X,Y}(x,y)$, $x$ and $y$ are real numbers.

**Definition (Theorem)**: The conditional law of $X$ given $Y$ is 

$$f_{X|Y}(x|y) = \frac{f_{X,Y}(x,y)}{f_Y(y)}}$$

Consequently, the CDF of $X$ given $Y=y$ is 

$$F_{X|Y}=P(X\leq x|Y= y)=\int_{-\infty}^{x}f_{X|Y}(u,v)du$$

Discrete case using the same idea.

For $Y$, no change in notation.

For $X$, use $\sum$ instead of integrals.

## Example 1

Let $N\sim Poi(\lambda)$ and $X\sim Bin(N,\theta)$, here we see law $(X\|N=k)=Bin(k,\theta)$.

This type of example is called a mixture. A mixture is when the parameter of one random variable is determined by the value of another random variable.

In our example, we would like to find law $(X)$ unconditional on $N$. We want to find $P(X=i)$ for any $k=0,1,2,...$.

$$\begin{align*}
	P(X=i) &= \sum_{k=i}^{\infty}P(X=i ~and~N=k) \\
	&= \sum_{k=i}^{\infty} P(X=i|N=k)P(N=k) \\
	&= \sum_{k=i}^{\infty} C_k^i \theta^i(1-\theta)^{k-i} e^{-\lambda}\frac{\lambda^k}{k!} \\
	&= \sum_{k=i}^{\infty}\frac{k!}{i!(k-i)!}\theta^i(1-\theta)^{k-i}e^{-\lambda}\frac{\lambda^k}{k!} \\
	&= \frac{e^{-\lambda}\theta^i}{i!}\sum_{k=i}^{\infty}\frac{(1-\theta)^{k-i}}{(k-i)!}\lambda^k \\
	&= \frac{e^{-\lambda}\theta^i}{i!}\sum_{k'=0}^{\infty}
	\frac{(i-\theta)^{k'}}{k'!}\lambda^{k'+i} \\
	&= \frac{e^{-\lambda}(\theta\lambda)^i}{i!}\sum_{k'=0}^{\infty}
	\frac{(i-\theta)^{k'}}{k'!}\lambda^{k'} \\
	&= \frac{e^{-\lambda}(\theta\lambda)^i}{i!}e^{\lambda(1-\theta)} \\
	&= e^{-\lambda\theta}\frac{(\lambda\theta)^i}{i!}
\end{align*}$$

It is Poisson distribution with parameter $\lambda'=\lambda\theta$.

## Home exercise

Read and understand the section of the book in Chapter 5 on Markov Chains.

## Conditional expectations - Chapter 5.2

$$E(X|Y=y)=\int_{-\infty}^{\infty}f_{X|Y}(x|y)xdx$$

For the discrete case,

$$E(X|Y=y)=\sum_{k=-\infty}^{\infty}P_{X|Y}(x_k|y)x_k$$

### Super important theorem (definition)

let $X$ and $Y$ be given. Let 

$$g(x)=E(Y|X=x)$$

$$v(x)=Var(Y|X=x)=E(Y^2|X=x)-(E(Y|X=x))^2 = E((Y-g(x))^2|X=x)$$

**Theorem**: $E(XY) = E(Xg(x))$

(the idea of "tower property": $E(E(Z\|X))=E(Z)$. "Given $X$" means $X$ is not random).

Proof: use the property to prove the theorem

$$\begin{align*}
	E(XY) &= E(E(XY|X)) \\
	&= E(XE(Y|X)) \\
	&= E(Xg(X))
\end{align*}$$

Notice: 

- this is the function $g$ with $x$ replaced by $X$.
- $E(h(X)Y) = E(h(X)g(X))$. If we put $X$ in another function.

Now recall $v(x)$. It turns out 

$$Var(Y)=E(v(X)) + Var(g(X)) = E(v(x))+var(E(Y|X))$$

Explanation: The unconditional variance of $Y$ is the expected conditional variance plus the variance of the conditional expectation.

## Example 2

Let $X\|N \sim Bin (N,\theta)$, $N\sim Poi(\lambda)$.

(We found that $X\sim Poi(\lambda)$)

From the theorem, ignoring the fact above, we apply $E(X)=E(E(X\|N))$

If we give some information and then take the information away, it is equivalent to not giving information at the first place.

$$E(X)=E(E(X\|N))=\theta E(N)=\lambda\theta$$

$$E(Poi(\lambda\theta))=\lambda\theta$$

We verify the theorem above.

For variance

$$Var(X)=E(v(N))+Var(E(X|N)) = N\theta(1-\theta) + N\theta=\theta(1-\theta)\lambda+\theta^2\lambda = \lambda\theta$$

This is also correct.
