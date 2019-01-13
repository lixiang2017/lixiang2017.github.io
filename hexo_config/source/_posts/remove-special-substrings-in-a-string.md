---
title: Remove Special Substrings in a String
date: 2018-12-01 00:28:32
categories:
tags:
---
删除字符串中的“b”和“ac”，即保证删除后的结果中不出现“b”和“ac”。
例如：acbac ==> ""；aaac ==> aa；ababac ==> aa；bbbbd ==> d。
```python
# Cloudin云英 面试题
# remove "b" and "ac" in a string


def remove_special_strings(s):
    i = 0
    while i < len(s):
        if s[i] == "b":
            s = s[: i] + s[i+1:]
            continue

        if i >= 1 and s[i-1: i+1] == "ac":
            s = s[: i-1] + s[i+1:]
            i -= 1
            continue

        i += 1
    return s


if __name__ == "__main__":
    s = "qwert"
    print(s, "==>", remove_special_strings(s))
    s = "aacc"
    print(s, "==>", remove_special_strings(s))
    s = "aaaacccc"
    print(s, "==>", remove_special_strings(s))
    s = "acbac"
    print(s, "==>", remove_special_strings(s))
    s = "aaac"
    print(s, "==>", remove_special_strings(s))
    s = "ababc"
    print(s, "==>", remove_special_strings(s))
```
![](remove_substrings.png)
```python
# Cloudin云英 面试题
# remove "b" and "ac" in a string
# use stack


def remove_special_strings_stack(s):
    stk = []
    for i in s:
        if i == "b":
            continue
        elif len(stk) >= 1 and i == "c" and stk[-1] == "a":
            stk.pop(-1)
            continue
        else:
            stk.append(i)

    return "".join(stk)


if __name__ == "__main__":
    s = "qwert"
    print(s, "==>", remove_special_strings_stack(s))
    s = "aacc"
    print(s, "==>", remove_special_strings_stack(s))
    s = "aaaacccc"
    print(s, "==>", remove_special_strings_stack(s))
    s = "acbac"
    print(s, "==>", remove_special_strings_stack(s))
    s = "aaac"
    print(s, "==>", remove_special_strings_stack(s))
    s = "ababc"
    print(s, "==>", remove_special_strings_stack(s))
    s = "accccc"
    print(s, "==>", remove_special_strings_stack(s))
```
