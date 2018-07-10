---
title: Aws
description: <center> AWS잡다한 정보들 </center>
categories:
 - AWS
tags:
---


## docker지우기
```
docker rm $(docker ps -a -q)
docker rmi $(docker images -q)
```

## 인바운드 규칙
22번포트 =ssh기본

소스 0.0.0.0 = 전세계 어디에서 오든 다 받겠다.

보안그룹(EC2 Security Group)을 설정 안하면 외부에서의 연결을 전부 거부한다.

## static
deployment에서는 static을 따로 지정해주어야 한다. django에서 기본적으로 제공하는 admin안에도 static이 있기 때문에 구분하기 위해서 따로 지정해주어야 한다. `import user`와 `get_user_model`을 구분하는 것과 비슷하다.

## collect static
app폴더 바깥에 `.static`이라는 폴더를 만들고 `settings.py`에서 경로를 지정해 주어야한다. 

```
ROOT_DIR = os.path.dirname(BASE_DIR)
STATIC_ROOT = os.path.join(ROOT_DIR, '.static')
```


```
./manage.py collectstatic
```

이렇게 해주면 위에서 만든 `.static`폴더에 `admin, css, images`폴더가 생긴다 경로를 잘못 지정한 경우에 다른 곳에 폴더가 생기니 주의 하도록 하자.

이렇게 3개가 온 이유는 우리가 만들어준 `static`폴더에서 `css`폴더와 `images`폴더를 가져오고 `django`가 지원하는 admin안의 static안에 또 `admin`폴더가 존재하는데 이렇게 3개의 폴더를 우리가 만든 `.static`폴더로 오게 된다.

## debug
`runserver`를 쓰고 `debug = true`라면 `/static/`으로 요청이 오면 자동으로 `staticfile`을 가져오는 것을 실행한다. 하지만 
`debug = false` 라고 해두면 `staticfile`에 접근할 방법이 없다.

## 웹 서버
웹 서버의 주된 기능은 웹 페이지를 클라이언트로 전달하는 것이다. 주로 그림, css자바스크립트를 포함한 HTML 문서가 클라이언트로 전달된다.

대다수의 웹 서버는 ASP, PHP 등의 서버 사이드 스크립트 언어를 지원한다. 웹 서버는 정적인 파일들을 리턴해준다. 어떤 회원이 로그인 했다 라는 정보가 담긴 html같은 것을 리턴할 수 가 없다 때문에 서버 사이드 언어와 합쳐진 것 들이 많다. 즉 서버 소프트웨어의 변경 없이도 수행할 동작을 분리된 언어에 기술 할 수 있다. (django안쪽에서 동적으로 랜더링 되는 view를 만들 수 있다.)

## WSGI(Web Server Gateway Interface)
wsgi는 웹서버와 웹 애플리케이션의 인터페이스를 위한 파이썬 프레임 워크다. 인터페이스란 서로 다른 플랫폼에서 자신을 다른 플랫폼에서 사용하고자 할때 그쪽에 제공하는 기능이다.(페이스북 로그인)

웹애플리케이션(django)과 웹서버(Ngninx) nginx와 django가 동작하기 위해서 가운데서 양쪽을 중계해주는 인터페이스 이다.


### 동작 원리
Wevserver (Nginx): HTTP요청수신/응답송신(프로토콜: HTTP), 동적인 처리가 필요하면 Django로 넘겨야 하므로 WSGI사용

WSGI (uwsgi): Python application과 WebServer간의 인터페이스 (프로토콜: Unix Socket)

Python appliacation (Django): 특정 HTTP요청에 대한 동적응답 생성

ORM과 비슷한 원리로 작동한다.

### nginx.conf복사하기

```
ln -s ../common/nginx.conf .
```


### nginx실시간 로그 확인

```
docker exec 포트번호 tail -f/var/log/nginx/error.log
tail -f /var/log/nginx/access.log
```

### settings불러오기

```
from django.conf import settings
```
여기서 불러와야한다.
config에서 불러오면 인식을 못한다.