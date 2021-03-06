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
	
- A 50-$\Omega$ microstrip line for a substrate height of 128 $\mu$m and $\varepsilon_r$ of 3 (RT Duroid)

- A 50-$\Omega$ microstrip line for a substrate height of 10 $\mu$m and $\varepsilon_r$ of 4.1 (CMOS)

- A 50-$\Omega$ microstrip line for a substrate height of 5 $\mu$m and $\varepsilon_r$ of 4.1 (CMOS)

- For the CMOS case, assuming the minimum allowable line width and spacing  is 2 $\mu$m on the top metal, what is the highest characteristic impedance we can achieve?
	
- What is the lowest characteristic impedance we can achieve? What would be the limiting factor?


# Solution
		
## Problem 1

For RT Duroid material, use the $w/h1$ formula to recalculate. i.e.
		
$$Z_0=\frac{120\pi}{\sqrt{\varepsilon_{\rm eff}}\big[\frac{w}{128}+1.393+0.667\ln(\frac{w}{128}+1.44)\big]}$$
		
This time I substitute the $w=400 \rm{\mu m}$ (another assumption) in the $\varepsilon_{\rm eff}$ formula. I choose this value to get rid of the recursive calculation to find the exact value of $w$.

$$\begin{eqnarray}
	\varepsilon_{\rm eff} &\approx& \frac{\varepsilon_r+1}{2}+\frac{\varepsilon_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big] \\
	&=& \frac{3+1}{2}+\frac{3-1}{2}[\frac{1}{\sqrt{1+12\times128/400}}] =2.4545
\end{eqnarray}$$
		
Denote $C = \frac{120\pi}{Z_0\sqrt{\varepsilon_{\rm eff}}}-1.393$, we obtain

$$\begin{eqnarray}
	f(w) &=& \frac{w}{128}+0.667\ln(\frac{w}{128}+1.44)-C=0 \\
	\implies f(x) &=& x+0.667\ln(x+1.44)-C \\
	f'(x) &=& 1+\frac{0.667}{x+1.44}-C
\end{eqnarray}$$
		
Use Newton-Raphson method to find the value $w$.
		
$$x_{i+1}=x_{i}-\frac{f(x_i)}{f'(x_i)}$$
		
and finally $\frac{w}{128}=2.9520$, thus $w=2.9520\times 128=320.5948 \rm{~\mu m}$. 
		
## Problem 2

When it comes to CMOS cases, the substrate height $h$ is usually very small, but I also assume $w/h>1$. Take $w=15 {~\mu m}$ to calculate the efficient $\varepsilon$.

$$\begin{eqnarray}
	\varepsilon_{\rm eff} &\approx& \frac{\varepsilon_r+1}{2}+\frac{\varepsilon_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big] \\
	&=& \frac{4.1+1}{2}+\frac{4.1-1}{2}[\frac{1}{\sqrt{1+12\times10/15}}]=3.0667
\end{eqnarray}$$
		
Go through the similar process above, it is not hard to calculate that $C_1=2.9125$, and $\frac{w}{h}=2.0746$, which returns $w_1=20.7459 \rm{~\mu m}$. This result is close to the value we used to calculate $\varepsilon_{\rm eff}$, so there is no need to redesign again.
		
## Problem 3

For the CMOS case with substrate height $h=5 \rm{~\mu m}$, similarly first calculate the efficient $\varepsilon_{\rm eff}$.

$$\begin{eqnarray}
	\varepsilon_{\rm eff} &\approx& \frac{\varepsilon_r+1}{2}+\frac{\varepsilon_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big] \\
	&=& \frac{4.1+1}{2}+\frac{4.1-1}{2}[\frac{1}{\sqrt{1+12\times5/8}}]=3.0816
\end{eqnarray}$$
		
And $C_2=2.9021$, $\frac{w}{h}=2.0658\implies w = 10.3289\rm{~\mu m}$.
		
## Problem 4

$Z_0$ increases with $h$ and decreases with $w$ and $\varepsilon_r$. When the minimum allowable $w_{\min}=2\rm{~\mu m}$,

$$\begin{eqnarray}
	\varepsilon_{\rm eff} &\approx& \frac{\varepsilon_r+1}{2}+\frac{\varepsilon_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big] \\
	&=& \frac{4.1+1}{2}+\frac{4.1-1}{2}[\frac{1}{\sqrt{1+12\times\frac{1}{2}}}]=2.980
\end{eqnarray}$$
	
When $h=10\rm{~\mu m}$,

$$\begin{eqnarray}
	Z_{0,\max} &=& \frac{120\pi}{\sqrt{\varepsilon_{\rm eff}}\big[\frac{w}{h}+1.393+0.667\ln(\frac{w}{h}+1.44)\big]} \\
	&=& \frac{120\pi}{\sqrt{2.98}\big[\frac{2}{10}+1.393+0.667\ln(\frac{2}{10}+1.44)\big]} \\
	&=& 113.5691~\Omega.
\end{eqnarray}$$
	
When $h=5\rm{~\mu m}$,
	

$$ Z_{0,\max}=\frac{120\pi}{\sqrt{2.98}\big[\frac{2}{5}+1.393+0.667\ln(\frac{2}{5}+1.44)\big]}=96.7805~\Omega$$
	
That is the highest characteristic impedance we can achieve with the CMOS.
	
## Problem 5

As demonstrated above, $Z_0$ increases with $h$ and decreases with $w$ and $\varepsilon_r$. We need to lower the substrate height $h$ and increase microstrip width $w$ and $\varepsilon_r$. Let's choose a substrate material, say GaAs, and $\varepsilon_r=12.7$. 

$$\begin{eqnarray}
	\varepsilon_{\rm eff} &\approx& \frac{\varepsilon_r+1}{2}+\frac{\varepsilon_r-1}{2}\Big[\frac{1}{\sqrt{1+12h/w}}\Big] \\
	&=& \frac{12.7+1}{2}+\frac{12.7-1}{2}[\frac{1}{\sqrt{1+12\times\frac{1}{2}}}]=9.0611
\end{eqnarray}$$
	
More detailedly, it is the ratio $w/h$ that matters. For here, I choose $w/h=2$.
	
$$Z_{0,\max}=\frac{120\pi}{\sqrt{9.0611}\big[\frac{2}{1}+1.393+0.667\ln(\frac{2}{1}+1.44)\big]}=29.6983~\Omega$$
	
Further, if I increase the ratio to $w/h=5$, we can calculate that $Z_0=16.4027~\Omega$. This is lower than the previous case. 
	
I don't know whether there is a theoretical limitation for the $w/h$ ratio, but in practical application when $w$ is too high, there will be less space for other components. Also, a rule of thumb is that we need to limit the thickness of the microstrip substrate to 10% of a wavelength.
	
# Simulation result

lineCalc result in ADS (Advanced Design System, a keysight software):

(Follow the instruction in [this video](https://youtu.be/Oz1qsJD64Cs?list=PLxFNoL2xzVKZtJBYXeERgkMTfC8W-4HQ3).)

- $w_1 = 305.872 \mu\rm{m}$

- $w_2 = 18.5694 \mu\rm{m}$

- $w_3 = 8.71934 \mu\rm{m}$