---
layout: post
title:  "Flood Fill Algorithm"
categories: [ blog, algorithm ]
featured-img: algorithm
---

Just want to make a note on the well-known **flood fill** algorithm.

**Recursive Implementation**
{% highlight python linenos %}
Flood-fill (node, target-color, replacement-color):
  If target-color is equal to replacement-color, return.
  If the color of node is not equal to target-color, return.
  Set the color of node to replacement-color.
  Perform Flood-fill (one step to the south of node, target-color, replacement-color).
  Perform Flood-fill (one step to the north of node, target-color, replacement-color).
  Perform Flood-fill (one step to the west of node, target-color, replacement-color).
  Perform Flood-fill (one step to the east of node, target-color, replacement-color).
  Return.
{% endhighlight %}

**Iterative Implementation**
{% highlight python linenos %}
Flood-fill (node, target-color, replacement-color):
  If target-color is equal to replacement-color, return.
  If color of node is not equal to target-color, return.
  Set Q to the empty queue.
  Set the color of node to replacement-color.
  Add node to the end of Q.
  While Q is not empty:
    Set n equal to the first element of Q.
    Remove first element from Q.
    If the color of the node to the west of n is target-color,
    set the color of that node to replacement-color and add that node to the end of Q.
    If the color of the node to the east of n is target-color,
           set the color of that node to replacement-color and add that node to the end of Q.
    If the color of the node to the north of n is target-color,
           set the color of that node to replacement-color and add that node to the end of Q.
    If the color of the node to the south of n is target-color,
           set the color of that node to replacement-color and add that node to the end of Q.
  Continue looping until Q is exhausted.
  Return.
{% endhighlight %}

I think this is interesting not just because this is classic but my personal [Go](https://github.com/zonggen/gomoku) game project should have included this method to check for the cleared pieces. Plus, when we are doing an **in-order tree walk** in a BST, we used similar technique (both *recursive* and *iterative* solution).
