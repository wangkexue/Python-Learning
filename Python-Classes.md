### Namespace
Namespace is generally implemented in Python by dict.
```python
__main__
__module__
```
#### Method Objects

```python
class MyClass:
  def f(self):
    print "hello world"
```
A call to `x.f()` is exactly equvalent to `MyClass.f(x)`.

#### Class and Instance Variables
```python
class Dog:
  kind = 'canine'               # class variable shared by all instances (static)
  
  def __init__(self, name):
    self.name = name            # instance variable unique to each instance
```
