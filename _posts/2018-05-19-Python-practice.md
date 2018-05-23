---
title: Python 복습하기
description: <center> 학원에서 배운 파이썬 복습하기. </center>
categories:
 - Python
tags:
---

# 파이썬 실행해보기
파이썬 설치를 마쳤다면 이제 실행해 보아야 한다. 우선 표현식에 대해 알아보자.
## 표현식
<br> 표현식이란 값을 의미하는 표현 또는 값을 반환하는 표현을 뜻 한다.
```c
>>> sec = 60
>>> 2 * 3 = 6
```
## 구문
구문은 값의 의미를 지니지 않으며, 어떠한 목적을 수행하는 코드를 뜻 한다.
<img src ="{{ site.url }}/assets/images/blog-python-statement.png" alt="구문 실습" width="400px" height="200px">
# 변수
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
# 수학 연산자
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

# 문자열
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
## 문자열 더하기
문자열을 합칠때 사용한다.
<img src ="{{ site.url }}/assets/images/blog-python-textadd.png" alt="문자열 더하기 실습" width="300px" height="200px">

## 문자열 형변환
```c
>>> str(147)
'147'
```
문자열을 제외한 객체를 print함수로 호출하면, 내부적으로 `str`함수를 사용한 결과를 나타내준다.

|   이스케이프 문자   |      설명     |
|:-------:|:-------:|
| /a |  비프음 발생  |
| \t |    탭(tab)  |
| \n | 줄바꿈   |
| \\ | \(역슬래시) 입력 |  
| \' | 작은따옴표(') 입력 |  
| \" | 큰따옴표(") 입력  |

## 인덱스 연산
문자열에서 문자를 추출하기 위해 대괄호와 오프셋을 지정할 수 있다. 가장 왼쪽은 0이며, 가장 오른쪽은 -1로 시작한다.

<img src ="{{ site.url }}/assets/images/blog-python-text-index.png" alt="인덱스 연산 실습" width="400px" height="400px">
문자열은 불변이므로 인덱싱한 부분에 새 값을 대입할 수 없다.
```python
>>> lux[0] = '별'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

## 슬라이스 연산
```c
[start:end:step] 형식을 사용한다.

[:]
처음부터 끝까지
[start:]
start오프셋부터 마지막까지
[:end]
처음부터 end오프셋까지
[start:end]
start오프셋부터 end오프셋까지
[start:end:step]
start오프셋부터 end오프셋까지, step만큼씩 뛰어넘은 부분
```
## 길이
내장함수 len을 사용하면 된다.

## 문자열 나누기
문자열의 내장함수 split을 사용해야한다. spilt함수에 인자로 주어진 구분자를 기준으로 하나의 문자열을 리스트 형태로 반환해준다.

```python
>>>girlsday = '민아, 유라, 소진, 혜리'
>>>girlsday.split(',')
['민아', '유라', '소진', '혜리']
```
split함수에 인자를 주지 않을 경우, 공백문자를 구분자로 사용한다.

## 문자열 결합
split 함수와 반대의 역할을 한다.
문자열 리스트를 하나의 문자열로 결합해주며, 각 문자열을 결합해줄 구분자 문자열을 지정한 후 join함수를 사용해준다.

```python
>>> girlsday_list = girlsday.split(',')
>>> girlsday_str = ','.join(girlsday_list)
>>> print(girlsday_str)
민아, 유라, 소진, 혜리
```

## 대소문자 다루기

```python
>>> lux = 'lux, the lady of Luminosity'
>>> lux.capitalize()
'lux, the lady luminosity'
>>> lux.title()
'lux, The Lady of Luminosity'
>>> lux.upper()
'LUX, THE LADU OF LUMINOSITY'
>>> lux.lower()
'lux, the lady of luminosity'
>>> lux.swapcase()
'LUX, THE LADY OF LUMINOSITY'
```

## 문자열 포맷
옛 스타일(%)
```python
string % data
```

|   변환타입   |      설명     |
|:---:|:---:|
| %s |  문자열  |
| %d |  10진수  |
| %x |  16진수  |
| %o |  8진수  |
| %f |  10진 부동소수점수  |
| %e | 지수로 나타낸 부동소수점수 |  
| %g | 10진 부동소수점수 혹은 지수로 나타낸 부동소수점수 |  
| %% | 리터럴%  |

```python
>>> '%s' % 42
'42'
>>> '%d x %d : %d' % (3, 4, 12)
'3 x 4 : 12'
```

## 정렬
```c
%[정렬기준(-,없음)][전체글자수].[문자길이 또는 소수점 이후 문자길이][변환타입]
```

```python
>>> d = 37
>>> f = 3.14
>>> s = 'Fastcampus'
>>> '%d %f %s' % (d, f, s)
'37 3.140000 Fastcampus'
>>> '%10d %10f %10s' % (d, f, s)
'        37   3.140000 Fastcampus'
>>> '%14d %14f %14s' % (d, f, s)
'            37       3.140000     Fastcampus'
>>> '%-14d %-14f %-14s' % (d, f, s)
'37             3.140000       Fastcampus    '
>>> '%-14.3d %-14.3f %-14.3s' % (d, f, s)
'037            3.140          Fas           '
```

## 새 스타일 ({}, format)
```c
{}.format(변수)
```
```python
# 기본형태
>>> '{} {} {}'.format(d, f, s)
'37 3.14 Fastcampus'

# 각 인자의 순서를 지정
>>> '{1} {2} {0}'.format(d, f, s)
'3.14 Fastcampus 37'

# 각 인자에 이름을 지정
>>> '{d} {f} {s}'.format(d=50, f=1.432, s='WPS')
'50 1.432 WPS'

# 딕셔너리로부터 변수 할당
>>> dict = {'d': d, 'f': f, 's': s}
>>> '{0[d]} {0[f]} {0[s]} {1}'.format(dict, 'WPS')
'37 3.14 Fastcampus WPS'

# 타입 지정자 입력
>>> '{:d} {:f} {:s}'.format(d, f, s)
'37 3.140000 Fastcampus'

# 이름과 타입지정자를 모두 사용
>>> '{digit:d} {float:f} {string:s}'.format(digit=700, float=1.4323, string='Welcome')
'700 1.432300 Welcome'

# 필드길이 10, 우측정렬
>>> '{:10d}'.format(d)
'        37'
>>> '{:>10d}'.format(d)
'        37'

# 필드길이 10, 좌측정렬
>>> '{:<10d}'.format(d)
'37        '

# 필드길이 10, 가운데 정렬
>>> '{:^10d}'.format(d)
'    37    '

# 필드길이 10, 가운데 정렬, 빈 공간은 ~로 채움
>>> '{:~^10d}'.format(d)
'~~~~37~~~~'
```
## `f`표현법
```python
# 기본 형태
apple = '사과'
banana = '바나나'
train = '기차'

f'{apple}는 맛있어 맛있으면 {banana} {banana}는 길어 길면 {train}'

# 옵션 지정
f'''{apple:^10}
{banana:^10}
{train:^10}'''
```
