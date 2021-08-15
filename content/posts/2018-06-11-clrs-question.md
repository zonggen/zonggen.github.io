---
layout: post
title:  "CLRS Question"
categories: [ clrs, algorithm ]
date: 2018-06-11
draft: false
comment: true
---

This weekend I have been working on the *CSC263* assignment. There was one question regarding augmenting data structure that was on the *CLRS* I found interesting:

> Consider **n** chords on a circle, each defined by its endpoints. Describe an **O(nlgn)** time algorithm to determine the number of pairs of chords that intersect inside the circle. (For example, if the n chords are all diameters that meet at the center, then the correct answer is **nC2**). Assume that no two chords share an endpoint.

My solution would be:

Insert *n* nodes to build an *AVL Tree* in *O(nlogn)* time, where each node has attribute: **key**, **parent**, **left**, **right**, **intersections**, **sum**. *Note:* **sum** is the sum of the intersections of nodes rooted at this node, including the root itself.

Pseudocode:

```text
def count-pairs (chords):
  # Takes O(nlogn) time since there are n chords
  # and each Insert operation in AVL Tree takes
  # O(logn) time
  avl-tree = Build-AVLTree (chords)
  number-of-intersection = avl-tree.root.sum
  return number-of-intersection / 2
```

Maintaining the tree structure is pretty standard, as every time we insert a node, we need to first go down the tree to find the correct spot to insert the new node and implement rotation as necessary (*O(logn)*). After insertion, we need to access every ancestor of the node and change the sum of intersection correspondingly (*O(logn)*).
