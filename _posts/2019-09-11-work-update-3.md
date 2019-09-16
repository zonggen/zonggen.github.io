---
layout: post
title:  "Work Update #3"
categories: [ blog, work]
featured-img: work-update-2
---

These two days I have been learning Rust. Unlike Javascript, I would love to
learn Rust more throughly since multiple of our projects uses Rust and we are
also planning to migrate to Rust for coreos-assembler so it might be very helpful
to have good fundamentals.

Here is a summary of _unique_ feature that Rust has comparing to C, Java, Python and Haskell, to
which Rust somewhat resembles in some way:
 - Rust prevent memory vulnerabilities by taking ownership of memeory (aka one heap memory chunk
 belongs to only one control block)
 - Lifetimes of references
 - No `null` value in Rust

Similarities with other languages:
 - Haskell (Functional Programming Languages): Monads,Iterators, Closures, Memoiization (Lazy Evaluation)
 - Java (OOP): Traits (Interfaces), Generic Types
 - C++: Smart pointers
 - C: Channel (Pipe)

Reference:
 - [The Rust Programming Language](https://doc.rust-lang.org/book/title-page.html),
_by Steve Klabnik and Carol Nichols, with contributions from the Rust Community_