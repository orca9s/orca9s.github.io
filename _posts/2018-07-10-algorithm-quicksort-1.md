---
title: Algorithm - quik_sort-1
description: <center> Quick정렬을 대비한 재귀함수 </center>
categories:
 - Algorithm
tags:
---


### 유클리드 호제법 - 최대공약수 구하기
```
def get_gcd(num1, num2):  # num1 > num2
   return get_gcd(num2, num1 % num2) if num1 % num2 else num2
```

### 피보나치 뽀개기

```
import time


def fibonacci(index):
   if index < 2:
       return index
   return fibonacci(index - 1) + fibonacci(index - 2)


def fibonacci_non_recursive(index):  # 반복문으로 피보나치 수열을 구해보자
   if index < 2:
       return index

   value = 1
   prev1 = 1
   prev2 = 1

   for i in range(index - 2):
       value = prev1 + prev2
       prev2 = prev1
       prev1 = value

   return value


mem = [0] * 101  # index 번째 피보나치 수열 저장소


def fibonacci_dynamic(index):  # 다이나믹 프로그래밍으로
   if index < 2:
       return index

   # mem 리스트의 인덱스 : index - 2도 가능 - 1, 2번째 리스트는 그냥 리턴하기 때문에 저장안되기 때문에...

   if mem[index]:  # 피보나치 수열을 이미 계산했다면...
       return mem[index]=
   else:  # 계산한 피보나치 수열이 아니에요...
       mem[index] = fibonacci_dynamic(index - 1) + fibonacci_dynamic(index - 2)  # 값 계산해서 리스트에 저장해놓고
       return mem[index]  # 리턴하기


print("--- START ---")
start_time = time.time()
print(fibonacci_dynamic(40))
print("--- %s seconds ---" % (time.time() - start_time))
```