---
layout: post
title: Fcitx Pinyin - Complete vs. Incomplete
description: I accidentally change the configuration in fcitx. Strange things happened. Now I fixed it.
permalink: /complete-incomplete-pinyin-in-fcitx/
categories: [blog]
tags: [pinyin, input method, linux, Fedora, fcitx]
date: 2019-03-22 04:36:52 
---

`fcitx` is a famous input method framework for Linux. Many languages use `fcitx` as the input methods backend. In my case, I use Pinyin input methods. There are three Pinyin input methods installed on my Fedora machine.

-   `Pinyin`
-   `sunpinyin`
-   `LibPinyin`

Today I accidentally changed the configuration of the `fcitx`, actually a bunch of settings all at once. After that I could not get the correct character candidates if I typed an acronym for a specific phase. I was to post an image of this case. But the screenshot failed to capture it (conflict with `fcitx`). I intended to type "cf" for "chifan", but not a single Chinese character came out.

I double checked. This only happened to `Pinyin` and `LibPinyin`, while `sunpinyin` works normally.

After debugging one by one, I identified the cause.

Just confirm that you choose "enable incomplete" Pinyin mode.

-   In `Pinyin`, **do not check** "Use Complete Pinyin".
-   In `LibPinyin`, **do check** "Use Incomplete pinyin".

That's it.

Configuration of `Pinyin`:

![img](../assets/post-img/complete-incomplete-pinyin-in-fcitx/pinyin-config.png "Pinyin Config")

Configuration of `LibPinyin`:

![img](../assets/post-img/complete-incomplete-pinyin-in-fcitx/libpinyin-config.png "LibPinyin Config")

Configuration of `sunpinyin` (You don't have this option here):

![img](../assets/post-img/complete-incomplete-pinyin-in-fcitx/sunpinyin-config.png "sunpinyin Config")
