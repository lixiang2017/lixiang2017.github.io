---
title: Method Chaining or Cascading in Python
date: 2019-01-23 20:08:44
categories:
tags:
---
```python
class Person:
    def name(self, name):
        self.name = name
        return self

    def age(self, age):
        self.age = age
        return self

    def show(self):
        print "My name is", self.name, "and I am", self.age, "years old."


if __name__ == "__main__":
    p = Person()
    p.name("Li Xiang").age(18).show()
```

```cmd
My name is Li Xiang and I am 18 years old.
```
