---
title: Python 딕셔너리, 셋
description: <center> 학원에서 배운 파이썬 복습하기. </center>
categories:
 - Python
tags:
---

# 딕셔너리(dictionary)
Key-Value형태로 항목을 가지는 자료구조.

## 딕셔너리 생성
```python
>>> dict1 = {}
>>> dict2 = dict()
>>> champion_dict = {
    'lux': 'the lady of luminosity',
    'ahri': 'the Nine-Tailed Fox',
    'Ezreal': 'the Prodigal Explorer',
    'Teemo': 'the Swift Scout'
}
```
## 형변환
## dict 함수를 사용, 두 값의 시퀀스(리스트 또는 튜플)을 딕셔너리로 변환 한다.
```python
>>> sample = [[1,2], [3,4], [5,6]]
>>> dict(sample)
{1: 2, 3: 4, 5: 6}
```
## 항목 찾기/추가/변경[key]
```python
>>> champion_dict['lux']
'the lady of luminosity'
>>> champion_dict['Sona'] = 'Maven of the Strings'
>>> champion_dict
{'lux': 'the lady of luminosity',
 'ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings'}
>>> champion_dict['Lux'] = 'Demacia'
>>> champion_dict
{'lux': 'the lady of luminosity',
 'ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings',
 'Lux': 'Demacia'}
```
## 항목이 없을 경우 기본값을 지정하고 찾기
```python
champion_dict.get('Soraka') #없을경우 None
champion_dict.get('Soraka', 'Healer') #없을 경우'Healer'문자열
```
## 결합(update)
```python
>>> item_dict = {
    'Doran\'s Ring': 400,
    'Doran\'s Blade': 450,
    'Doran\'s Shield': 450,
}
>>> com_dict = {}
>>> com_dict.update(champion_dict)
>>> com_dict.update(item_dict)
>>> com_dict
{'lux': 'the lady of luminosity',
 'ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings',
 'Lux': 'Demacia',
 "Doran's Ring": 400,
 "Doran's Blade": 450,
 "Doran's Shield": 450}
```
서로 같은 키가 있을 경우, update에 주어진 딕셔너리의 값이 할당된다.

## 삭제(del)
```python
>>> del com_dict['Doran\'s Blade']
>>> del com_dict['Doran\'s Shield']
>>> com_dict
{'lux': 'the lady of luminosity',
 'ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings',
 'Lux': 'Demacia',
 "Doran's Ring": 400}
```
## 전체 삭제 (clear)
전체 항목을 삭제
```python
>>> com_dict.clear()
>>> com_dict
{}
```
## in으로 키 검
True/False를 반환한다.

## 키 또는 값 얻기
keys(): 모든 키 얻기<br>
values(): 모든 값 얻기 <br>
items(): 모든 키-값 얻기(튜플로 변환)<br>
복사 : copy()

```python
>>> colors = {
     ...:      ...: 'red':'apple',
     ...:      ...: 'yellow':'banana',
     ...:      ...: 'green':'melon',
     ...:      ...: }

>>> color_dict = colors

>>> color_dict.keys()
>>> dict_keys(['red', 'yellow', 'green'])

>>> color_dict.values()
>>> dict_values(['apple', 'banana', 'melon'])

>>> color_dict.items()
>>> dict_items([('red', 'apple'), ('yellow', 'banana'), ('green', 'melon')])
```
# 셋(Set)
셋은 키만 있는 딕셔너리와 같으며, 중복된 값이 존재할 수 없다.

## 셋 생성
```python
>>> empty_set = set()
>>> champions = {'lux', 'ahri', 'ezreal'}
```
## 형변환
문자열, 리스트, 튜플, 딕셔너리를 셋으로 변환할 수 있으며, 중복된 값이 사라진다.
```python
>>> set('ezreal')
{'a', 'e', 'l', 'r', 'z'}
```
```python
>>>set(champion_dict)
{'Ezreal', 'Lux', 'Sona', 'Teemo', 'ahri', 'lux'}
```
딕셔너리 키만 남는다

## 집합 연산

|   연산자   |      설명     |
|:---:|:---:|
| \| |  합집합(Union)  |
| & |  교집합(Intersection)  |
| - |  차집합(Difference)  |
| ^ |  대형차집합(Exclusive)  |
| <= |  부분집합(Subset)  |
| < | 진부분집합(Priper subset) |  
| >= | 상위집합(Superset) |  
| > | 진상위집합(Proper superset)  |

```python
>>> A = {1,2,3,4,5}
>>> B = {4,5,6,7,8,9}
>>> C = {4,5,6}
>>> A|B
{1, 2, 3, 4, 5, 6, 7, 8, 9}
>>> A&B
{4, 5}
>>> A-B
{1, 2, 3}
>>> B-A
{6, 7, 8, 9}
>>> A^B
{1, 2, 3, 6, 7, 8, 9}
>>> A <= B
False
>>> C <= B
True
>>> C < B
True
>>> B <= B
True
>>> B < B
False
```
