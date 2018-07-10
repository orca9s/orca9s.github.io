---
title: Algorithm - bubble_sort
description: <center> Algorithm bubble_sort </center>
categories:
 - Algorithm
tags:
---

## bubble_sort

```
import random
numbers = [random.randrange(1000) for i in range(10)]

def bubble_sort(list):
    length = len(list)
    for i in range(length -1, 0, -1):
        for j in range(i):
            if list[j] > list[j+1]:
                list[j], list[j+1] = list[j+1], list[j]
    return list
print(bubble_sort(numbers))
```