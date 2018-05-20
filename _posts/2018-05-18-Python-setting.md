---
title: mac os에 Python 설치.
description: <center> mac os에 Python설치하기 </center>
categories:
 - Python
tags:
---

# pyenv라이브러리 설치하기
우선 python을 설치하기 전 python을 버전별로 관리하기 편하게 도와주는 프로그램인 pyenv를 설치해야 한다.<br> 그래야 각각의 라이브러리간의 충돌을 막을 수 있다.  아래를 보고 pyenv를 설치하도록 하자.
```c
brew install pyenv
brew install pyenv-virtulenv
```
## pyenv 설청하기
pyenv 설치를 완료했다면 shell을 설정에 추가 해주어야한다. vi ~/.zshrc를 이용해서 편집창에 들어가도록한다. <br>다음 아래의 코드를 추가해 준다.

```c
export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```
설정을 추가한 후에 터미널 창을 재실행 하거나 `source ~/.zshrc`를 이용하여 터미널 창에 적용시켜준다.

## 파이썬 관련 유틸리티 설치
셀에서 방향키 관련 이슈를 해결하기 위해 관련 유틸리티를 설치 해주어야 한다.
<br>아래 코드를 사용해서 설치해 하도록 한다.
```c
brew install readline xz
```
## 파이썬 설치
유틸리티 설치까지 완료 했다면, 이제 파이썬을 설치해 주어야 한다. pyenv를 이용해서 파이썬을 설치해 주자.

```c
pyenv install 3.6.4
```
## pyenv사용하기
이제 파이썬을 사용할 준비가 되었다. pyenv를 이용해서 가상환경을 생성해 주자.

```c
pyenv virtulenv 3.6.4 name
```
자신의 버전을 입력하고 이름을 정한후 입력하면 된다.
이제 사용할 폴더로 이동 해야한다.

## 사용할 폴더 지정

```c
cd project
mkdir Python
cd python
```
폴더로 이동을 했다면 이제 로컬에 가상환경을 지정해주어야 한다.
```c
pyenv local name
```
가상환경을 지우고 싶다면 uninstall 정한이름 을 입력하면 된다.

## iPython
iPython은 기본 파이썬 셸보다 다양한 기능을 제공해 준다.

```c
pip install iptython
```
설치를 완료한 후 터미널 창에서 ipython을 실행해주면 된다.
<br>이것으로 mac에서 파이썬을 사용할 준비가 끝났다.
<br>
다음번에는 학원에서 배운 파이썬 강의를 복습해보자.
