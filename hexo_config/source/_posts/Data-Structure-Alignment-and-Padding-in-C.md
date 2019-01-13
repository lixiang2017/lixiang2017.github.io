---
title: Data Structure Alignment and Padding in C
date: 2018-12-01 18:44:09
categories:
tags:
---

```c
// Coundin云英 面试
#include <stdio.h>

typedef struct
{
    char c;
    int i;
}T_FOO;

typedef struct
{
    int i;
    char c;
}U_FOO;

int main()
{
    printf("sizeof(char) = %ld\n", sizeof(char));
    printf("sizeof(int) = %ld\n", sizeof(int));
    printf("sizeof(long) = %ld\n", sizeof(long));
    
    T_FOO a;
    U_FOO b;
    
    printf("a.c -> %ld, a.i -> %ld\n", (void *)&a.c - (void *)&a, (void *)&a.i - (void *)&a);
    printf("b.i -> %ld, b.c -> %ld\n", (void *)&b.i - (void *)&b, (void *)&b.c - (void *)&b);

    printf("sizeof(a) = %ld\n", sizeof(a));
    printf("sizeof(b) = %ld\n", sizeof(b));
    return 0;
}
```
![](alignment.png)
