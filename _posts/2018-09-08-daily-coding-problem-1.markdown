---
layout: post
title:  "Exercises: Daily Coding Problem #1"
categories: Programming
tags: [Common Lisp, Python, Daily Coding Problem]
author: Nix
comments: true
description: "Write a function that, given numbers $$ n_{0},n_{1},\\ldots,n_{k} $$ and $$ m $$, determines
if $$ \\exists i,j $$ such that $$ i\\neq j $$ and $$ n_{i}+n_{j}=m $$."
---

Today's exercise:

Write a function that, given numbers $$ n_{0},n_{1},\ldots,n_{k} $$ and $$ m $$, determines
if $$ \exists i,j $$ such that $$ i\neq j $$ and $$ n_{i}+n_{j}=m $$.

Easy enough.

This code is [on GitHub](https://github.com/PedestalNix/polyglot/tree/master/daily-coding-problem/problem-001).

### Python

```python
def has_sum(numbers, target):
    for i in range(len(numbers)-1):
        for j in range(i, len(numbers)):
            if numbers[i] + numbers[j] == target:
                return True
    else:
        return False
```

We could optimize a bit, if we sort the list, but a solution of this nature is
going to be $$ O(n^2) $$ in any case.

If we put the numbers in a dictionary, we can solve it in $$ O(n\log(n)) $$.

```python
from collections import defaultdict

def has_sum_dict(numbers, target):
    d = defaultdict(int)
    for n in numbers:
        d[n] += 1
    for n in d:
        if n == target/2:
            if d[n] >= 2:
                return True
        elif (target - n) in d:
            return True
    else:
        return False
```

### Common Lisp

Substantially the same solution as `has_sum` above, with a little recursion for
flavor:

```common-lisp
(defun has-sum-p (numbers target &optional (count 2))
  (if (= count 0)
      (= target 0)
      (do ((i 0 (1+ i)))
          ((or (> count (- (length numbers) i))
               (has-sum-p (last numbers (- (length numbers) (+ i 1))) (- target (nth i numbers)) (- count 1)))
           (not (> count (- (length numbers) i)))))))
```
