---
layout: post
comments: true
title: "Daily Coding Problem #3"
categories: Programming
tags: [Daily Coding Problem, Python]
author: Nix
description: Write functions to serialize and deserialize a binary tree.
---

Given the root of a binary tree, write functions `serialize` and `deserialize`
that convert the tree to a string and back.

This code is available [on GitHub](https://github.com/PedestalNix/polyglot/blob/master/daily-coding-problem/problem-003/problem_003.py).

### Python

With a properly written `__repr__` on the node class, this problem is trivial.

```python
def __repr__(self):
    return f"Node(val={self.val!r}, left={self.left!r}, right={self.right!r})"
```

Then the serialize and deserialize functions are just `repr` and `eval`:

```python
def serialize(node):
    return repr(node)

def deserialize(s):
    return eval(s)

# or more simply
serialize = repr
deserialize = eval
```

Even if we can't modify the `Node` class (maybe it has its own special
`__repr__` that doesn't work for this?), it's a simple problem to recursively
serialize the nodes:

```python
def serialize_beta(node):
    if node is None:
        return "None"
    return f"Node(val={node.val!r}, left={serialize_beta(node.left)}, right={serialize_beta(node.right)})"
```

And then `deserialize` is still just `eval`.

The problem of serializing and deserializing objects with random shapes isn't so
simple as this. In particular, if `node.val` isn't something with a useful
`repr` then this won't work. You could try to do something with `node.__dict__`
for arbitrary objects, but that wouldn't get you much further.

In more complex situations it'd be better to go with the standard library's
[pickle] module--actually, it'd be better for any case other than a homework
problem asking you to implement object serialization. `pickle` will keep track
of objects with multiple references to ensure that all the references point to
the same object when unpickled. There are situations `pickle` doesn't handle,
but it's good to use the standard library wherever practical. See also [json]
and [shelve] for alternatives in the standard library.

If you're not happy with the use of `eval`, then it'd be easy enough to write
functions that will recursively create the needed nodes and join them together,
but I've spent enough time on this already.

[pickle]: https://docs.python.org/3/library/pickle.html
[json]: https://docs.python.org/3/library/json.html
[shelve]: https://docs.python.org/3/library/shelve.html
