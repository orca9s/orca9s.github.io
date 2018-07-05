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

## AWS세팅하기
아마존 웹 서비스를 사용하기 위해선 visa나 master카드가 필요하다 회원가입시 카드 등록을 하게되면 카드가 유효한지 검사를 하기 위해 1달러가 결제 된다. 회원가입 후 

* EC2로 이동한다.
* 국가 설정이 서울로 되어 있는지 확인후 
* 인스턴스 시작
* 본인 환경에 맞는 인스턴스 설정(ubuntu 16.04)64비트
* 새로운 키 생성해서 키를 다운로드 해준다. (한번 다운받은 키는 재발급이 불가능하니 잘 보관하도록 한다.)

이제 아래의 순서대로 적용하면 된다.


### 다운받은 키페어를 숨김 모드로 ssh로 이동시키기
```python
mv ~/Downloads/fc-8th.pen ~/.ssh
```
### 만들어둔 인스턴스서버로 이동하기

```python	
ssh -i ~/.ssh/key.pem ubuntu@퍼블릭 DNS(IPv4)
```

### 읽기모드 400으로 바꿔주기
```python
chmod 400 ~/.ssh/fc-8th.pm
```

* 읽기(r):파일의 읽기권한
* 쓰기(w):파일의 쓰기권한
* 실행(x):파일의 실행권한

```python
-r--------@  1 jeonsangmin  staff   1.7K  7  3 14:54 fc-8th.pem
```

퍼미션의 사용자 지정

* 소유자: 소유자에 대한 퍼미션 지정
* 그룹: 소유그룹에 대한 퍼미션 지정
* 공개: 모든 사용자들에 대한 퍼미션 지정

### locale설정해주기
우선 locale을 설정해주어야 한다. 아래의 코드를 이용해서 locale을 설정해주자

```python
sudo vi/etc/default/locale
```
우선 편집창으로 들어가준다. 그후 아래의 코드를 추가하고 저장해주자!

```python
LANG=en_US.UTF-8
LANGUAGE=en_US.UTF-8
LC_ALL=en_US.UTF-8
```

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
위의 설정까지 완료 했다면 exit를 통해 서버에서 나간후 다시 ssh로 접속해야 적용이 완료된다.

### pip설치 및 version다운
아래의 코드를 사용해서 pip설치와 version을 다운받아야 한다.

```
sudo apt-get install python-pip
sudo python -m pip install -U pip
```

### pipenv설치하기
pyenv와 같은 다양한 버전으로 python을 실행해 볼 수 있도록 도와주는 프로그램이다. 그러나 pyenv와 다른점은 매번 requirements.txt를 갱신해줄 필요가 없이 pip file에 자동으로 저장된다. 패키지 설치도  pipenv install을 통해 간편하게 할 수 있다.

```
sudo -H pip install -U pipenv
```

### pyenv설치
프로젝트 별로 각각 맞는 다양한 버전으로 python을 실행해 볼 수 있도록 도와주는 프로그램인 pyenv를 설치해야한다. 하지만 매번 개발환경을 적어놓는 requirements.txt를 갱신해주어야 하는 번거로움이 있다.

```
curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```

설치를 완료하고 zshrc에 몇가지 코드를 추가 해주어야 한다.

```
vi .zshrc 를 이용해 편집 창으로 들어간다.
```
맨 아래줄에 아래의 코드를 추가해주면 된다.

```
export PATH="/home/ubuntu/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

#### pyenv를 위한 requirements설치
아래의 코드를 사용해서 requeirements를 설치해주자.

```
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev
```

requirements설치가 끝났다면 exit으로 나간후 다시 ssh로 접속하자.

### pyenv로 필요한 파이썬 버전 설치하기 
이제 pyenv를 이용해 필요한 파이썬 버전을 설치 해주어야 한다. 아래의 코드로 파이썬을 설치하자.

```python
pyenv install 3.6.5
```
## AWS와 django연결 하기
이제 AWS서버의 기본적인 세팅을 해주었으니 django와 연결해주어야 한다. django의 app폴더안에 config폴더의 settings.py에 코드를 추가 해주어야 한다. ALLOWED HOST부분에 아래의 코드를 추가해주자

```python
'localhost',
'127.0.0.1',
'.amazonaws.com',
```
코드를 추가했다면 이제 aws서버쪽으로 파일들을 보내주어야 한다. app폴더 밖에서 아래의 코드를 입력하자.

```python
scp -i ~/.ssh/fc-8th.pem \
-r ~/project/deploy/ec2-deploy \
ubuntu@:/home/ubuntu/project
```
위 코드에서 @뒤부터 콜론(:)표시 앞부분에는 자신의 DNS서버 주소를 입력하면 된다.

이제 다시 aws서버가 실행중인 터미널 창으로 돌아가서 서버안의 가상환경에 접속해준다 

```python
pipenv shell
```

서버안에 project폴더가 들어왔는지 확인하고 들어 왔다면 `pipenv install`을 통해 django의 환경과 같도록 만들어 준다.

### EC2보안그룹 설정하기
이제 aws홈페이지에서 자신이 실행중인 인스턴스를 선택하고 보안그룹을 추가 해주어야 한다. 보안그룹 - 인바운드 - 편집 - 규칙추가 - 유형(사용자 지정TC), 프로토콜(TCP), 포트범위(8000), 소스(위치무관) - 저장 설정을 마치고 aws서버가 실행중인 터미널에서 `./manage.py`가 있는 위치에서 아래의 코드를 실행하면 실행이 된다.

```python
./manage.py runserver 0:8000
```
이제 runserver를 시켰으니 인터넷 창에서 확인을 해야한다. 주소창에 자신의 DNS서버+8000을 입력하면 자신의 페이지로 이동하게된다. 특별한 설정이 없다면 Django프로젝트의 첫 화면이 나오면 성공이다.
