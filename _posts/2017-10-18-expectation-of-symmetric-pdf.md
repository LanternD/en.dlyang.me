---
layout: post
title: Find the Expectation of a Symmetric Probabiliry Density Function
description: If the PDF is symmetric about c, show that E(X)=c. This is a homework problem for course STT802-002 Theory of Probabilities and Statistics I in MSU.
permalink: /expectation-of-symmetric-pdf/
categories: [blog]
tags: [course, probability, function, problem, solution]
date: 2017-10-18 16:35:32
---

# Problems

Suppose that X has a density $f$ that is symmetric about $c$. That is, $f (c + h) = f (c - h)$ for all real $h$. Show that, if it exists, $E(X) = c$. Hint: Make the change of variable $h = x - c$.

# Solution [^footnote]

$$\begin{align}
	E(X)&=\int_{-\infty}^{\infty}xf(x)dx\\
	&=\int_{-\infty}^{\infty}(c+(x-c))f(x)dx \\
	&= \int_{-\infty}^{\infty}cf(x)dx + \int_{-\infty}^{\infty}(x-c)f(x)dx \\
	&= c + \int_{-\infty}^{\infty}(x-c)f(x)dx
\end{align}$$

We have already had $c$ in the expression, we just need to prove the second term is 0. Let $h=x-c$, then $dh=dx$, $x=h+c$. 

$$\begin{align}
	\int_{-\infty}^{\infty}(x-c)f(x)dx &= \int_{-\infty}^{\infty}hf(h+c)dh\\
	&=\int_{-\infty}^{0}hf(h+c)dh+\int_{0}^{\infty}hf(h+c)dh \\
	&= -\int_{0}^{\infty}(-m)f(c-m)d(-m) +\int_{0}^{\infty}hf(h+c)dh \\
	&= -\int_{0}^{\infty}mf(c-m)dm +\int_{0}^{\infty}hf(h+c)dh \\
	&= 0
\end{align}$$

Therefore,

$$ E(X)=c+0=c $$

[^footnote]: [Proof of $E(X)=aE(X)=a$ when $a$ is a point of symmetry](https://math.stackexchange.com/questions/488989/proof-of-ex-a-when-a-is-a-point-of-symmetry)

