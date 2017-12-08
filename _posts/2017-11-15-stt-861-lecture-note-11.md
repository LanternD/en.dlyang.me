---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 11
description: Proof of the "Tower" property; discrete conditional distribution; continuous conditional distribution expectation and variance and their examples; linear predictor and mean squared error.
permalink: /stt-861-lecture-note-11/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-11-15 20:45:32
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
- [Lecture 10 - 2017.11.08](/stt-861-lecture-note-10/)
- [Lecture 11 - 2017.11.15](/stt-861-lecture-note-11/) -> This post
- [Lecture 12 - 2017.11.20](/stt-861-lecture-note-12/)
- [Lecture 13 - 2017.11.29](/stt-861-lecture-note-13/)
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/)

# Lecture 11 - Nov 15 2017


Reinterpretation of last part of item (c) in proof of Theorem 5.2.1 in textbook.

**Recall** : let $X$, $Y$ be 2 random variables. Just to make things simple,
assume $X$ and $Y$ are discrete, with PMF's $P_x$ and $P_y$ and joint PMF
$P_{X,Y}$.

Generally, for $h$ a function $\mathbb{R}\rightarrow\mathbb{R}$,

\\[E(h(X)Y) = E(h(X)g(X))\\]
 
where \\(g(x)=E(Y\vert X=x)\\).

We want to think of that result in the following way:

- The meaning of the notation \\(g(X)\\) is the value of the function \( g(x) \)
where \\(x\\) is replaced by the random variable \\( x \\).

- However, we reinterpret \\(g(x)\\) as:

\\[ g(X)=E(Y\vert X) \\]

(think of this as a definition.)

Now we reinterpret the formula above like this:

$$\begin{align*}
  E(h(x)|Y) &= E(E(h(X)Y|X)) (\star) \\
  &= E(h(X)E(Y|X))
\end{align*}$$

The first line means "An expectation can always be written as the expectation of
a conditional expectation". It is known as the "tower" property of
conditional expectation.

The second line means: "when conditioning by \\(X\\), \\(X\\) can be considered as
known (non-random) and any factor depending on \\(X\\) can be pulled out of the
conditional expectation".

Proof the Star ($\star$):

$$\begin{align*}
  RHS &= E(h(X)g(X)) \\
      &= E(h(X)E(Y|X)) \\
      &= \sum_{X} h(x)E(Y|X=x)P_X(x) \\
      &= \sum_xh(x)\sum_y f \frac{P_{X,Y}(x,y)}{P_X(x)}\\
      &= \sum_x h(x) \sum_y yP_{X,Y}(x,y) \\
      &= \sum_x\sum_yh(x)yP_{X,Y}(x,y)\\
      &= E(h(X)Y)
\end{align*}$$

(RHS = right hand side) This is the proof of star.

Next, we use star ($\star$) to compute the unconditional variance \\(Var(Y)\\) by
conditional by \\(X\\).

$$\begin{align*}
  Var(Y) &= E((Y-E(Y))^2) \\
         &= E((Y-g(X)+g(X)-E(Y))^2) \\
         &\triangleq E(A^2+2AB+B^2)
\end{align*}$$

where $A=Y-g(X)$, $B=g(X)-E(Y)$. 

We will first compute

$$\begin{align*}
E(AB) &= E((Y-g(X))(g(X)-E(Y)))\\
&=E(E((Y-g(X))(g(X)-E(Y))|X)) \\
& = E(E(Y-g(X)|X)(g(X)-E(Y))) \\
&= E((g(X)-g(X))g(X)-E(Y)) = 0
\end{align*}$$

We have proved

\\[ Var(Y) = E(A^2)+E(B^2) \\]

Now we interpret

$$\begin{align*}
  E(A^2) &= E((Y-g(X))^2) \\
         &= E(E((Y-g(X))^2|X)) \\
         &= E(Var(Y|X))
\end{align*}$$

\\(Var(Y\vert X)\\) is also known as \\(v(X)\\).

So we see \\(E(A^2)=E(v(X))\\) (expectation of conditional variance).

Finally,

$$\begin{align*}
  E(B^2) &= E((g(X)-E(Y))^2)\\
         &= E((g(X)-E(E(Y|X)))^2) \\
         &= E((g(X)-E(g(X)))^2) \\
         &= Var(g(X))
\end{align*}$$

this is the variance of the conditional expectation.

### Homework Problem 5.2.5 Part b

$X$ takes value $\{0,1,2\}$ with probability $\{0.3, 0.4, 0.3\}$, $\varepsilon=\pm1$ with probability 0.5 and 0.5. $Y=5-X^2+\varepsilon$.

Q: Find $\rho=\rho(X,Y)$

\\[\rho(X,Y) = \frac{cov(X,Y)}{\sqrt{Var(X)Var(Y)}}\\]

$$\begin{align*}
  E((X-\mu_X)-(Y-\mu_Y)) &= E(XY)-\mu_X\mu_Y\\
                         &=E(X(5-X^2+\varepsilon))\\
                         &= E(5X-X^3+X\varepsilon) \\
                         &= 5E(X) -E(X^3) =-E(X\varepsilon)\\
                         &=5\mu_X - E(X^3)
\end{align*}$$

### Example 1

\\(N\\) people come into a store in a given day, customer spends \\(X_i\\) dollars.
Let \\(T\\) be the total \$ of sales for the day.

\\[ T= X_1+X_2+\cdots + X_N=\sum_{i=1}^{N}X_i\\]

A: Find \\(E(T)\\) and \\(Var(T)\\).

