---
title: Django Aws
description: <center> Django AWS 세팅하기 </center>
categories:
 - Django
tags:
---


## 장고에서 runserver 실행 했을때

```
Browser -> localhost(127.0.0.1) -> runserver -> Django
```

## AWS를 사용할때

```
Browser -> AWS -> runserver -> Django
```
소스코드가 AWS에 올라가 있어야 한다. 물리적으로 컴퓨터 한대를 사용할 수 있지만, 클라우드 서비스를 쓸때는 클라우드 서비스에서 지원하는 자원을 할당받아서 사용한다. 할당받아서 사용하는 자원은 EC2이다.

EC2는 클라우드에서 안전하고 크기 조정이 가능한 컴퓨팅 파워를 제공하는 웹 서비스 이다.

인스턴스 개수 1개가  프리티어 제한 인스턴스 개수가 늘어나면 비용이 추가 된다. 


### 다운받은 키페어를 숨김 모드로 ssh로 이동시키기
```
mv ~/Downloads/fc-8th.pen ~/.ssh
```
### 만들어둔 인스턴스서버로 이동하기

```
ssh -i ~/.ssh/key.pem ubuntu@퍼블릭 DNS(IPv4)
```

### 읽기모드 400으로 바꿔주기
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

### 우분투 업데이트

```
sudo apt-get update
```

의존성 검사하며 설치하기

```
sudo apt-get dist-upgrade
```
aws를 통해 들어간 우분투는 16.04버전으로 옛날 버전이기 때문에 그냥 사용하기엔 어렵다. 그래서 위의 코드를 이용해서 업데이트를 먼저 해주어야 한다.

### AWS에 zsh설치해주기
기본쉘 보다는 화려한 테마와 편리한 기능을 가진 Oh My Zsh을 사용하려면 우선 zsh를 설치해주어야한다. 아래의 코드를 이용해서 zsh를 설치하자!

```
sudo apt-get install zsh
```
### AWS에 oh-my-zsh설치하기
우리가 사용하는 터미널에는 이미 zsh과 oh-my-zsh을 설치해서 사용하는 사람이 대부분 일 것이다. 하지만 AWS에서도 이 환경을 사용하고 싶으면 새로 설치해 주어야 한다.


oh-my-zsh설치해주기 아래의 코드를 입력하자.

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

```
oh-my-zsh을 설치할때 우분투의 패스워드를 물어보는 경우가 발생하는데 control + c 를 사용해서 종료해주고 루트 유저로 전환 해주어야 한다.
아래의 코드를 터미널에 입력해주자

```
sudo su
```
이렇게 하면 루트 폴더에 들어가게 된다. 이제 다시 위의 설치코드를 사용해서oh-my-zsh을 설치해 주도록 하자

### ubuntu유저의 shell을 변경
이제 zsh설치가 완료되었으니 shell을 zsh로 변경해 주어야 한다. 아래의 코드를 작성하자 작은 따옴표가 아니라 키패드 1옆의 ~표시 키이니 주의 해서 작성하도록 하자.

```
sudo su 를 이용해 루트 환경에서
```

```
chsh ubuntu -s `which zsh`
```

아직 zsh로 완전히 바뀐게 아니다. vi .zshrc로 이동해서 두번째 줄 주석을 해제 해주어야 한다.(아래부분을 주석해제를 해주면 된다.)
 
```
export PATH=$HOME/bin:/usr/local/bin:$PATH
```