---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 13
description: Recap of linear predictor; almost surely convergence, converge in probability, converge in distribution; central limit theorem, theorem of DeMoivre-Laplace. 
permalink: /stt-861-lecture-note-13/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-11-29 20:45:32
---

# Portal to all the other notes

You would encounter a 404 error if I haven't taken the lecture. :-)

I will add this after I finished everything.

# Lecture 13 - Nov 29 2017

## For Video Recording

### Linear Prediction

Recall $ X, Y $ let

$$ g(x)=E[Y\vert X=x] $$

The r.v. $ g(x) $ is the  best predictor of $ Y $ given $ X $ in the least
square sense: $ g $ minimizes $ E(g(X)-Y)^2) $ = MSE. 

But what about making this MSE as small as possible when $ g $ is linear?
So use notation $ h(x)=a+bx $ (instead of $ g $).

We want to minimize

$$ MSE = E((Y-(a+bX))^2) $$

Find $ a $ and $ b $ to make this as small as possible. Let

$$ Z_Y = \frac{Y-\mu_Y}{\sigma_Y} $$

$$ Z_X = \frac{X-\mu_X}{\sigma_X} $$

We also know,

$$ E(Z_XZ_Y) = Corr(X,Y) = \rho $$

$$ Y-(a+bX) = (Z_Y-cZ_X)\sigma_Y+(d-a) $$

where $ c=b \frac{\sigma_Y}{\sigma_X} $, and $ d=\mu_Y-b\mu_X $,

$$\begin{align*}
  MSE & = \sigma_Y^2E((Z_y-cZ_X)^2) + (d-a)^2 \\
      &= \sigma_Y^2(1-2c\rho +c^2) + (d-a)^2 \\
      &= \sigma_Y^2(1-\rho^2 + (c-\rho)^2) + (d-a)^2
\end{align*}$$

We see immediately that this is minimal for $ a=d $ and $ c=\rho $.

Therefore,

$$ b= \rho \frac{\sigma_Y}{\sigma_X} $$

This answers the question of what the best linear predictor of $ Y $ given $ X
$ is the mean square sense.

We see the smallest MSE is therefore $ \sigma_Y^2(1-\rho^2) $.

Therefore, we see that the proportion of $ Y $'s variance which is not
explained by $ X $ is

$$ \frac{MSE}{\sigma_Y^2}=1-\rho^2 $$

Finally, the proportion of $ Y $'s variance which is explained by $ X $ is $ \rho^2 $. 

------

## Chapter 6 - Convergences

**Definition**: We say that the sequence of r.v.'s $ (X_n)_{n\in\mathbb{N}}
  $ converges ("a.s."(almost surely)) to the r.v. $ X $ if

  
  $$ \lim_{n\rightarrow\infty} X_n=X $$

  with probability 1. In other word,
    
  $$ P(\lim_{n\rightarrow\infty}|X_n-X|) = 1$$

  **Definition**: (A weaker notion of convergence) A sequence of r.v.'s $ (X_n)_{n\in\mathbb{N}}$ converges in probability to $X$ if
    
  $$ \forall \varepsilon >0: P(|X-X_n|>\varepsilon) \rightarrow 0 $$

Note: [Convince yourself as an exercise at home] Convergence in probability is
(easier to achieve) than converge a.s. 

**Definition**: (even weaker version) Let sequence of r.v.'s $ (X_n)_{n\in\mathbb{N}}$ as above but now let $ F $
be the CDF of some distribution. We say $ X_n $ converges in distribution to
  the law $ F $ is

  $$ F_{X_n}(X) \rightarrow F(X) $$

  as $ n\rightarrow\infty$ for every fixed $ x $ where $ F(x) $ is
  continuous.

  Note: unlike the previous two notions, here there is no need for a limiting
  r.v. $ X $ and the $ X_n $'s. Do not need to share a probability space with
  $ X $ or anyone else. 
   
### Example 1

Let $ Y_i $, $ i=1,2,3,... $ be i.i.d with $ \mu $ and
  $ \sigma^2 $ is finite. We proved that, with

  $$ X_n= \frac{Y_1 + Y_2 + \cdots + Y_n}{n} = \mu $$

  then

  $$ P(|X_n-\mu|>\varepsilon) \leq \frac{\sigma^2}{\varepsilon^2n} $$

