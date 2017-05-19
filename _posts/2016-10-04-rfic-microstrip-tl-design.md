---
layout: post
title: RFIC - Microstrip Transmission Line Design
description: Microstrip transmission line is one of the basic type of transmission line in RF integrated circuit. Here is a basic/simple design example of it. This is a homework for course ECE810 RF Integrated Circuits in MSU.
permalink: /rfic-microstrip-tl-design/
categories: [blog]
tags: [course, microstip, design, problem, solution]
date: 2016-10-04 16:35:32
---


# To begin with

Microstrip is one kind of transmission line in the circuit. We use them to achieve impedance matching or some other application. Here are some simple design examples.

# Problems

Design following transmission lines (use simplifying assumptions):
	
- A 50-$\Omega$ microstrip line for a substrate height of 128 $\mu$m and $\varepsilon\_r$ of 3 (RT Duroid)

- A 50-$\Omega$ microstrip line for a substrate height of 10 $\mu$m and $\varepsilon\_r$ of 4.1 (CMOS)

- A 50-$\Omega$ microstrip line for a substrate height of 5 $\mu$m and $\varepsilon\_r$ of 4.1 (CMOS)

- For the CMOS case, assuming the minimum allowable line width and spacing  is 2 $\mu$m on the top metal, what is the highest characteristic impedance we can achieve?
	
- What is the lowest characteristic impedance we can achieve? What would be the limiting factor?

[[MORE]]

# Solution
		
## Problem 1

For RT Duroid material, use the $w/h1$ formula to recalculate. i.e.
		
$$Z\_0=\frac{120\pi}{\sqrt{\varepsilon\_{eff}}\big[\frac{w}{128}+1.393+0.667\ln(\frac{w}{128}+1.44)\big]}$$
		
This time I substitute the $w=400 \rm{\mu m}$ (another assumption) in the $\varepsilon\_{eff}$ formula. I choose this value to get rid of the recursive calculation to find the exact value of $w$.
		
$$\varepsilon\_{eff}\approx\frac{\varepsilon\_r+1}{2}+\frac{\varepsilon\_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big]=\frac{3+1}{2}+\frac{3-1}{2}[\frac{1}{\sqrt{1+12\times128/400}}]=2.4545$$
		
Denote $C = \frac{120\pi}{Z\_0\sqrt{\varepsilon\_{eff}}}-1.393$, we obtain
		
$$f(w)=\frac{w}{128}+0.667\ln(\frac{w}{128}+1.44)-C=0$$
		
$$\implies f(x) = x+0.667\ln(x+1.44)-C$$
		
$$f'(x)=1+\frac{0.667}{x+1.44}-C$$
		
Use Newton-Raphson method to find the value $w$.
		
$$x\_{i+1}=x\_{i}-\frac{f(x\_i)}{f'(x\_i)}$$
		
and finally $\frac{w}{128}=2.9520$, thus $w=2.9520\times 128=320.5948 \rm{~\mu m}$. 
		
## Problem 2

When it comes to CMOS cases, the substrate height $h$ is usually very small, but I also assume $w/h>1$. Take $w=15 {~\mu m}$ to calculate the efficient $\varepsilon$.
		
$$\varepsilon\_{eff}\approx\frac{\varepsilon\_r+1}{2}+\frac{\varepsilon\_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big]=\frac{4.1+1}{2}+\frac{4.1-1}{2}[\frac{1}{\sqrt{1+12\times10/15}}]=3.0667$$
		
Go through the similar process above, it is not hard to calculate that $C\_1=2.9125$, and $\frac{w}{h}=2.0746$, which returns $w\_1=20.7459 \rm{~\mu m}$. This result is close to the value we used to calculate $\varepsilon\_{eff}$, so there is no need to redesign again.
		
## Problem 3

For the CMOS case with substrate height $h=5 \rm{~\mu m}$, similarly first calculate the efficient $\varepsilon\_{eff}$.
		
$$\varepsilon\_{eff}\approx\frac{\varepsilon\_r+1}{2}+\frac{\varepsilon\_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big]=\frac{4.1+1}{2}+\frac{4.1-1}{2}[\frac{1}{\sqrt{1+12\times5/8}}]=3.0816$$
		
And $C\_2=2.9021$, $\frac{w}{h}=2.0658\implies w = 10.3289\rm{~\mu m}$.
		
	
## Problem 4

$Z\_0$ increases with $h$ and decreases with $w$ and $\varepsilon\_r$. When the minimum allowable $w\_{\min}=2\rm{~\mu m}$,
	
$$\varepsilon\_{eff}\approx\frac{\varepsilon\_r+1}{2}+\frac{\varepsilon\_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big]=\frac{4.1+1}{2}+\frac{4.1-1}{2}[\frac{1}{\sqrt{1+12\times\frac{1}{2}}}]=2.980$$ 
	
When $h=10\rm{~\mu m}$,


$$ Z\_{0,\max}=\frac{120\pi}{\sqrt{\varepsilon\_{eff}}\big[\frac{w}{h}+1.393+0.667\ln(\frac{w}{h}+1.44)\big]}$$
$$=\frac{120\pi}{\sqrt{2.98}\big[\frac{2}{10}+1.393+0.667\ln(\frac{2}{10}+1.44)\big]}$$
$$=113.5691~\Omega$$

	
When $h=5\rm{~\mu m}$,
	

$$ Z\_{0,\max}=\frac{120\pi}{\sqrt{2.98}\big[\frac{2}{5}+1.393+0.667\ln(\frac{2}{5}+1.44)\big]}$$
$$=96.7805~\Omega$$
	
That is the highest characteristic impedance we can achieve with the CMOS.
	
## Problem 5

As demonstrated above, $Z\_0$ increases with $h$ and decreases with $w$ and $\varepsilon\_r$. We need to lower the substrate height $h$ and increase microstrip width $w$ and $\varepsilon_r$. Let's choose a substrate material, say GaAs, and $\varepsilon_r=12.7$. 
	
$$\varepsilon\_{eff}\approx\frac{\varepsilon\_r+1}{2}+\frac{\varepsilon\_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big]=\frac{12.7+1}{2}+\frac{12.7-1}{2}[\frac{1}{\sqrt{1+12\times\frac{1}{2}}}]=9.0611$$
	
More detailedly, it is the ratio $w/h$ that matters. For here, I choose $w/h=2$.
	
$$Z\_{0,\max}=\frac{120\pi}{\sqrt{9.0611}\big[\frac{2}{1}+1.393+0.667\ln(\frac{2}{1}+1.44)\big]}$$
$$=29.6983~\Omega$$
	
Further, if I increase the ratio to $w/h=5$, we can calculate that $Z\_0=16.4027~\Omega$. This is lower than the previous case. 
	
I don't know whether there is a theoretical limitation for the $w/h$ ratio, but in practical application when $w$ is too high, there will be less space for other components. Also, a rule of thumb is that we need to limit the thickness of the microstrip substrate to 10\% of a wavelength.
	
# Simulation result

lineCalc result in ADS (Advanced Design System, a keysight software):

(Follow the instruction in [this video](https://youtu.be/Oz1qsJD64Cs?list=PLxFNoL2xzVKZtJBYXeERgkMTfC8W-4HQ3).)

- $w_1 = 305.872 \mu\rm{m}$

- $w_2 = 18.5694 \mu\rm{m}$

- $w_3 = 8.71934 \mu\rm{m}$