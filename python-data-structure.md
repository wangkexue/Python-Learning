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
s = set([1, 2, 1, 3])    # s = [1, 2, 3]
s1 = set([3])
sub = s - s1                   
union = s | s1                   
intersect = s & s1
xor = s ^ s1
```
## Dictionary

