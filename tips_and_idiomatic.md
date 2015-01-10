[Python: izip vs zip - Stack Overflow](http://stackoverflow.com/questions/4989763/what-is-the-difference-between-izip-and-zip-in-python)

`izip` call by need like stream, while `zip` will generate a list (of pair?)
```python
import timeit
from itertools import izip
a = range(1, 10000)
b = range(9999)

print timeit.timeit('any(x > y for x, y in izip(a, b))', setup='from __main__ import a, b, izip', number=1000)
print timeit.timeit('any(x > y for x, y in zip(a, b))', setup='from __main__ import a, b', number=1000)
""" the output should be something like this:
0.00149917602539
0.933961868286
"""
```
