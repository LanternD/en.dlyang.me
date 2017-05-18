---
layout: post
title: Try MathJax Here
description: MathJax is a commonly-used web-based math formula and expression render tool. Here is the test of it.
permalink: /try-mathjax/
categories: [blog]
tags: [academic, mathjax, configuration, start]
date: 2016-09-06 16:35:32
---

<!-- <script type="text/x-mathjax-config">MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}});</script>
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script> -->


That comes to my mind that I may use my English blog for some academic writting.

It would be better that those complicated mathematics equations and formula can be clearly displayed on the screen. Of cause the first thing came across my mind is MathJax, the one I use in my Chinese blog (not too often though). 

The solution I followed is to add the MathJax CDN files in the header part of my HTML code, which could be found in the Theme Edit dashboard. For more info, please visit this [StackExchange](http://webapps.stackexchange.com/questions/11904/adding-mathjax-to-tumblr) pages, from which I found the solution.

So here's my try!

$$E=mc^2$$

Isn't that cool?!

Now the next part is inline math expressions. The second parameters estimation algorithm that I learned today on my Adaptive Control course is using the Least-Squre methods, given as defining a cost function like $J(\theta(t))=\frac{1}{2}\int_{0}^{t}\|\theta^T(t)\phi(\tau)-y(\tau)\|^2d\tau$. Then we take the partial derivative of the formula and set it to 0, then find the corresponding solution $\theta(t)$ as our parameter estimation of the time $t$. In other words, solve the equation $\frac{\partial J(\theta)}{\partial \theta} = 0$.

Something longer:

$$\begin{array}{c}

\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} &
= \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\

\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\

\nabla \cdot \vec{\mathbf{B}} & = 0

\end{array}$$

Kind of ugly style though.

Yep. It works. Now this marks the REAL start of my academic blog!

Go Green.