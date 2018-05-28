---
title: Pycharm 프로젝트 세팅
description: <center> pyenv를 사용한 PyCharm프로젝트 세팅 </center>
categories:
 - Python
tags:
---

# pycharm설치하기
pycharm 사용환경 세팅을 위해서 우선 pycharm을 설치 해주어야 한다.
<br>우선 [파이참 설치 링크](https://www.jetbrains.com/pycharm/)로 이동해서 파이참을 설치해준다. 링크에서 자신에게 맞는 os를 선택하고 설치한다. 여기서 professional버전은 유료버전이니 community버전을 이용해서 설치해주자 만약 ac.kr로 끝나는 이메일을 가지고 있다면 이메일 인증을 통한 professional버전을 무료로 사용이 가능하다.

## pyenv를 사용한 pycharm프로젝트 세팅
pycharm 프로그램을 설치했다면 이제 가상환경을 설정 해주어야 한다. 아래의 코드를 터미널 창에 입력하자.
```python
>>> take crawler
```
이제 crawler라는 폴더를 생성했다. 폴더명은 자신이 원하는대로 정하면 된다.
```python
>>> git init
```
위의 코드를 입력하고 터미널 창에 `l`을 입력하면 바뀐걸 볼 수 있을 것이다.
## gitignore파일 수정하기
[gitignore.io](https://www.gitignore.io/)링크로 들어가게 되면 창이 뜰 것이다. 거기다 `git`, `linux`, `macos`, `python`, `PyCharm+all`을 입력해서 검색 후 페이지의 모든 부분을 복사하자. 이제 터미널 창에 `vi .gitignore` 를 입력해준다. 입력 후 `vim`창으로 들어가지면 `i`를 눌러서 문서 편집 모드로 진입해주자. 문서 편집 모드로 진입했다면 앞에서 복사한 것들을 붙여넣기 해주자 붙여넣기 완료후 `ESC`키를 통해 편집모드에서 나온 후 `:wq`를 입력후 엔터를 입력하자.

## pip install requests설치하기
이제 gitignore파일 수정까지 완료했다. 이제는 터미널 창에 `pip install requests`입력하자 requests는 PyCharm에서 파싱을 할때 좀 더 편리하게 할 수 있도록 도와주는 프로그램이다.

## virtulenv 사용해서 가상환경 설정하기
앞의 설정을 모두 완료 했다면 이제 터미널 창에 `pyenv virtulenv 3.6.5 가상환경명-폴더이름`을 입력하자
```python
>>> pyenv virtulenv 3.6.5 fc-crawler
```
이제 가상환경을 설정해 주었으니 가상환경으로 들어가 보아야 한다. 터미널 창에 `pyenv local 가상환경명-폴더이름`을 입력하자
```python
pyenv local fc-crawler
```
잘 작동 한다면 터미널 창에`l`을 입력해 보면 아래와 같이 뜰 것 이다.
```python
(fc-crawler)  jeonsangmin@jeonui-MacBook-Pro > ~/project/crawler > > master > l
total 16
drwxr-xr-x   5 jeonsangmin  staff   160B  5 28 18:27 .
drwxr-xr-x  12 jeonsangmin  staff   384B  5 28 18:23 ..
drwxr-xr-x   9 jeonsangmin  staff   288B  5 28 18:27 .git
-rw-r--r--   1 jeonsangmin  staff   3.4K  5 28 18:25 .gitignore
-rw-r--r--   1 jeonsangmin  staff     9B  5 28 18:27 .python-version
```
## git 저장소에 연동하기
위의 작업들을 모두 끝마쳤다면 마지막으로 git저장소와 연동을 해주어야 한다.
```python
git remote add origin https://github.com/orca9s/crawler.git
```
터미널에 위의 코드를 입력하면 이제 사용할 준비가 모두 끝난 것이다. 저장소 주소는 자신의 주소로 입력하면 된다.
