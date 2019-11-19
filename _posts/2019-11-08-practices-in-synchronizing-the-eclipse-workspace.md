---
layout: post
title: Practices in Synchronizing the Eclipse Workspace
description: The best practice not messing up things is create different folder for different computer.
permalink: /practices-in-synchronizing-the-eclipse-workspace/
categories: [blog]
tags: [Eclipse, workspace, sync]
date: 2019-11-08 20:29:22
---

# The Vision of Synchronization

I am really enthusiastic abotu synchronizing all of my configuration files via Dropbox thing to keep my working environment consistent. Yeah, why not? Every programmer has their ways to make it.

However, the problem I was trying to solve is that I could not get a consistent environment for Eclipse workspace.

# Workspace in Eclipse

Eclipse introduces the concept of `workspace` to store the layout, logs, opened files, project organization, and whatever metadata.

In the beginning, I thought I could create only one workspace, synchronize it with my Dropbox, and made sure everything is the same no matter which computer I used. But it turned out it failed. After I added a project on my Macbook and open several files for editing, I closed Eclipse and opened the Eclipse on the other computer (Ubuntu). Then the software was screwed. It could not open all the files that I had opened on my Mac.

The problem was, the workspace uses the absolute path for all the projects. For example, on Mac, the path would be

```sh
/Users/my_login/Dropbox/somewhere/project_names/
```

However, on my Ubuntu machine, the path was

```sh
/home/my_login/Dropbox/somewhere/project_names/
```

While on the Windows machine, there would be a partition indicator in the path, like

```sh
D:\Dropbox\somewhere\project_names\
```

Since different systems could not interpret the path on other systems. The Eclipse failed to load the correct path of the projects.

# Solved

The keypoint of solving this problem occurs when I realize that the projects are not necessarily placed in the same directory of the workspace. Then everything has its way out.

**I don't need to synchronize the workspace at all.**

I created three (which is the number of machines) folders to store the workspace folders, still synchronized via Dropbox, and then created different workspace for different machines. Then, I could import the same project from somewhere else on my Dropbox to the workspace.

This solution works very well so far.

The drawback is, your Eclipse is going to open the same files as your closed last time, so different machine will open different files, which may be a little bit inconsistent. However, everything else works just fine.

The best way to synchronize the Eclipse workspace is not to synchronize them. Maybe creating the workspace folder locally would be another option (not synchronize it via Dropbox).
