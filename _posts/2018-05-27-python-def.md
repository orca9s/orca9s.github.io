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
함수 결과로 Bool값을 갖는 데이터를 리턴하여 if문이나 while문의 조건으로 사용 가능하다.

## 매개변수를 사용하는 함수 정의
```python
>>> def print_arguments(something):
...   print(something)
...
>>> print_arguments('ABC')
ABC
```
## 매개변수(parameter)와(argument)의 차이

함수 내부에서 함수에게 전달 되어 온 변수는 매개변수라 부르며, 함수를 호출할 때 전달하는 변수는 인자로 부른다.
```python
# 함수 정의때는 매개변수
def func(매개변수1, 매개변수2):
  ...

# 함수 호출시에는 인자
>>> func(인자1, 인자2)
```

## 리턴값이 없을 경우
함수에서 리턴해 주는 값이 없을 경우, 아무것도 없다는 뜻을 가진 `None`객체를 얻는다.

# 위치인자(Positional arguments)
매개변수의 순서대로 인자를 전달하여 사용하는 경우

```python
>>> def student(name, age, gender):
...   return {'name': name, 'age': age, 'gender': gender}
...
>>> student('hanyeong.lee', 31, 'male')
{'name': 'hanyeong.lee', 'age': 31, 'gender': 'male'}
```

## 키워드 인자(keyword arguments)
매개 변수의 이름을 지정하여 인자로 전달하여 사용하는 경우
```python
>>> student(age=31, name='hanyeong.lee', gender='male')
{'name': 'hanyeong.lee', 'age': 31, 'gender': 'male'}
```
위치인자와 키워드인자를 동시에 쓴다면, 위치인자가 먼저 와야 한다.

## 기본 매개변수값의 정의 시점
>>> 기본 매개변수값은 함수가 실행될 때 마다 계산되지 않고, 함수가 정의되는 시점에 계산되어 사용된다.

```python
>>> def return_list(value, result=[]):
...   result.append(value)
...   return result
...
>>> return_list('apple')
['apple']
>>> return_list('banana')
['apple', 'banana']
```
함수가 실행되는 시점에 기본 매개변수값을 계산하기 위해, 아래와 같이 바꿔줘야 한다.

```python
>>> def return_list(value, result=None):
...   if result is None:
...     result = []
...   result.append(value)
...   return result
...
>>> return_list('apple')
['apple']
>>> return_list('banana')
['banana']
```

## 위치인자 묶음
함수에 위치인자로 주어진 변수들의 묶음은 `*매개변수명`으로 사용할 수 있다.<br>
관용적으로`*args`를 사용한다.
```python
def print_args(*args):
  print(args)
```

## 키워드인자 묶음
함수에 키워드인자로 주어진 변수들의 묶음은 `**매개변수명`으로 사용할 수 있다.<br>
관용적으로`**kwargs`를 사용한다.
```python
def print_kwargs(**kwargs):
  print(kwargs)
```
## docstring
함수를 정의한 문서 역할을 한다.
함수 정의 후, 몸체의 시작부분에 문자열로 작성하며, 여러줄로도 작성 가능하다.
```python
>>> def print_args(*args):
...   'Print positional arguments'
...   print(args)
...
>>> help(print_args)
```
## 함수를 인자로 전달
파이썬 에서는 함수 역시 다른 객체와 동등하게 취급되므로, 함수에서 인자로 함수를 전달, 실행, 리턴하는 형태로 프로그래밍이 가능하다.
## 내부 함수
함수 안에서 또 다른 함수를 정의해 사용할 수 있다.

## 스코프(영역)
파이썬에서는 코드 작성 시, 각 함수마다 독립적인 스코프(영역)을 가진다.<br>
메인 프로그램(현재 동작하는 프로그램의 최상위 위치)의 영역은 전역 영역(Global Scope)라고 하며, 전역 스코프 내부에서 독립적인 영역을 갖고 있는 경우에는 지역 영역(Local Scope)라고 부른다.
<br>
아래 코드의 경우 `show_global_champion`함수 내부의 영역은 별개의 로컬 스코프를 가지며, `champion`변수는 전역 영역의 것을 가져와 출력하는것을 볼 수 있다.
```python
champion = 'Lux'

def show_global_champion():
    print('show_global_champion : {}'.format(champion))

show_global_champion()
print('print champion : {}'.format(champion))
```
위 코드를 아래와 같이 변경 후, 실행 해 본다.
```python
champion = 'Lux'

def show_global_champion():
    print('show_global_champion : {}'.format(champion))

def change_global_champion():
    print('before change_global_champion : {}'.format(champion))
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

show_global_champion()
change_global_champion()
```
`change_global_champion`함수에서 오류가 발생한다.<br>

