---
layout: post
title: Embed Texts in Other Files in reStructuredText
description: Include the texts in other files to generate a new files.
permalink: /embed-texts-in-other-files-in-restructuredtext/
categories: [blog]
tags: [reST, embedding, markup]
date: 2021-01-11 00:27:57
---

# Basic

[reStructuredText](https://docutils.sourceforge.io/rst.html), shortened as reST, is a markup language, with complexity between Markdown and LaTeX, somewhat similar to [org-mode](https://orgmode.org/).

Recently I learn reST and use it in documenting my side project.

reST is an extension of [`docutils`](https://docutils.sourceforge.io/index.html), and reST nowadays usually works together with [sphinx-doc](https://www.sphinx-doc.org/en/master/index.html). All of them are powered by Python.

# Goal

My goal is to manage a list of items in separate files, but I need a file to generate a completed list of items from those subfiles.

Suppose I have:

-   `vege.txt`

```rst
Vegetables
==========

- Carrot
- Cabbage
- Lettuce
- Tomato
```

-   `fruits.txt`

```rst
Fruits
==========

- Apple
- Peach
- Pear
- Strawberry
```

-   `dairy.txt`

```rst
Dairy
==========

- Milk
- Cream
- Butter
- Cheese
```

I would like to generate a file `items_in_fridge.txt` (automatically), listing all the items above.

```rst
Items in Refrigerator
==========

Vegetables
------

- Carrot
- Cabbage
- Lettuce
- Tomato

Fruits
------

- Apple
- Peach
- Pear
- Strawberry

Dairy
----------

- Milk
- Cream
- Butter
- Cheese
```

# How

We can use the "[include](https://docutils.sourceforge.io/docs/ref/rst/directives.html#including-an-external-document-fragment)" directive. "Directive" can be consider as "command".

In this example, the files should be modified as following:

-   `vege.txt`

```rst
Vegetables
==========

.. start_mark

- Carrot
- Cabbage
- Lettuce
- Tomato

.. end_mark
```

-   `fruits.txt`

```rst
Fruits
==========

.. start_mark

- Apple
- Peach
- Pear
- Strawberry

.. end_mark
```

-   `dairy.txt`

```rst
Dairy
==========

.. start_mark

- Milk
- Cream
- Butter
- Cheese

.. end_mark
```

-   `items_in_fridge.txt` (Here we go)

```rst
Items in Refrigerator
==========

Vegetables
------

.. include:: vege.txt
    :start-after: .. start_mark
    :end-before: .. end_mark

Fruits
------

.. include:: fruits.txt
    :start-after: .. start_mark
    :end-before: .. end_mark

Dairy
----------

.. include:: dairy.txt
    :start-after: .. start_mark
    :end-before: .. end_mark
```

In this case, we just need to modify the items in the subfiles (`vege.txt`, `fruits.txt`, and `dairy.txt` in this case). Then the `items_in_fridge.txt` will include them automatically.

I use the mark `.. start_mark` (comment syntax in reST) to avoid displaying any text in the original documents. You can replace them with something else.

# Read More

-   [Reusing text in RST for Sphinx Documentation - StackOverflow](https://stackoverflow.com/questions/41930823/reusing-text-in-rst-for-sphinx-documentation)
-   [Including an External Document Fragment - Docutils](https://docutils.sourceforge.io/docs/ref/rst/directives.html#including-an-external-document-fragment)