(By Chebyshev's inequality) 

The whole thing goes to 0 as $ n\rightarrow \infty $, this proves that $
X_n\rightarrow\mu $ in probability.

Note: assuming only $ \mu $ exists ($ \sigma^2 $ could be infinity),
conclusion still holds. See W. Feller's book in 1950. 

Let $ X_n=Uniform\\{1,2,...,n\\} $. This is a stepper function, with $ 1/n $
increment each step. Let's try to find out $ F_{X_n}(x) =\frac{1}{n}[x]$ for
$ x\in [0,n] $ (integer
function, the integer larger than $ x $ ).

For fixed $ x\in\mathbb{R^+} $, as $ n\rightarrow\infty $, $
F_{X_n}(x)\rightarrow 0(\star) $.

Since the function $ \star $, is not the CDF of any random variable, this proves that $
X_n $ does not converge in distribution, And therefore, $ X_n $ cannot
converges in any stronger sense (in probability or a.s.).

How about $ Y_n=Uniform \\{1/n, 2/n, ..., n/n\\} $?

Since

$$ F_{Y_n}(x)\rightarrow x $$

for $ x\in[0,1] $, this is the CDF of $Uniform(0,1)$.

### Example 2

Let $ U_n\sim Unif(0,1) $, i.i.d. Let $ M_n =\max_{i=1,2,...,n}(U_i)$. We
can tell that $ M_n\rightarrow1  $ in some sense. Let's prove it in
probability:

Let $ \varepsilon>0 $,
$$\begin{align*}
  P(\vert M_n-1\vert > \varepsilon) &= P(1-M_n>\varepsilon)  \\
                                   &=P(M_n<1-\varepsilon)\\
                                    &=P(\max_{i=1,2,...,n}U_i<1-\varepsilon) \\
                                    &=P(\forall i: U_i<1-\varepsilon)\\
                                    &=P(\cap_{i=1}^{n}\{U_i<1-\varepsilon\}) \\
                                    &=\prod_{i=1}^{n}P(U_i<1-\varepsilon) =(1-\varepsilon)^n\\
                                      \lim P(\vert M_n-1 \vert >\varepsilon) &=0
\end{align*}$$

We proved that $ M_n\rightarrow1 $ in probability.

Now consider $ Y_n=(1-M_n)n $. Let's see about CDF of $ Y_n $.

$$\begin{align*}
  1-F_{Y_n}(y)  & = P((1-M_n)>y) \\
                &= P((1-M_n)>\frac{y}{n}) \\
                &=P(M_n<1-y/n) \\
                &=P(\prod \{U_i<1-y/n\}) \\
                &=(1-y/n)^n\\
  &\rightarrow e^{-y}
\end{align*}$$

This CDF is exponential. Thus $ Y_n \rightarrow Exp(\lambda = 1)$ in distribution.

------

**Theorem** (6.3.6): Let $ (X_n)\_{n\in\mathbb{N}} $ be a sequence of
r.v.'s. If $ X_n $ has MGF $ M_{X_n}(t) $ and $ M_{X_n}(t)\rightarrow
M_X(t) $ for $ t $  not 0, then $ X_n \rightarrow X$ in distribution.

### Example 3

Let $ X_n $ be Bin($ n,p=\lambda/n $). We know that the PMF of $ X_n $
converges to the PMF of Poisson($ \lambda $). Try it again here. We will find

$$ M_{X_n}(t)=e^\lambda (e^t-1) $$

and here we recognize that this is the MGF of Poisson($ \lambda $). By Theorem
6.3.6, $ X_n\rightarrow Poiss(\lambda) $ in distribution.

Let $ X_i, i=1,2,...,n $ be i.i.d with $ E(X_i)=\mu $ and variance $
Var(X_i)=\sigma^2 $.

Let $ Z_i =\frac{X_i-\mu}{\sigma} $, $ S_n=\frac{\sum_{i=1}^{n}Z_i}{\sqrt{n}}
$,

(We divide by $ \sqrt(n) $ as a standardization and we know $ Var(S_n)=1 $).

## Central Limit Theorem (CLT)

As $ n\rightarrow\infty $, then $ S_n\rightarrow Normal(0,1)$ in distribution.

This means:

$$ \lim P(S_n\leq x) = F_{N(0,1)}(x) =
  \int_{-\infty}^{x}\frac{1}{\sqrt{2\pi}}\exp(-z^2/2) dz $$

The proof just combines the Taylor formula up to the order 2 and Theorem 6.3.6.

------

Next, consider

$$ Y_n = \frac{(\sum_{i=1}^{n}x_i)-n\mu}{\sqrt{n}}=\sigma S_n$$

A corollary of the CLT says this:

$$ Y_n\rightarrow N(0,\sigma^2) $$

in distribution.

Proof:

$$\begin{align*}
 P(Y_n\leq x) & = P(\sigma S_n\leq x) \\
              &=P(S_n\leq\frac{x}{\sigma}) \\
              &=\int_{-\infty}^{x/\sigma}\frac{1}{\sqrt{2\pi}}\exp(-z^2/2) dz
\end{align*}$$

and conclude by changing of variable.

------

## Theorem of DeMoivre-Laplace

Let $ X_i, i=1,2,3,..,n $ be i.i.d Bernoulli. Let $ W_n = X_1+X_2+\cdots+ X_n
$. We know $ W_n\sim Bin(n,p) $.

Let $ S_n =\frac{W_n-np}{\sqrt{np(1-p)}}$,

Therefore, by CLT, $ S_n\rightarrow N(0,1) $ as $ n\rightarrow\infty $ in
distribution.

In other words, to be precise,

$$ \lim P(S_n\leq x) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{x}\exp(-z^2/2)dz$$

$$ P(\frac{W_n-np}{\sqrt{np(1-p)}}\leq x) =P(W_n\leq x\sqrt{np(1-p)}+np) $$

The speed of convergence in the CLT is known as a "Berry-Esseen" theorem. But
the speed of convergence for Binomial CLT is much faster and rule of thrum is $
p\in [1/10, 9/10] $ and $ n\geq 30 $. CLT is good within $ 1\\% $
convergence error.

------

### Example 4

Let

$$ M_n =\frac{U_1+U_2+\cdots+U_n}{n}$$

where $ U_i $'s are i.i.d Uniform(0, 1). We know by Weak law of large numbers,
that $ M_n\rightarrow \frac{1}{2} $ in probability as $ n\rightarrow\infty
$. But how spread out is $ M_n $ around 1/2? For example, can we estimate the
chance that $ M_n $ is more than 0.02 away from its mean value 1/2? 

Answer:

$$\begin{align*}
  P(|M_n-\frac{1}{2}|>0.02) & = 1- P(-0.02 < M_n-\frac{1}{2} <0.02) \\
                           &= 1-P(-0.02<\frac{\sum (U_i-1/2)}{n}) \\
                           &=1- P(-0.02\sqrt{n}<\frac{\sum (U_i-1/2)}{\sqrt{n}}<0.02\sqrt{n}) \\
                           &=1- P(-0.02\sqrt{n}/\sqrt{1/12}<\frac{\sum (U_i-1/2)}{\sqrt{n}}\sqrt{1/12}<0.02\sqrt{n}\sqrt{1/12}) \\
                           &\approx 1-P(-\frac{0.02\sqrt{n}}{\sqrt{1/12}}<N(0,1)<\frac{0.02\sqrt{n}}{\sqrt{1/12}})
\end{align*}$$

We will feel comfortable if $ n $ is large enough to make this greater than
0.95. What value should $ n $ at least be.

In order to get this setup, it is known that the right-hand value should be =
1.96. 

This value

$$ 0.975 = P(N(0,1)\leq 1.95) $$

So 1.96 is therefore know as the 97.5$^{th}$ percentile of $ N(0,1) $.
Therefore, we must take

$$ \frac{0.02\sqrt{n}}{\sqrt{1/12}}\geq 1.96 \Rightarrow n>800.33 $$

