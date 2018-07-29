---
title: 합병정렬
description: <center> sort </center>
categories:
 - sort
tags:
---



### 합병정렬

```
def merge_sort(list):
    length = len(list)

    # divide 해야하는 상황
    if length > 1:

        # 리스트를 반토막내기
        mid = length // 2  # 반으로 자를 인덱스
        left_list = list[:mid]
        right_list = list[mid:]

        # length == 1일 때까지 재귀적으로 자른다
        merge_sort(left_list)
        merge_sort(right_list)

        # divide를 마쳤으니 conquer(정렬하기)
        i = 0  # left_list에서 쓸 인덱스
        j = 0  # right_list에서 쓸 인덱스
        k = 0  # list에서 쓸 인덱스

        length_left = len(left_list)
        length_right = len(right_list)

        while i < length_left and j < length_right:  # 아직 리스트에 정렬하지 않은 항목이 남아있으면
            if left_list[i] < right_list[j]:
                list[k] = left_list[i]
                i += 1
                k += 1
            else:
                list[k] = right_list[j]
                j += 1
                k += 1

        while i < length_left:
            list[k] = left_list[i]
            i += 1
            k += 1

        while j < length_right:
            list[k] = right_list[j]
            j += 1
            k += 1

    return list
    
```