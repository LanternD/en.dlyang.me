---
layout: post
title: Globally Change Footprint Reference Visibility in KiCad
description: In PCB design, we may encounter the case where we would like to hide the reference text in the silk layer for better visualization. Here is a short post showing how to make it.
permalink: /globally-change-footprint-reference-visibility-in-kiCad/
categories: [blog]
tags: [KiCad, PCB, CAD, design]
date: 2019-10-07 11:04:49
---

# A Link

Here is a link in the KiCad forum, discussing how to globally edit the text in the PCB.

<https://forum.kicad.info/t/globally-edit-reference-designator-text/488>

Then I managed to change all the footprint reference to invisible, rendering the PCB looks clean and elegant.

# Walk Through

Before changing, the reference symbol looks like:

![img](../assets/post-img/globally-change-footprint-reference-visibility-in-kiCad/before.png "Before")

Step 1. Open 'Edit' -> 'Edit Text & Graphic Properties&#x2026;'

![img](../assets/post-img/globally-change-footprint-reference-visibility-in-kiCad/window.png "Edit window")

Step 2. Select 'Footprint references' on the top left panel; check the filter as 'F.silks'; Specify the footprint you want to change in 'Filter items by parent footprint reference', e.g. 'R\*', 'C\*'.

![img](../assets/post-img/globally-change-footprint-reference-visibility-in-kiCad/edit.png "Edit window 2")

Step 3. [The most important one] **Uncheck the 'Visible'** in the 'Action' panel.

Step 4. Done. Here is how it looks after editing:

![img](../assets/post-img/globally-change-footprint-reference-visibility-in-kiCad/after.png "After")

# End

By the way, my KiCad version is 5.99.0 (Nightly build, installed in Aug 2019.