Assume:

- \\(N\\) is independent of all the \\(X_i\\)'s
- \\(X_i\\)s are i.i.d.

Let's compute

\\[E(T) = E(E(\sum X_i\vert N))\\]

$$\begin{align*}
  E(T) &= E(\sum E(X_i|N))\\
       &= E(NE(X_i))\\
       &=E(X_1)E(N)
\end{align*} $$

We know \\(T\\) is related to \\(N\\). Therefore we must compute conditional
variance

- Conditional variance is \\(v(n) = Var (T\vert N=n)\\)
- Conditional expectation is \\(g(n) = E(T\vert N=n)\\)

\\[Var(T\vert N=n)=Var(\sum X_i\vert N=n) = Var(\sum X_i) = nVar(X_1)\\]

We have just proved that \\(v(n)=nVar(X_1)\\).

Next,

\\(E(T\vert N=n) = E(\sum X_i\vert N=n) = E(\sum X_i) = nE(X_i) \\)

We proved here \\(g(n)=nE(X_1)\\), now finally go back to the original formula,

\\[Var(T) = E(v(N)+ Var(g(N)) = E(NVar(X_1))+Var(N(E(X_1))) = Var(X_1)E(N)+
  E(X_1)^2Var(N)\\]

where \\(T=\sum X_i\\), where \\(X_i\\) are i.i.d and \\(N\\) independent of \\(X_i\\)'s.

**Exercise**: Prove the following (using similar method of proof as for the
\\(Var(T)\\) formula).

\\[Cov(N,T)=E(X_1)Var(N)\\]

and therefore,

\\[\rho (N,T)=\frac{1}{\sqrt{1+\theta}}\\]

where \\(\theta=Var(X)/(E(X_1)Var(N)) \\).

Also, for \\(N\sim Poi(\lambda)\\) and \\(X\sim Ber(\theta)\\), compute \\(Var(T)\\)
and \\(\rho(N,T)\\).

### Example 2

let \\(X\sim Geom(p)\\), \\(D\sim NegBin(p,r=X)\\), therefore, \\(D\\) is a certain
\\(T\\), where the \\(N\\) is the \\(X\\) above and each \\(X_i\\) is \\(\sim Geom(p)\\),
i.i.d.

Let \\(Y=X+D\\), find \\(E(Y)F\\).

\\[E(Y)+E(X)+E(D)=\frac{1}{p} +E(X_1)E(X)=\frac{1}{p}+\frac{1}{p^2}\\]

\\[Var(Y) = Var(X+D)=Var(X)+Var(D)+ 2cov(X,D)\\]


## Continuous Case 

### Example 5.3.2

\\(X\sim \Gamma (\alpha,1)\\), \\(Y\sim \Gamma(\beta,1)\\).

Let \\(V=X+Y\\), therefore, \\(V\sim Gamma(\alpha+\beta,1)\\).

Let \\(V=\frac{X}{X+Y}\\), this is called Beta random variable \\(\sim
B(\alpha+\beta)\\).

Let's now try to prove that \\(U\\) and \\(V\\) are independent.

A: Let \\(g(u)=E(X\vert U=u)\\). It turns out (Wikipedia)
\\(E(V)=\frac{\alpha}{\beta}\\).

Therefore \\(E(UV\vert U=u)=uE(V\vert U=u)=uE(V)=u \frac{\alpha}{\alpha+\beta}\\).

This gives us an example where the function \\(g\\) is linear as a function of
\\(u\\) because \\(E(X|U=u)=E(UV|U=u)=u \frac{\alpha}{\alpha+\beta}\\).

This situation where \\(X\\) is linear given \\(U\\) is pretty exceptional.

We call \\(g(x)=E(Y|X=x)\\) the predictor of \\(Y\\) given \\(X\\). But what is the
linear predictor?

## Linear Predictor and Mean Squared Error

We would like to predict \\(Y\\) using a linear function of \\(X\\).

Let \\(aX+b\\) be the linear predictor. Consider the error in replacing \\(Y\\) by
\\(aX+b\\).

We can choose \\(a\\) and \\(b\\) such that \\(E(Y-aX-b)=0\\).

More systematically, let's consider what statistic cases might called the **mean
square error** (MSE)

\\[E((Y-(aX+b))^2)\\]

we want to minimize MSE over all possible choices of the 2 values \\(a\\) and
\\(b\\). It turns out that \\(a=Corr(X,Y) \frac{\sigma_X}{\sigma_Y}\\) and best \\(b=E(Y)-aE(X)\\).

Note: this is the closely allied to the question of linear regression. It turns
out the MSE fir that pair of \\((a,b)\\) is

\\[1-\rho^2Var(Y)\\]
 
This says: the uncertainty level on \\(Y\\) is \\(Var(Y)\\). The proposition of that
variance which is explained by \\(X\\) is the variance of \\(aX+b\\) is

\\[Var(aX)=a^2Var(X) =\rho\frac{\sigma_Y^2}{\sigma_X^2}\sigma_X^2\\]

and what is not explained by \\(X\\) is the MSE
\\((1-\rho^2)Var(Y)\\).

Summary: with \\((a,b)\\) as above and \\(\sigma_X^2=Var(X)\\), \\(\sigma_Y^2\\). we
see that the amount of variance of \\(Y\\) explained by \\(X\\) is
\\(Var(aX)=\rho^2\sigma_Y^2\\) The MSE \\(=(1-\rho^2)\rho_Y^2\\) is the variance of
\\(Y\\)unexplained by \\(X\\). 

