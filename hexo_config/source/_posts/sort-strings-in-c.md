---
title: Sort Strings in C
date: 2018-11-29 11:42:54
categories:
tags:
---

问题描述
![](sort_strings_question.jpg)
The function strlwr() is a function from the Microsoft c library and does not work in the standard c library. 
因此linux gcc需要自定义strlwr函数原型。自己写一个strlwr.h原型，放在/usr/inlcude/里面。

```c
// /usr/include/strlwr.h
char *strlwr(char *s) 
{
    char *str;
    str = s;
    while(*str != '\0')
    {   
        if(*str >= 'A' && *str <= 'Z')
        {   
            *str += 'a'-'A';
        }   
        str++;
    }   
    return s;
}

```

```c
#include <stdio.h>
#include <string.h>
#include <strlwr.h>

int main()
{
    int i, j, n;
    char str[15][100], str1[15][100], tmp[15];

    scanf("%d", &n);
    for(i = 0; i < n; i++)
    {   
        scanf("%s", str[i]);
    }   

    for(i = 0; i < n-1; i++)
    {   
        for(j = i+1; j < n; j++)
        {   
            if(strcmp(strlwr(str[i]), strlwr(str[j])) > 0)
            {   
                strcpy(tmp, str[i]);
                strcpy(str[i], str[j]);
                strcpy(str[j], tmp);
            }   
        }   
    }   

    for(i = 0; i < n; i++)
    {   
        puts(str[i]);
    }   
}
```
