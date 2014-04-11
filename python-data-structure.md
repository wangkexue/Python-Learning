## List-based Structure
### Stack
```python 
stack = [1, 2, 3] 
stack.append(4)  
stack.pop()    # 4
```
### Queue
Use [collections.deque](https://docs.python.org/2/library/collections.html#collections.deque) is more efficient.
```python
from collections import deque
queue = deque([1, 2, 3])
queue.append(4)
queue.popleft()    # 1
```
## Sets
No duplicate elements.
```python
s = set([1, 2, 1, 3])    # s = set([1, 2, 3])
1 in set                 # True
s1 = set([3])
sub = s - s1                   
union = s | s1                   
intersect = s & s1
xor = s ^ s1
```
Set comprehensions.
```python
s = {x for x in 'abracadabra' if x not in 'abc'}    # s = set(['r', 'd'}])
```
## Dictionaries
the same as lisp's associative array `((jack . 4098) (sape . 4139))` or an unordered_map
```python
tel = {'jack': 4098, 'sape': 4139}
tel['guido'] = 4127
'guido' in tel    # True
tel = dict([('jack', 4098), ('sape', 4139)])
```
Dict comprehensions.
```python
{x: x**2 for x in (2, 4, 6)}    #{2: 4, 4: 16, 6: 36}
```
When keys are simple string:
```python
dict(jack=4098, sape=4139)
```


