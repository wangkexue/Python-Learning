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
                                # be careful of mutable class variable
  def __init__(self, name):
    self.name = name            # instance variable unique to each instance
```
### Random Remarks
```python
foo = 10

class foo:                      # __main__.foo override the global var
  foo = 4                       # overrided by method attribute
  def __init__(self):
    self.foo = 7                # data attribute override method attribute
  def foo(self):                # overrided
    print foo                   # __main__.foo
    print foo.foo               # 7
    print foo.foo()             # Runtime error
```
#### Naming Convention
```python
# package_name/module_name.py
GLOBAL_VARIABLE = 10

class ClassName(object):
  CLASS_CONSTANT = 'cc'
  class_variable = []
  def mathod_name(self, method_param):
    local_variable = 1
    self.instance_variable = 2
    pass
```
"Private" instance variables inside an object don't exist in Python. However it's a convention to name `_private_variable`. 

Python also provite _name mangling_ to avoid name clashes in subclass, that is `__private_name` will be textually replaced by `_classname_private_name`.
```python
class Mapping(object):

  def __init__(self, iterable):
    self.items_list = [];
    self.__update(iterable)
    
  def update(self, iterable):
    for item in iterable:
      self.items_list.append(item)
      
  __update = update              # private copy of update
                                 # so when subclass override update, __init__ won't be broken
class MapplingSubClass(Mapping):

  def update(self, keys, values):
    for item in zip(keys, values):
      self.items_list.append(item)
```

Note: code passed to `exec`, `eval()`, `execfile()` does not consider the classname of the involing class to be the current class.

#### Odds
You can also use an empty class to mimic C "struct".
```python
class Employee:
  pass
  
jphn = Employee()
john.name = 'John Doe'
john.dept = 'computer lab'
john.salary = 1000
```

### (Multiple) Inheritance
Subclass could call the base class method directly by `BaseClass.method_name(self, arg)`.

For simplicity, one can think MRO in MI is determined by DFS, left to right (actually it's true for old-style classes in python 2, [new-style class](https://docs.python.org/2/glossary.html#term-new-style-class) in python 2, those classes inheritated from object, use below algorithm).

In fact, it is slightly more complex; the mro changes dynamically to support cooperative calls to `super()`. This approach is known in some other MI languages as call-next-method and is more powerful than the super call found in SI.

See [https://www.python.org/download/releases/2.3/mro/] for detail.

### Exceptions
User-defined exceptions are identified by classes as well (so it's possible to create extensible hierachies of exceptions). You can `raise Class` or `raise Instance`.
```python
class B(Exception):
  pass
class C(B):
  pass
class D(C):
  pass
  
for cls in [B, C, D]:
  try:
    raise cls()
  except D:
    print("D")
  except C:
    print("C")
  except B:
    print("B")
```
### Iterators
Iterator just call [`__next__()`](https://docs.python.org/3/library/stdtypes.html#iterator.__next__)  and when there is no iterms it raises a [`StopIteration`](https://docs.python.org/3/library/exceptions.html#StopIteration) exception.
```python
class Reverse:
  """Iterator for looping over a seq reversely 
     an example of adding iter() to user defined class"""
  def __init__(self, data):
    self.data = data
    self.index = len(data)
  def __iter__(self):
    return self
  def __next__(self):
    if self.index == 0:
      raise StopIteration
    self.index = self.index - 1
    return self.data[self.index]
```
### Generators
It uses `for` and `yield` the same way as Scala. (or without `yield` for generating instant var) 

What makes generators so compact is that the `__iter__()` and `__next()__` methods are created automatically, besides local var and execution state is stored between calls.
### [abc -- Abstract Base Classes](https://docs.python.org/3/library/abc.html)

### @classmethod @staticmethod
`@staticmethod` has no obligatory param, and it has no access to the object and its internel. It's just a function bounding to a the class, can be used before initialization.

`@classmethod` with the first parmam as the class (usually named as `cls`), and it also only has access to the class rather than an object instance.

[overloading __init__ in python](http://stackoverflow.com/questions/141545/overloading-init-in-python)
#### style
see Function and Method Decorators
