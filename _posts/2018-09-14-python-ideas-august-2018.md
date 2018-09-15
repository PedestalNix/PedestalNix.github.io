---
layout: post
comments: true
title: Python-ideas (August 2018)
categories: python-ideas-summary
tags: [Python, Python-ideas]
author: Nix
description: Summary of some topics of interest discussed on Python-ideas during
    August 2018. The discussion about design by contract was particularly
    interesting.
---

### [PEP 505: None-aware operators][m052532]

[The discussion the previous month][m052036] about [PEP 505] None-aware operators continues ([second thread][m052560]).

[m052532]: https://mail.python.org/pipermail/python-ideas/2018-August/052532.html
[m052036]: https://mail.python.org/pipermail/python-ideas/2018-July/052036.html
[PEP 505]: https://www.python.org/dev/peps/pep-0505/
[m052560]: https://mail.python.org/pipermail/python-ideas/2018-August/052560.html

### [With expressions][m052549]

Ken Hilton suggests that an expression version of the `with` statement would be useful. For example:

```python
contents = f.read() with open('file') as f #the most obvious one
multiplecontents = [f.read() with open(name) as f for name in names] #reading multiple files
```

The rejected [PEP 463] (Exception-catching expressions) is mentioned.

[m052549]: https://mail.python.org/pipermail/python-ideas/2018-August/052549.html
[PEP 463]: https://www.python.org/dev/peps/pep-0463/

### [Revisiting dedicated overloadable boolean operators][m052576]

Todd suggests new operators and corresponding dunder methods for boolean `and`, `or`, `not`, and `xor`, so that projects that need custom behavior from these (e.g. numpy or sqlalchemy) need not abuse the existing bitwise operators. A discussion about allowing custom infix operators develops.

[m052576]: https://mail.python.org/pipermail/python-ideas/2018-August/052576.html

### [Syntactic sugar to declare partial functions][m052605]

Fabrizio Messina proproses using curly braces as syntactic sugar for declaring partial functions.

Robert Vanden Eynde suggests using [funcoperators] (which is his project) for this.

Eventually the discussion descends into a less-than-polite argument about whether jargon is harmful. [Some discussion follows][m052702] about how to improve the quality of discourse, and eventually some [more extensive discussion][m052743] about the use of jargon, partciuarly centered on `lambda`.

[m052605]: https://mail.python.org/pipermail/python-ideas/2018-August/052605.html
[funcoperators]: https://pypi.org/project/funcoperators/
[m052702]: https://mail.python.org/pipermail/python-ideas/2018-August/052702.html
[m052743]: https://mail.python.org/pipermail/python-ideas/2018-August/052743.html

### [Make "yield" inside a with statement a SyntaxError][m052636]

Ken Hilton suggests that it is problematic to `yield` from inside a `with` statement, because then the `with` will stay open (e.g. leaving file handles open longer than expected).

[m052636]: https://mail.python.org/pipermail/python-ideas/2018-August/052636.html

### [Python docs page: In what ways is None special][m052737]

Jonathan Fine announces a [draft piece of documentation][none-is-special] that introduces `None`.

[m052737]: https://mail.python.org/pipermail/python-ideas/2018-August/052737.html
[none-is-special]: https://github.com/jfine2358/py-jfine2358/blob/master/docs/none-is-special.md

### [Pre-conditions and post-conditions][m052781]

Marko Ristin-Kaufmann suggests that python should better support design by contract, giving [icontract] as an example of a python implementation of the idea.

[m052781]: https://mail.python.org/pipermail/python-ideas/2018-August/052781.html
[icontract]: https://github.com/Parquery/icontract/

### [A GUI for beginners and experts alike][m052962]

Mike Barnett suggests that his project [PySimpleGUI] should be made part of the standard library, leading to some discussion of existing python GUI options.

[m052962]: https://mail.python.org/pipermail/python-ideas/2018-August/052962.html
[PySimpleGUI]: https://github.com/MikeTheWatchGuy/PySimpleGUI

### [Unpacking iterables for augmented assignment][m053012]

James Lu suggests that it should be possible to use augmented assignment with iterables:

```python
a = 0
b = 0
a, b += 1, 2
# a is now 1
# b is now 2
```

[m053012]: https://mail.python.org/pipermail/python-ideas/2018-August/053012.html
