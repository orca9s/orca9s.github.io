---
title: Algorithm
description: <center> Algorithm selection_sort </center>
categories:
 - Algorithm
tags:
---

## selection_sort

```
import random
numbers = list()
# range 범위 정해주기
for i in range(10):
    numbers.append(random.randrange(100))
def selection_sort(a):
    length = len(a)
    # 마지막 수는 비교할 필요가 없기 떄문에 length - 1을 해준다.
    for i in range(length - 1):
        # 최소 값을 min_index라고 주고 i라고 설정 변수가 i이기 때문에
        min_index = i
        # 여기선 i자신은 비교할 필요가 없기 때문에 i+1부터 시작 하면 된다 정해진 범위 까지 검사.
        for j in range(i+1, length):
            # 우리는 여태 인덱스 값을 가지고 비교를 한것이다. 하지만 실제 비교할 때는 숫자 끼리 비교해야 하기 
            # 때문에 a안의 실제 값을 입력해 주어야 하기 때문에 a[j]이런 표현으로 쓴다.
            # min_index가 정말 가장 작은 값인지 검
            if a[j] < a[min_index]:
                min_index = j
        # min_index가 가장 작은 값이면 비교할 필요가 없기 때문에 검사 해준다.
        if min_index != i:
            a[min_index], a[i] = a[i], a[min_index]
    return(numbers)
print(selection_sort(numbers))
        
```