첫 번째 코드에서는 `champion`변수가 함수의 로컬 스코프에 존재하지 않기 때문에 글로벌 스코프에서 해당 변수를 찾아 출력하였으나, 이번 코드에서는 내부에 또다른 `champion`변수가 존재하기 때문에 할당하기 전인 변수를 사용한 것으로 판단하여 프로그램에서 오류를 발생시킨다.
<br>
이름이 같은 두 변수가 다른 객체임을 내장함수`id`를 사용해 확인해보자.<br>
또한, 각 영역에 해당하는 데이터들은 `locals()`함수를 확인 할 수 있으며, 전역 역역의 데이터들은 `globals()`함수를 사용한다.

## 스코핑 룰
스코프는 지역(Local), 전역(Global)외에도 내장(Built-in)영역이 존재하며, 내장영역이 가장 바깥, 그 내부에 전역, 그 내부에 지역 순으로 정의된다.
분리된 영역에서, 외부 영역에서는 내부 영역의 데이터를 사용할 수 없지만 내부 영역에서는 자신의 외부 영역에 있는 데이터를 참조할 수 있다.
(반대의 경우에는 함수의 인자로 데이터를 전달한다)

## 내장 함수와 내장 영역
`print`, `dict`등 지정하지 않고 사용했던 내장 함수들은 위 스코핑 룰의 내장 스코프에 존재하는 함수들이다. <br>
전역 스코프의`__builtin__`변수에 할당되어 있으며, 전역 스코프에서는 해당 변수의 내부를 참조할 수 있도록 파이썬이 시작될 때 자동으로 처리된다.<br>
확인시 `dir`함수를 사용하며, `dir`함수는 해당 객체가 사용 가능한 속성 및 함수들을 리스트 형태로 나타내준다.
# 로컬 스코프에서 글로벌 스코프의 변수를 사용
```python
champion = 'Lux'

def change_global_champion():
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

change_global_champion()
print('print global champion : {}'.format(champion))
```
이 경우, 위의`show_global_champion`함수와는 다르게 `change_global_champion`함수는 `champion`변수에 새로운 값을 대입한다. 만약 로컬 스코프에서 글로벌 스코프의 변수를 변경해야 한다면, 해당 변수가 로컬 스코프에 생성되는 것이 아닌 글로벌 영역에 이미 존재하는 값을 사용함을 명시해주어야 한다.
```python
champion = 'Lux'

def change_global_champion():
    global champion
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

change_global_champion()
print('print global champion : {}'.format(champion))
```
파이썬에서든 한 스코프에서 동일한 이름을 가진 두 스코프의 변수를 사용할 수 없음을 기억해야 한다.

## 내부함수에서의 로컬 스코프(nonlocal)
```python
champion = 'Lux'

def local1():
    champion = 'Ahri'
    print('local1 locals() : {}'.format(locals()))

    def local2():
        champion = 'Ezreal'
        print('local2 locals() : {}'.format(locals()))
    local2()

print('global locals() : {}'.format(locals()))
local1()
```
로컬 스코프 내부에는 또 다른 로컬 스코프가 존재할 수 있다.<br>
전역 스코프가 아닌, 자신의 바로 바깥 영역의 로컬 스코프(자신보다 한 단계 위의 로컬 스코프)의 데이터를 참조하고자 한다면, `nonlocal`키워드를 사용한다.
```python
champion = 'Lux'

def local1():
    champion = 'Ahri'
    print('local1 locals() : {}'.format(locals()))

    def local2():
        nonlocal champion
        champion = 'Ezreal'
        print('local2 locals() : {}'.format(locals()))
    local2()
    print('local1 locals() : {}'.format(locals()))

print('global locals() : {}'.format(locals()))
local1()
```
