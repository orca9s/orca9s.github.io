---
title: Python 복습하기.
description: <center> 학원에서 배운 파이썬 복습하기. </center>
categories:
 - Python
tags:
---

## 파이썬 실행해보기
파이썬 설치를 마쳤다면 이제 실행해 보아야 한다. 우선 표현식에 대해 알아보자.
## 표현식
<br> 표현식이란 값을 의미하는 표현 또는 값을 반환하는 표현을 뜻 한다.
```c
>>> sec = 60
>>> 2 * 3 = 6
```
### 구문
구문은 값의 의미를 지니지 않으며, 어떠한 목적을 수행하는 코드를 뜻 한다.
<img src ="{{ site.url }}/assets/images/blog-python-statement.png" alt="구문 실습" width="400px" height="200px">
### 변수
파이썬은 모든것이 객체로 이루어져 있다. 객체는 데이터의 형태를 결정해주는 타입으로, 파이썬에서는 객체의 타입을 바꿀 수 없다. 프로그래머는 변수를 선언하고 사용하는 형태로 컴퓨터의 메모리에 값을 할당시키고 참조할 수 있다.<br> 파이썬 에서는 값을 할당할때 `=`기호를 사용하여 할당한다.
```c
프로그래밍 언어에서 =은 같다는 의미가 아니라 ==이 같다는 의미이다.
```
아래와 같은 코드를 입력하면 var1이라는 변수에 100이라는 정수를 할당하고 `print`를 이용해 출력한 것이다.
<img src ="{{ site.url }}/assets/images/blog-python-var.png" alt="var출력">
변수는 단지 이름일 뿐이며, 그 자체가 어떠한 값을 갖는것은 아니다.
위의 var1변수는 100이라는 데이터를 직접 가지는 것이 아니라 100이라는 정수형 객체가 있고 var1은 참조하는 역할을 하는 것이다. 아래의 코드를 입력해 본다.
<img src ="{{ site.url }}/assets/images/blog-python-copy.png" alt="var참조" width="200px" height="300px">
변수들이 참조하고 있는 객체가 메모리 상에서 가지고 있는 고유의 주소를 출력하는 id함수를 사용해보자.
<img src ="{{ site.url }}/assets/images/blog-python-copy2.png" alt="var id 출력" width="200px" height="300px">
var1을 제외한 모든 변수들이 같은 객체를 가리키는 것을 볼 수 있다.
var1이 다른 객체를 가리키는 이유는 변수는 언제든 다른 객체를 가리킬 수 있기 때문이다. 위의 경우에는 var1이 참조하는 객체가 바뀐것이다. var2, var3, var4는 var1이 참조하던 객체를 참조하고 있기 떄문에 같은 것이다.
## 변수의 타입 확인하기
변수의 타입을 확인하기 위해선 내장함수인 type을 사용하면 된다.
<img src ="{{ site.url }}/assets/images/blog-python-type.png" alt="type확인" width="300px" height="200px">
var1변수는 정수형 변수임을 알 수 있고, 문자열은 str형임을 나타내준다.  위의 출력에서, 클래스는 객체의 타입을 나타낸다.<br>`class`와 `type`은 거의 같은 의미로 사용된다.

## 변수의 이름 제한
사용가능한 문자
```c
* 소문자
* 대문자
* 숫자
* 언더스코어( _ )
```
이름은 숫자로 시작할 수 없으며, 언더스코어로 시작하는 변수명은 특별한 처리방법을 따르므로 일반적으로 사용하지는 않는다.<br>
예약어
<br>
아래 예약어들은 파이썬 구문을 정의하는데 사용되기 때문에 변수로 사용할 수 없다.
```c
False, class, finally, is, return,
None, continue, for, lambda, try,
True, def, from, nonlocal, while,
and, del, global, not, with,
as, elif, if, or, yield,
assert, else, import, pass,
break, except, in, raise
```
## 변수의 입력과 출력
입력은 내장함수 input을 사용한다.
```c
>>> var = input()
```
입력받는 프롬포트를 띄우려고 할 경우, `input`에 문자열을 인자로 전달해준다.
```c
>>> var = input('숫자를 입력해주세요 : ')
```
출력은 내장함수 print를 사용한다.
```c
>>> print(var)
```
## 수학 연산자
```c
+ 더하기
- 뺴기
* 곱하기
/ 나누기
/ / 정수 나누기
% 나머지
**지수
```

## 산술 연산자 결합
a에 100을 할당하고, 3을 뺸 결과를 다시 a에 할당하기
```c
>>> a = 100
>>> result = a - 3
>>> a = result
>>> print(a)
97
```
위의 코드는 아래와 같이 사용도 가능하다
```c
>>> a = 100
>>> a = a - 3
>>> print(a)
97
```
```c
>>> a = 100
>>> a - = 3
97
```
## 우선순위
```c
>>> 64 + 7 * 3
```
이 경우 곱셈이 우선시 되지만 가독성에 문제가 있기 때문에 괄호로 묶어주는게 좋다.
```c
>>> 34 + (58 * 2)
```
## 진수
기본적으로 숫자형 데이터는 10진수로 간주 되지만, 파이썬에서는 2진수, 8진수, 16진수를 표현할 수 있다.
<br>
2진수(binary): 0b또는 0B로 시작<br>
8진수(octal): 0o또는 0O로 시작<br>
16진수(hex): 0x또는 0X로 시작
<img src ="{{ site.url }}/assets/images/blog-python-base.png" alt="진수 실습" width="300px" height="200px">

## 형변환
내장함수 int, float를 사용
<img src ="{{ site.url }}/assets/images/blog-python-int-float.png" alt="형변환 실습" width="300px" height="200px">

## 문자열
```c
파이썬3에서는 문자열에서 기본적으로 유니코드(Unicode)를 사용하며, 불변(immutable)하다.
```

## 문자열 표현
작은 따옴표 또는 큰 따옴표로 문자열을 표현한다.
```c
>>> '패스트캠퍼스'
  '패스트 캠퍼스'
>>> "패스트 캠퍼스"
  "패스트 캠퍼스"
```
작은 따옴표나 큰 따옴표를 문자열을 표현할 때 사용하면 사용하지 않은 다른 부호는 문자열 내부에서 사용이 가능하다.
```c
>>> ' 패스트캠퍼스 "웹 프로그래밍 스쿨" '
  ' 패스트캠퍼스 "웹 프로그래밍 스쿨" '
```
세 개의 작은 따옴표 또는 큰 따옴표는 여러줄에 걸친 문자열을 나타낼 때 사용한다.
<img src ="{{ site.url }}/assets/images/blog-python-multieline.png" alt="멀티라인 실습" width="300px" height="200px">
