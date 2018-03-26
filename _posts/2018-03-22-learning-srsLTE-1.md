---
layout: post
title: Learning srsLTE - 1
description: Overview.
permalink: /learning-srslte-1/
categories: [blog]
tags: [srslte, software radio, software]
date: 2018-03-22 10:34:56
---

# 　

## Introduction

srsLTE is an open-source library that control the RF front-end to build a software radio LTE system, including eNodeB, UE (user equipment) and the EPC (Evolved Packet Core).

There are so many API provided by srsLTE library. One can find an API document of srsLTE provided by the well-known [ShareTechNote](http://www.sharetechnote.com/) website, including

-   [API description](http://www.sharetechnote.com/html/SDR_srsLTE_Api.html)
-   [Data structure description](http://www.sharetechnote.com/html/SDR_srsLTE_Api_TypeDef.html)

Though the website is comprehensive and detailed, I think the web page was not well-rendered, especially the code. Using sans-serif non-monospaced fonts for the code is not a good practice, isn't it? By the way, the data structure page does not have anchor links to navigate.

In this document, I will give a reference to the structure type definition. I'll leave the API functions to the future posts.

## How to start

Plan:

Post 2, 3, 4 are the references to the data structures defined in the srsLTE header files.

Later posts will be the basic exploration of the srsLTE library.
