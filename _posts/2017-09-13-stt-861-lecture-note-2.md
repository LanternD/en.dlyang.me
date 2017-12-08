---
layout: post
title: STT 861 Theory of Prob and STT I Lecture Note - 2
description: Some of the basic probability and statistics concepts. joint probabilities, combinatories; conditional probabilities and independence and their examples; Bayes' rule.
permalink: /stt-861-lecture-note-2/
categories: [blog]
tags: [course, probability, statistics, lecture, note, MSU]
date: 2017-09-13 16:35:32
---

# Portal to all the other notes

- [Lecture 01 - 2017.09.06](/stt-861-lecture-note-1/) 
- [Lecture 02 - 2017.09.13](/stt-861-lecture-note-2/) -> This post
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
- [Lecture 14 - 2017.12.06](/stt-861-lecture-note-14/)

# Lecture 02 - Sept 13 2017

Recall: If A & B are 2 disjoint events, then $P[A\cup B]=P[A]+P[B]$, $P[A\cap B]=P[A]\cdot P[B]$.

If $A\cup B \neq \varnothing$, then $P[A\cap B]=P[A]\cdot P[B] - P[A\cap B]$.

General formula ("inclusion-exclusion formula")

$$P[A_1\cup A_2\cup ... \cup A_n] = \sum_{\emptyset\neq J\subseteq\{1,2,...,n\}}(-1)^{|J|-1}\bigcap_{j\in J}A_j$$

### Example 1

Weather data for 2 consecutive days in some month in some location. We aggregate this data and find: 'R1 is rain on 1st day', 'R2 is rain on 2nd day'. $P[R1]=0.6, P[R2]=0.5, P[R1\cap R2^C]=0.2$. Find $P[R1\cap R2]$ and $P[R1\cup R2]$.

Answer:

$P[(R1\cap R2^C)\cup(R1\cap R2)]=P[R1]$.

$P[R1\cap R2^C]+P[R1\cap R2]=P[R1] \rightarrow P[R1\cap R2]=0.4$

$P[R1\cup R2] = P[R1] + P[R2] - P[R1\cap R2]=0.6+0.5-0.4 = 0.7$

### Example to introduce the use of some combinatories

Form a jury with 6 people. We choose from a group with 8 men & 7 women. Find the prob that there are exactly 2 women in the selected jury.

Need an assumption about the relative prob. of people being picked: 6/15. Every one has equal chance of being picked.
 
P=({\# of ways to pick exactly 2 women})/({\# of ways to pick 6 out of 15})

$(C_7^2 \times C_8^4)/C_{15}^6 $

(tree idea)

$$\left(
\begin{array}{c}
N \\
n
\end{array}
\right) = \frac{N!}{n!(N-n)!}$$

$C_{15}^6 = 5005$

numerator$ = 21 \times 70 = 1470$

$P = 1470/5005=0.2937$

------

After the break.

## Chapter 1.3 Conditional prob. & independence

**Definition**: A & B are independence events, if $P[A\cap B] = P[A] \times P[B]$.

The definition comes from the definition of conditional prob.

**Definition**: Let A & B be two events. The conditional prob of B given A denoted by $P[B\|A]$, is $P[A \cap B]/P[A]$.

Note: if $P[B\|A] = P[B]$ (given information of A does not affect/influence the chance of B), then the definition is proven.

### Example 2

$P[disease]= 0.006$. Test: positive vs negative. $P[positive\|dissease] = 0.98$ (sensitivity). $P[pos\|no disease]=0.01$.

Q1: Find prob P[pos].

$P[pos] = P[pos \cap disease] + P[neg \cap no disease]$

$P[pos\|disease] = P[pos \cap disease]/P[disease] $

$P[pos \cap disease] = 0.98\times0.006$

similarly, $P[neg \cap no~disease] = (1- 0.99)\times(1-0.006)$

$P[pos] = 0.98\times0.006 + (1- 0.99)\times(1-0.006) = 1.582\%$

Q2: Find $P[dis\|pos]$.

$P[dis\|pos] = P[dis \cap pos]/P[pos] = 0.00588/0.01582 = 0.3717$

The law of total probabilities:

Let $A_1, A_2, ..., A_n$ be a partition of $\Omega$. ($A_i$ are all mutually incompatible, and $\sum A_i=\Omega$)

then for any $B\in\Omega$, $P[B]=\sum_i P[B\|A_i]P[A_i]$.

Try to prove it at home.

### Bayes' rule

$$P[A|B]=\frac{P[A\cap B]}{P[B|A]P[A]+P[B|A^C]P[A^C]}=P[B|A]\times P[A]/P[B]$$

denominator: from law of total prob when n=2, $A_1=A,A_2=A^C$

#### General Bayes' Rule:

For every fixed $i$:

$$P[A_i|B]=\frac{P[B|A_i]P[A_i]}{\sum_{j=1}^n P[B|A_j]P[A_j]}$$

Role of different pieces of information in the formula:

- $P[A\|B]$: B has happend, the prob of A.
- $P[A]$ and $P[A^C]$: "The prori" a priori info about the events you are interested in, regard of the observation.
- $P[B\|A]$ and $P[B\|A^C]$: "Likelihood" likelihoods that eventsthat you observe B actually happen given the events of interest to you.

At home, relate disease example problem to Bayes' rule.
