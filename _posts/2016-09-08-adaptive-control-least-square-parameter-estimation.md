---
layout: post
title: Adaptive Control - Least-Squares Algorithm in Parameters Estimation
description: Parameter estimation is one of the keystones in Adaptive control; the main idea of parameter estimation is to construct a parametric model and then use optimization methods to minimize the error between the true parameter and the estimation. Least-square algorithm is one of the common optimization methods.
permalink: /adaptive-control-least-square-parameter-estimation/
categories: [blog]
tags: [course, adaptive control, parameter, estimation, math, least square, optimization]
date: 2016-09-08 16:35:32
---

# Background

I take adaptive control course this semester, and in the homework after the second lecture, we are going to derive the formular for the estimated parameter vector $\theta(t)$ at time $t$.

Some terms we need to demonstrate the problem:

- Parametric model (linear): $y(t)=\theta^{*T}\phi(t)$.
- $\theta^\*$ is the truth value of the parameters in the system, which is what we want to reach or approach. However we only have the knowledge of $y(t)$ and $\theta(t)$. So we are going to estimate $\theta^\*$ based on what are known.
- $y(t)$ is the output of the system, $1\times1$ scaler, which could be measured and it is known.
- $\phi(t)$ is the input or reference of the system, which is also known.
- $\theta(t)$ is the estimated system parameter at time $t$, which is what we want.
- Cost function $J(\theta(t))$ is what we would like to minimized, so that the error between $\theta\phi$ and $y$ is minimized.

There are two algorithms that can solve this problem. The first one is Gradient (Descent) Algorithm, another one is what we are going to say here, Least-squares algorithm. Basically, the differences between these two algorithms are the cost function they employed and the method to minimize the cost function.

[[MORE]]

# Problem

So here is our setting:

Given the cost function in Least-Squares algorithm,
	
$$ J(\theta(t)) = \frac{1}{2} \int_0^t |\theta^T(t)\phi(\tau)-y(\tau)|^2 d\tau $$
	
Take the partial derivative of $J(\theta(t))$, let it be 0, solve the equation 
	
$$\frac{\partial J(\theta)}{\partial \theta} = 0$$
	
and derive that 
	
$$\theta(t) = [\int\_0^t \phi(\tau)\phi^T(\tau)d\tau]^{-1}\int_0^t y(\tau)\phi(\tau)d\tau$$
	
# Solution


$$\frac{\partial J(\theta)}{\partial \theta} = \frac{1}{2}\frac{\partial}{\partial \theta}\Big\\{\int\_0^t \big[[\theta^T(t)\phi(\tau)]^2-2\theta^T(t)\phi(\tau)y(\tau)-y^2(\tau)\big]d\tau\Big\\}$$
$$= \frac{1}{2}\int\_0^t\frac{\partial}{\partial \theta}[\theta^T(t)\phi(\tau)]^2d\tau-\frac{1}{2}\int\_0^t\frac{\partial}{\partial \theta}[2\theta^T(t)\phi(\tau)y(\tau)]d\tau $$
$$= \int\_0^t\theta^T(t)\phi(\tau)\frac{\partial}{\partial \theta}[\theta^T(t)\phi(\tau)]d\tau - \int_0^t y(\tau)\phi(\tau)d\tau $$
$$= \int\_0^t\theta^T(t)\phi(\tau)\phi^T(\tau)d\tau - \int_0^t y(\tau)\phi(\tau)d\tau=0 $$


Therefore,

$$ \theta^T(t)[\int\_0^t \phi(\tau)\phi^T(\tau)d\tau] = \int\_0^t y(\tau)\phi(\tau)d\tau $$

$$ [\int\_0^t \phi(\tau)\phi^T(\tau)d\tau]\theta(t) = \int\_0^t y(\tau)\phi(\tau)d\tau $$

Finally,

$$ \theta(t) = [\int\_0^t \phi(\tau)\phi^T(\tau)d\tau]^{-1}\int_0^t y(\tau)\phi(\tau)d\tau $$


(The right hand side is a column vector, so when taking $\theta^T(t)$ out of the integral, it should transpose to become a column vector. And $\phi(\tau)\phi^T(\tau)=[\phi(\tau)\phi^T(\tau)]^T$, because it is a symmetric matrix.)

# Revision and Updates

Since the solution above required $\int\_0^t \phi(\tau)\phi^T(\tau)d\tau$ to be invertible, in some scenario where t is very small, usually the matrix is not full ranked and is not invertible. To deal with this situation, we revise the cost function as 

$$J(\theta(t)) = \frac{1}{2} \int\_0^t|\theta^T(t)\phi(\tau)-y(\tau)|^2d\tau+\frac{1}{2}[\theta(t)-\theta\_0]^TQ\_0[\theta(t)-\theta\_0]$$

where $\theta\_0=\theta(0)$ is the initial estimation of parameters, and $Q\_0=Q\_0^T$ is a symmetric and positive definite matrix.

We can do the same process like the solution above, and we achieve:

$$\theta(t) = [Q\_0+\int\_0^t\phi(\tau)\phi^T(\tau)d\tau]^{-1}[Q\_0\theta\_0+\int\_0^t y(\tau)\phi(\tau)d\tau]$$

(Notice that: $\frac{\partial x^TAx}{\partial x}=(Ax)^T+x^TA=x^TA^T+x^TA$, where $x$ and $A$ are matrices, $A$ is not a function of $x$.If A is a symmetric matrix, $A^T=A$, then the result would be $2x^TA$ or $2x^T A^T$.)

Positive definite matrix is always invertible, so this formula can suit for more situations. 

# Matrix Formula

- If $U$ and $V$ are vectors,

$$\frac{\partial V^TU}{\partial V}=U^T$$

- $[AB]^T=B^TA^T$