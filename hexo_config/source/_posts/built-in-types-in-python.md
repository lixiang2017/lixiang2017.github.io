---
title: Built-in Types in Python
date: 2018-11-28 01:04:43
categories:
tags:
---

```python
# type
print(" 0.type example")
print(type(type(int('227'))))
print(type(type('227')))
print(type(type('227')) == type)
print(type(type('227')) == "type")

# three distinct numeric types: integers, floating point numbers, and complex numbers.
# Booleans
print(" 1.0 bool example")
print(type(True))
print(type(False))
print(type(True) == bool)
print(type(True) == int)
# int
print(" 1.1 int example")
print(type(120))
print(type(120) == int)
# float
print(" 1.2 float example")
print(type(2.5))
print(type(2.5) == float)
# complex
print(" 1.3 complex example")
print(complex)
print(complex())
print(complex(3 + 4j))
print(type(complex(2 + 6j)))
print(type(complex(1 + 2j)) == complex)

# str
print(" 2.str example")
print(type(""))
print(type(''))
print(type(''''''))
print(type(""""""))
print(type('''test'''))
print(type("""test"""))
print(type("") == str)

# list
print(" 3.list example")
print(type([]))
print(type([]) == list)

# tuple
print(" 4.tuple example")
print(type(()))
print(type(()) == tuple)

# set
print(" 5.set example")
print(type({}))
print(type({1, 4, 2}))
print(type({1, 4, 2}) == set)

# dict
print(" 6.dict example")
print(type({}))
print(type({1: 2}))
print(type({1: 2}) == dict)
print(set == dict)

# frozenset
print(" 7.frozenset example")
print(frozenset([1, 4, 3, 5, 2]))
print(type(frozenset([1, 4, 3, 5, 2])) == frozenset)
```
