---
title: Algorithm - insertion_sort
description: <center> Algorithm insertion_sort </center>
categories:
 - Algorithm
tags:
---

## insertion_sort

```
def insertion_sort(list):
    length = len(list)
    
    for i in range(1, length):
        curr = list[i]
        index = i
        
        while index > 0 and list[index - 1] > curr:
            list[index] = list[index-1]
            index -= 1
            
        list[index] = curr
    return list
print(insertion_sort(numbers.copy()))
```