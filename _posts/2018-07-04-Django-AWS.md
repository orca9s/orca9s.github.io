---
title: Django Aws
description: <center> Django AWS 세팅하기 </center>
categories:
 - Django
tags:
---


장고에서 실행 했을때

```
Browser -> localhost(127.0.0.1) -> runserver -> Django
```

AWS를 사용할때

```
Browser -> AWS -> runserver -> Django
```
소스코드가 AWS에 올라가 있어야 한다. 물리적으로 컴퓨터 한대를 사용할 수 있지만, 클라우드 서비스를 쓸때는 클라우드 서비스에서 지원하는 자원을 할당받아서 사용한다. 할당받아서 사용하는 자원은 EC2이다.

EC2는 클라우드에서 안전하고 크기 조정이 가능한 컴퓨팅 파워를 제공하는 웹 서비스 이다.

인스턴스 개수 1개가  프리티어 제한 인스턴스 개수가 늘어나면 비용이 추가 된다. 


다운받은 키페어를 숨김 모드로 ssh로 이동시키기
```
mv ~/Downloads/fc-8th.pen ~/.ssh
```

읽기모드 400으로 바꿔주기
```
chmod 400 ~/.ssh/fc-8th.pm
```

* 읽기(r):파일의 읽기권한
* 쓰기(w):파일의 쓰기권한
* 실행(x):파일의 실행권한

```
-r--------@  1 jeonsangmin  staff   1.7K  7  3 14:54 fc-8th.pem
```

퍼미션의 사용자 지정

* 소유자: 소유자에 대한 퍼미션 지정
* 그룹: 소유그룹에 대한 퍼미션 지정
* 공개: 모든 사용자들에 대한 퍼미션 지정

우분투 업데이트

```
sudo apt-get update
```

의존성 검사하며 설치하기

```
sudo apt-get dist-upgrade
```
aws를 통해 들어간 우분투는 16.04버전으로 옛날 버전이기 때문에 그냥 사용하기엔 어렵다. 그래서 위의 코드를 이용해서 업데이트를 먼저 해주어야 한다.

zsh설치해주기

```
sudo apt-get install zsh
```

oh-my-zsh설치해주기

```

```

