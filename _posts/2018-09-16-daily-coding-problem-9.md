---
layout: post
comments: true
title: "Daily Coding Problem #9"
date: 2018-09-16 23:25:37
categories: Programming
tags: [Daily Coding Problem]
author: Nix
description: Given a list of integers, write a function that returns the largest
  sum of non-adjacent numbers.
---

> Given a list of integers, write a function that returns the largest sum of
> non-adjacent numbers. Numbers can be 0 or negative.
>
> For example, [2, 4, 6, 2, 5] should return 13, since we pick 2, 6, and 5.
> [5, 1, 1, 5] should return 10, since we pick 5 and 5.
>
> Follow-up: Can you do this in O(N) time and constant space?

The follow-up gives this one away, really. We just need to keep track of the
best sums we've found so far, and then on each step decide whether the new
number should be included in the chain (yes, if it's >= 0) and whether it is
better to chain it after the $$(n-1)^\text{th}$$ or the $$(n-2)^\text{th}$$
(whichever is bigger, of course). Then we update our best-sums-so-far and keep
going.

This code is available [on GitHub](https://github.com/PedestalNix/polyglot/tree/master/daily-coding-problem/problem-009).

### Python

```python
def greatest_sum(numbers):
    if len(numbers) <= 2:
        return max(0, *numbers)
    sums = [0, 0] + numbers[:2]
    for n in numbers[2:]:
        sums.append(max(
            0,       # if n <= 0 and so were previous sums
            n,       # if previous sums were <= 0
            n+sums[1],
            n+sums[2],
            sums[1], # if n < 0 either this
            sums[2], #          or this
        ))
        sums.pop(0)

    return max(sums[-2:])
```
