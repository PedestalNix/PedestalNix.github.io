---
layout: post
comments: true
title: "Daily Coding Problem #5"
date: 2018-09-15 21:23:35
categories: Programming
tags: [Daily Coding Problem, Python]
author: Nix
description: Implement `car` and `cdr` given a `cons` function.
---

Given the following `cons`:

```python
def cons(a, b):
    def pair(f):
        return f(a, b)
    return pair
```

Implement `car` and `cdr` such that `car(cons(1, 2)) == 1` and
`cdr(cons(1, 2)) == 2`. Generally, `car` should return the first element of the
pair, and `cdr` should return the second.

### Python

The solution practically writes itself:

```python
def car(pair):
    return pair(lambda a, b: a)

def cdr(pair):
    return pair(lambda a, b: b)
```

Chaining with `cons` works as you'd expect:

```pycon
>>> car(cdr(cons(1, cons(2, 3)))) == 2
True
>>> cdr(cdr(cons(1, cons(2, 3)))) == 3
True
```

For lisp-style lists it'd look something like:

```pycon
>>> car(cdr(cdr(cons(1, cons(2, cons(3, None)))))) == 3
True
```

The only thing of note with this problem is that `cons` is defined to return a
higher-order function closed over `a` and `b`, so our `car` and `cdr` should
call it with the actual function on the pair as an argument.
