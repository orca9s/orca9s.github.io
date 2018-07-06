---
title: Docker
description: <center> Docker Nginx </center>
categories:
 - Docker
tags:
---

# Nginx - uWSGI - Django

**Web Server** <-> **WSGI** <-> **Web Application**

## Nginx

### 웹 서버 설정

```
/etc/nginx/nginx.conf
```
- `user`:nginx 프로세스를 실행할 유저
- `daemon` : `off`로 나타탤 시, background가 아닌 foreground프로세스로 실행
	- `nginx -g "daemon off;` <- 이것과 같은 효과가 됨

### 운영가능한 가상서버(Virtual host)

A, B, C, D, E 5개의 서버정보가 있다면, `sites-available`폴더에 들어있음

```
/etc/nginx/sites-available/*
```

### 실제 운용중인 가상서버
`sites-available`폴더에 있는 파일을 링크해서 사용

```
/etc/nginx/sites-enableed/<링크파일>
```

링크 명령어

```
ln -s <소스> <타겟>
```

## Nginx와 uWSGI

**Web Server <-> WSGI**

서로간에 `Unix socket`을 사용해서 연결 `/tmp/app.sock`을 사용 이떄, `uWSGI`를 실행하는 프로세스들이 모두 해당 소켓파일에 접근할 권한이 있어야함.

(실습때는 `uWSGI`와 `Ngnix`모두 `root`계정을 사용해서 해결)

### Nginx에서

자신의 가상서버 설정 (`server`블록)의 `location`에서, `uswgi_pass`부분에 유닉스 소켓 프로토콜과 위치(`unix://`, `/tmp/app.sock`)을 지정

### uWSGI에서

uWSGI를 실행하기 위한 설정파일 (`uwsgi.ini`)의 `socket`항목에 `/tmp/app.sock`을 지정

## uWSGI
uWSGI 설정은 `<파일명>`.ini 파일에 `ini`방식으로 설정을 기술.

- `chdir`: 웹 애플리케이션의 파이썬 프로젝트 루트 폴더
- `home`: 실행할 파이썬 가상환경 / 파이썬 인터프리터의 위치
- `module`:웹 애플리케이션에서 `WSGI`프레임우커으오의 연결을 기술한 파이썬 모듈

### nginx error 확인

`/var/log/nginx`에서 아래 코드 사용시 nginx의 에러 내용을 확인 할 수 있다.

```
nginx tail -f /var/log/nginx/error.log
```

## uWSGI와 Django

**WSGI <-> Application**

서로간의 견결에 웹 애플리케이션(Django)의 `config.wsgi`모듈 (`app/config/wsgi.py`)