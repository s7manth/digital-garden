---
title: Dunder Methods in Python
summary: Fun fact - Dunder methods are called Magic methods in Python. Are they so magical to deserve that name? Let’s find out. 
publish_date: 2023-01-20
---

Python becomes really fun to work with when it becomes advanced. And the good part is that, even though advanced may sound a bit too much, Python never fails to amuse us with how easy it is to work with things in general. 

Dunder methods are one of those concepts where if you know it, you will want to use it wherever possible, just because it functions in such a cool manner. 

TL;DR dunder methods, mostly, begin with two underscores `__` . Let me show you an example using the `Lit` class. 

```python
class Lit:
    def __init__(self, value):
        self.value = value
        self.expression = str(value)
        self.left = None
        self.right = None
        self.operator = None

    def Add(self, other):
        result = Lit(self.value + other.value)
        result.expression = f'({self.expression} + {other.expression})'
        result.left = self
        result.right = other
        result.operator = '+'
        return result

    def Mul(self, other):
        result = Lit(self.value * other.value)
        result.expression = f'({self.expression} * {other.expression})'
        result.left = self
        result.right = other
        result.operator = '*'
        return result

    def Sub(self, other):
        result = Lit(self.value - other.value)
        result.expression = f'({self.expression} - {other.expression})'
        result.left = self
        result.right = other
        result.operator = '-'
        return result
    
    def Div(self, other):
        if other.value == 0:
            raise ArithmeticError('Division by zero')
        
        result = Lit(self.value / other.value)
        result.expression = f'({self.expression} / {other.expression})'
        result.left = self
        result.right = other
        result.operator = '/'
        return result

    def FloorDiv(self, other):
        if not isinstance(other, Lit): 
            return

        if other.value == 0:
            raise ArithmeticError('Division by zero')
        
        result = Lit(self.value // other.value)
        result.expression = f'({self.expression} // {other.expression})'
        result.left = self
        result.right = other
        result.operator = '//'
        return result

    def __repr__(self):
        return self.expression

    def __str__(self):
        return self.expression

    def evaluate(self) -> int:
        return self.value

    def __add__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)

        return self.Add(other)
    
    def __radd__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)

        return other.Add(self)

    def __sub__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)

        return self.Sub(other)
    
    def __rsub__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)
        
        return other.Sub(self)

    def __mul__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)

        return self.Mul(other)
    
    def __rmul__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)
        
        return other.Mul(self)

    def __floordiv__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)

        return self.FloorDiv(other)

    def __rfloordiv__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)
        
        return other.FloorDiv(self)

    def __truediv__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)

        return self.Div(other)

    def __rtruediv__(self, other):
        if not isinstance(other, Lit):
            other = Lit(other)
        
        return other.Div(self)
```

Wow, that’s a lot of dunder methods. Let’s go step by step. 

Lit class essentially represents a literal expression, currently supporting as a wrapper class for integers and floats. Think of it as a simulation for understanding expression trees and precedence of operators. The class preserves the whole computation as a string, evaluates the final value if and when needed, and follows the following grammar (informally expressed). 

```
expression := constant | expression operator expression
constant := any real number
operator := + | - | // | / | *
```

Let’s understand this more through an example. 

```python
from literal_expression import Lit

a = Lit(4) # all you need is one literal to get started 
b = 3 + a
c = b * 4
d = 5 - c

print(d) # the output is: (5 - ((3 + 4) * 4))
```

In the example shown above, it is clear that dunder methods provide a magical functionality. The fact that you can use the operators directly with the class objects and play with them is mesmerizing to me, at least. Yes, that’s what dunder methods allow you to do. They basically can be used to overload built-in python functionality like operators, calling, implicit string representation. 

More popular dunder methods: 

- `__call__` 
This method is used to specify functionality when a user calls using the class name. So, if this method is supported by a class, one can do something like this

```python
from class import Class

c1 = Class(...)
c1() # functionality implemented by __call__ is fulfilled 
```

- `__del__` 
This method is to overload for the `del` keyword. Most commonly, this is used to forcefully specify the deletion of an object instance, or resetting the same. Python does this automatically when the program ends its execution as a means of automated garbage collection.

```python
from class import Class

c1 = Class(...)
del c1 # functionality implemented by __del__ is fulfilled 

# as mentioned, this happens by default as well, so there is no point specifying
# del object at the end of file 
```

- `__len__` 
This method allows users to call `len` function on the object.

```python
from class import Class

c1 = Class(...)
len(c1) # functionality implemented by __len__ is fulfilled 
```

Some key observations and trivia: 

- `__init__` is also a dunder method that allows you to create instances of a class.
- `__str__` and `__repr__` are two seemingly ambiguous methods that seem to have the same job. The subtle difference, however, is that the goal of `__repr__` is to be unambiguous and the goal of `__str__` is to be readable. In other words, `__str__` acts like a typical `to_string()` method in other languages. `__repr__` is used for debugging purposes.
- There are a bunch of methods that allow you to specify in-place operations. These dunder methods begin with ‘i’. For instance, `__iadd__` method is like the `__add__` method. But, it is invoked when using the `+=` operator. Similarly, you have `__imul__` , `__idiv__` , `__isub__`.
