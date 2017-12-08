---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 14
description: Proof of central limit theorem; multivariate normal distribution and its example; review of the second half of the semester, Poisson approximation vs. normal approximation to binomial distribution; miscellaneous notes of convergence.
permalink: /stt-861-lecture-note-14/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-12-06 20:45:32
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
- [Lecture 11 - 2017.11.15](/stt-861-lecture-note-11/)
- [Lecture 12 - 2017.11.20](/stt-861-lecture-note-12/)
- [Lecture 13 - 2017.11.29](/stt-861-lecture-note-13/)
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/) -> This post

# Lecture 14 - Dec 06 2017

## Proof of CLT (Central Limit Theorem)

This is the last lecture of this course.

Let $ X_i $ be $ n $ i.i.d distribution. $ \mu=E(X_i) $, $
\sigma^2=Var(X_i) $. WOLOG (without loss of generality), $ \mu=0 $, $ \sigma^2=1 $.

$$ S_n=\frac{\sum_{i=1}^{n}X_i}{\sqrt{n}} \rightarrow N(0,1)$$

  It is sufficient to show that MGF of $ S_n \rightarrow $ MGF of $
  Normal(0,1) $ for all $ t $ near 0.

$$\begin{align*}
  M_{S_n}(t)=E(e^{tS_n})&=E(\prod_{i=1}^{n}e^{t/\sqrt{n}\cdot X_i}) \\
                          &=\prod E(e^{t/\sqrt{n}X_i}) \\
                         &=(E(\exp(t/\sqrt{n}X_i)))^n \\
                           E(\exp(t/\sqrt{n}X_1))&\triangleq M_{X_1}(u)
\end{align*} $$

where $ u=t/\sqrt{n} $.

We will use the following fundamental property of MGF. 

$$ \frac{d}{du}M_X(0)=E(\frac{d}{du}e^{uX})|_{u=0}=E(X) $$

$$ \frac{d^2}{du^2}M_X(0)=E(X^2), \frac{d^p}{du^p}M_X(0)=E(X^p) $$

In our case: $ E(X_1)=0, E(X^2)=1 $.

Then expand $ M_X(u) $ using Taylor's formula.

$$ M_{X_1}(u)=M_{X_1}(0) + \frac{dM_X(0)}{du}u + \frac{1}{2}\frac{d^2M(0)}{du^2}+\cdots$$

(This is for $ u $ near 0. )

Therefore,

$$ M_{X_1}(u)=1+\frac{1}{2}u^2+O(u^3) $$

for small $ u $.

Next,

$$ M_{S_n}(t)=(1+\frac{1}{2}(\frac{t}{\sqrt{n}})^2+\varepsilon(u))^n $$

When $ n\rightarrow\infty $,

$$ M_{S_n}(t) \rightarrow \exp(\frac{1}{2}t^2) $$

which is the MGF of N(0,1).

Calculation of the MGF of $Normal(0,\sigma^2)$:

$$\begin{align*}
 M_Z(t) & = E(e^{tZ}) \\
        &= \int_{-\infty}^{\infty} \exp(zt) \frac{1}{\sqrt{2\pi\sigma^2}} \exp(-\frac{z^2}{2\sigma^2})dz \\
       &= \int_{-\infty}^{\infty} \frac{1}{\sqrt{2\pi\sigma^2}} \exp(-\frac{1}{2\sigma^2}(z^2-2\sigma^2tz+\sigma^4t^2-\sigma^4t^2))dz \\
       &= \int_{-\infty}^{\infty}\frac{1}{\sqrt{2\pi\sigma^2}} \exp(-\frac{1}{2\sigma^2}(z-2\sigma^2t)^2+\sigma^4t^2)) dz \\
       &= \exp(\frac{1}{2}\sigma^2t^2)
\end{align*}$$

(this part is in the homework 6.)

## Multivariate Normal

Quick review from a new example.

### Example 1

Let $X=(X_1,X_2,...,X_k) $ be a normal vector. Assume $ E(X_i)=\mu_i $ and $
Cov(X_i,X_j)=\Sigma_{ij} $. Find the MGF of the entire vector.

$$ M_X(t_1,...,t_k)=E(\exp (\sum_{i=1}^{k}t_iX_i)) $$

Let $ Y=t_iX_i $. Since $ X $ is multivariate normal, then $ Y $ is
normal. We just need to compute the expectation and variance of $ Y $.

$$\begin{align*}
  E(Y) & = \sum_{i=1}^{k} t_iE(X_i) = \sum_{i=1}^{k}t_i\mu_i \\
  Var(Y)&= \sum_{i=1}^{k}\sum_{j=1}^{k}Cov(t_iX_i,t_jX_j) \\
       &=\sum\sum t_it_j \Sigma_{ij} =\sigma^2\\
         M_t(X)&=E(e^Y)=E(e^{\mu+\sigma Z})
\end{align*}$$

where $ Z\sim N(0,1) $.

$$ M_t(X) = e^\mu E(e^{\sigma Z}) =M_Z(\sigma)e^\mu = e^{\mu+\frac{1}{2}\sigma^2}$$

We have proved that

$$ M_X(t) = e^{\mu+\frac{1}{2}\sigma^2} $$

where $ t=\sum_{i=1}^{k}\mu_it_i $, $ \sigma^2=t^T\Sigma t $. Finally, the
full form of MGF of $ Y $ is:

$$ M_X(t) = \exp(\sum_{i=1}^{k}\mu_it_i + \frac{1}{2}t^T\Sigma t) $$

We can identify what it means for multivariate normal vectors to be independent
of each other. 

$ X=((X^{(A)})(X^{(B)}))^T $ with length $ k=k_A+k_B $, then if $ X^{(A)} $
is independent of $ X^{(B)} $,

