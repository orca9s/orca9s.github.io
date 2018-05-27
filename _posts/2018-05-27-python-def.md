---
title: Python 함수
description: <center> 학원에서 배운 파이썬 복습하기. </center>
categories:
 - Python
tags:
---

# 함수
반복적인 작업을 하는 코드를 재사용이 가능하게 정의해 놓은 것.
```python
def 함수명(매개변수[parameters]):
  동작
```
## 함수의 정의, 실행
```python
# 실행 시 'call function!'을 print하는 함수 정의
>>>def call_function():
      print('call function!')

# 함수 자체는 function객체를 참조하는 변수
>>> call_function
<function func at 0x10dabf378>

# 함수를 실행시키기 위해 () 사용
>>> call_function()
call_function:
```
## 리턴값이 있는 함수 정의
```python
>>> def return_ture():
      return True

>>> return_ture()
True
```

## 함수 결과로 Bool값을 갖는 데이터를 리턴하여 if문이나 while문의 조건으로 사용 가능하다.
