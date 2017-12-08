---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 12
description: Examples on continuous distirbution conditional on discrete distribution; bivariate normal distribution. Not much for today.
permalink: /stt-861-lecture-note-12/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-11-20 20:45:32
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
- [Lecture 12 - 2017.11.20](/stt-861-lecture-note-12/) -> This post
- [Lecture 13 - 2017.11.29](/stt-861-lecture-note-13/)
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/)

# Lecture 12 - Nov 20 2017

## Some notes

- Exponential distribution and geometry distribution are the only
  distributions which have the memoryless property (continuous and discrete).
- Geometry is not scalable. It only takes integer values.  $
  T=\frac{1}{60}Geom(p) $ is not a geometry distribution.

------

**Exercise**: see the textbook's treatment of discrete mixtures of continuous r.v.'s.

### Example 1

Let  $ X\sim Exp(\lambda) $ and  $ Y\sim Exp(\mu) $,  $
\varepsilon \sim Bernoulli(\frac{1}{2}) $. They are all independent.

let  $ Z=X $ if  $ \varepsilon=0 $ and  $ Z=-Y $ if  $ \varepsilon = 1 $. 

**Exercise**: See book on `continuous mixtures'.

### Example 2
$ X\sim Poisson(\lambda) $. Assume  $ \lambda $ itself is
random.  $ \lambda\sim \Gamma(m,\theta) $.

Easy to say, $ X $ is Poisson conditional on  $ \lambda $, but what is the
unconditional distribution of  $ X $?

Answer is in the book. We just want to compute  $ P(X=k)$ for  $
k=0,1,2,... $.

## Bivariate Normal

Let  $ X \sim N(\mu,\sigma^2)$. We know we can represent  $ X $ as  $
X=\mu+\sigma Z $ where  $ Z\sim N(0,1) $.

More generally, let  $ X_1, X_2 $ be bivariate normal. It turns out that we
can represent  $ X_2 $ using  $ X_1 $ and an independent component  $
\varepsilon_2 $ like this:

$$ X_2=a+bX_1+\varepsilon_2 $$

where  $ a \& b $ are constants.  $ \varepsilon_2 $ is a normal r.v.
independent of  $ X $ , with  $ E(\varepsilon_2) $. 

We would like to compute  $ a $ and  $ b $ and  $ Var(\varepsilon_2) $.
All we know is

$$ Var(X_1)=\sigma_1^2 $$

$$ Var(X_2)=\sigma_2^2 $$

$$ Corr(X,Y)=\rho $$

To simplify, assume  $ \sigma_1=\sigma_2 $, then we know, from linear
prediction, that  $ b=\rho $. Then for  $ Var(\varepsilon_2)$:

$$ \begin{align*}
  Var(X_2) & = 1= Var(bX_1) + Var(\varepsilon_2) \\
           &= Var(\varepsilon_2) = 1-\rho^2
\end{align*} $$

Also note: by taking expectation of the whole model,


$$ \mu_2=a+b\mu_1+0 $$

Therefore,  $ a=\mu_2-\rho\mu_2 $.

------

Going back to our work with densities for the multivariate normal. We find the
following density for the pair $ X=(X_1,X_2) $:

$$ f(x_1,x_2) = const\cdot \exp\big(-\frac{1}{2d}(x_1^2-2\rho x_1x_2 + x_2^2)\big) $$

where  $ d=1-\rho^2 $, and const  $ =\frac{1}{2\pi d} $. Notice that

$$
d=1-\rho^2=\det\begin{pmatrix}
1 & \rho \\
\rho & 1 
\end{pmatrix} $$

Also note: the expression

$$ Q(x)=Q(x_1,x_2) = (x_1^2-2\rho x_1x_2+x_2^2)/(2d) $$

is the ``quadratic form'', which we encountered as the term  $ 1/2
x^T[cov(X)]^{-1}x $. Go back and check this is true.

When  $ \rho=0 $, const $\frac{1}{2\pi}$.

$$ f(x_1,x_2) = \frac{1}{2\pi}\exp(-\frac{1}{2}(x_1^2+x_2^2)) = \frac{1}{2\pi} \exp({-\frac{1}{2}}x_1^2)\cdot \exp(-\frac{1}{2}x_2^2)  $$

This proves the independence ($\rho=0$). 