$$ \Sigma= \begin{pmatrix}
    \Sigma^{(A)} & 0\\
    0 & \Sigma^{(B)}
  \end{pmatrix}
$$

This also implies that if a normal vector has a block diagonal covariance
matrix, then the corresponding two subvectors are independent. 

### Really Important Example - Example 2

Let $ X=(X_1, X_2,...,X_k) $ be i.i.d $ N(\mu,\sigma^2) $. Let $
\bar{X}=\frac{1}{n}(X_1+X_2+\cdots+X_k )$ (empirical mean)

- what is the covariance $ Cov(\bar{X}, X_i) $?

Answer:

$$\begin{align*}
 Cov(\bar{X}, X_i) & =E\Big((\bar{X}-\mu)(X_i-\mu)\Big) \\
                   &=\frac{1}{n}E\Big(\big(\sum_{j=1}^{n}(X_j-\mu)\big)(X_i-\mu)\Big) \\
                   &=\frac{1}{n}\sum_{j=1}^{n}E\Big((X_j-\mu)(X_i-\mu)\Big)\\
                   &=\Sigma_{j\neq i} + \frac{\sigma^2}{n} = \frac{\sigma^2}{n}
\end{align*}$$

- Forget the above one. Next, what is $ Cov(\bar{X}, X_i-\bar{X}) $ (this is the actual important question)?

$$\begin{align*}
 Cov(\bar{X},X_i-\bar{X}) & = Cov(\bar{X}, X_i) -Cov(\bar{X}, \bar{X})\\
                         &= \frac{\sigma^2}{n} - \frac{\sigma^2}{n} = 0
\end{align*}$$

this proves that the bivariate $ (\bar{X}, X_i-\bar{X}) $ is bivariate normal
since the original $ X $ is multivariate normal and also $ \bar{X} $ and $
X_i-\bar{X} $ are independent because their covariance is 0.

- Next part of the example, let $ S^2= $ empirical variance $
=\frac{1}{n-1}\sum_{i=1}^{n}(X_i-\bar{X})^2 $. What's the relation between $
\bar{X} $ and $ S^2 $?

Since $ X_i-\bar{X} $ and $ \bar{X} $ are independent for fixed $ i $,
this is still true of $ (X_i-\bar{X})^2 $ and $ \bar{X} $.

Therefore, the entire vector $ Y=(X_i-\bar{X})^n_{i=1} $ is independent of $
\bar{X} $. In fact, any function of $ Y $ is independent of $ \bar{X} $. In
particular $ S^2 $ is independent of $ \bar{X} $.

Also,

$$ \frac{(n-1)S^2}{\sigma^2}=\sum_{i=1}^{n}(\frac{X_i-\bar{X}}{\sigma})^2 $$

This is all i.i.d.

This is Chi-Square distribution $ \chi^2(n-1) $. 

## Review of the Second Part of the Semester

When to use Poisson and when to use Normal to approximate a series of Bernoulli
trials?

### Poisson Approximation Case

$ X_i \sim Bernoulli(p) $ i.i.d. For example, $ X_i=1 $ vote for Dr. Jill
Stein (or Gary Johnson), $ X_i = 0$ otherwise. 

$ P=P(X_i=1] $ is small. What if $ p=\lambda n $ where $ n $ is the \# of
trials?

Then $ Y_n=X_1+X_2+\cdots + X_n, Y\sim Bin (n,p) $,

$$ E(Y_n) = np=\lambda $$

Since average \# of successes is constant $ \lambda $ then $ Bin(n,p)\approx
Poisson(\lambda $. Range $ 0.2 \leq \lambda \leq 10 $.

Note: $ Var(Y_n)=np(1-p) = \lambda(1-\frac{\lambda}{n}\approx\lambda $. If $
p=\frac{\lambda}{n}+O(\frac{1}{n}) $ then $ Bin(n,p) \approx Poisson(\lambda)
$ still holds.

### Normal Approximation Case

it works for Binomial and many other ``partial sums''
(like Negative Binomial).

In Binomial case, assume $ n\rightarrow \infty $ and
$ p $ is fixed. $ \lambda\neq np $ here, not constant.

Let $ Y=X_1+\cdots+X_n \sim Bin(n,p)$ 

$$ E(Y_n) = np\rightarrow\infty $$

$$ Var(Y_n)= np(1-p)\rightarrow\infty $$

Let

$$ Z_n=\frac{Y_n-np}{\sqrt{np(1-p)}} $$

then $ Z_n\rightarrow N(0,1) $, by CLT.

Note: Unlike Poisson approximation, CLT (Normal approximation) works for any $
X_i $ i.i.d as long as $ Var(X_i)=\sigma^2<\infty $. 

$ X_n\rightarrow X $ in distribution  $ \Leftrightarrow
F_{X_n}(x)\rightarrow F_X(x) $ for all $ x $

($ X_n $ is a sequence of random variables, $ X $ is a random variable)

Quick notes:

- If $ F $ is not continuous, the convergence does not need to hold for those $
x $'s where $ F $ is not continuous.
 
- If there exists $ \lambda $ such that $ F_{X_n}(x)\rightarrow 0 $ for all $
x\in \mathbb{R} $ then $ X_n $ does not converges in distribution, because
there is no r.v. $ X $ such that $ F_X(x)=0 $ all the time.

- Convergence in probability: $ X_n\rightarrow X $ in probability if $ X_n $
and $ X $ all live in the same probability space because we need to evaluate
$ X_n - X $. And we ask, for any $ \varepsilon>0 $ no matter how small.

- $ P(\vert X_n-X\vert> \varepsilon) $ is really small when $ n\rightarrow\infty $. 

- $ X_n\rightarrow X $ almost surely if $ P(\lim X_n=X) = 1$.


