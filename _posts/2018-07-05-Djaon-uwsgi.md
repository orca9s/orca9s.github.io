---
title: Django uWSGI
description: <center> Django, ssh, uWSGI </center>
categories:
 - Django
tags:
---

## .sh파일 만들어주기
AWS세팅은 끝났지만 파일을 바꿔서 올리거나 다시 실행시키고 싶을때 코드를 일일이 하나씩 입력해서 실행시키기에는 매우 번거롭다. 그래서 .sh파일을 만들어 주게 되면 쉽게 실행시킬 수 있다. 

## aws서버 안에서 서버가 돌아가고 있는지 확인
aws서버 안에서 서버가 이미 돌아가고 있는지 확인하기 위해선 아래의 코드를 입력하면 된다.

```python
ps -ax | grep runserver
```
현재 실행되고 있는 서버의 PID만 검색 할 수 있다. 아래의 코드를 사용하면 된다.

```python
ps -ax | grep runserver | awk '{print$1}'
```

실행중이 서버를 종료시킬 수 있는 코드

```python
kill $(ps -ax | grep runsever | awk '{print$1}')
```

##  플러그인 설치하기
플러그인은 따로 설치 하는게 아니라 `deploy.sh` 파일을 생성하게 되면 자동으로 설치하게 된다.

## 권한 수정하기(permission denied오류)
처음 sh파일을 만들고 실행시키면 권한이 없다는 permission denied오류가 발생하기 때문에 권한을 수정 해주어야 한다. 

```python
chmod 755 test.sh
* test는 본인의 파일명으로 하면 된다.
```

### 쉘명령어 사용하기
아래의 코드를 입력 하면 .sh파일에서 쉘 명령어를 사용할 수 있다.

```python
#!/usr/bin/env bash
```

이제 쉘 파이참에서 쉘 명령어를 사용할 수 있게 되었으니 파일에 하나씩 추가해주어야 한다. 

```python
IDENTITY_FILE="자신의 키페어 위치"
USER="ubuntu(사용자명)"
HOST="자신의 aws DNS서버 주소"
PROJECT_DIR="프로젝트 파일 주소"
SERVER_DIR="서버의 프로젝트 파일 주소"
```

### ssh로 서버에 접속하는 명령어

```python
CMD_CONNECT="ssh -i ${IDENTITY_FILE} ${USER}@${HOST}"
echo "Start deploy"
```
여기서 `echo`는 `print`와 같은 역할을 한다. 실행이 제대로 되는지 확인하기 위해 Start deploy를 써준다. 중간중간 작동이 되는지 확인하기 위해 기능별로 출력을 시키도록 하자.

### 서버에서 실행중이던 runserver 프로세스들을 모두 종료
우선 서버에서 기존에 실행중이던 runserver들을  모두 종료해주어야한다.

```python
${CMD_CONNECT} "pkill -9 -ef runserver"
echo "- Kill runserver processes"
```

### 서버의 파일을 지움
기존에 서버에 있던 파일들을 모두 지워 주어야 한다.

```python
${CMD_CONNECT} rm -rf ${SERVER_DIR}
echo "- Delete server files"
```

### 서버에 project파일을 다시 업로드 시키기
이제 서버에 있던 파일들을 지웠으니 다시 django에 작성한 project파일들을 업로드 시켜주면 된다.

```python
scp -q -i ${IDENTITY_FILE} -r ${PROJECT_DIR} ${USER}@${HOST}:${SERVER_DIR}
echo "- Upload files"
```

### 서버 접속 후 SEVER_DIR로 이동,  pipenv --venv로 가상환경의 경로 가져오기

```python
VENV_PATH=$(${CMD_CONNECT} "cd ${SERVER_DIR} && pipenv --venv")
echo $VENV_PATH
```

### 가상환경의 경로에 /bin/python을 붙여 서버에서 사용하는 python의 경로 만들기

```python
PYTHON_PATH="${VENV_PATH}/bin/python"
echo $PYTHON_PATH
```

### runserver를 background에서 실행해주는 커맨드 (nohup)

```python
RUNSERVER_CMD="nohup ${PYTHON_PATH} manage.py runserver 0:8000 &>/dev/null &"
echo $RUNSERVER_CMD
```

### 서버 접속 후, project의 'app'폴더까지 이동한 후 runserver명령어를 실행

```python
${CMD_CONNECT} "cd ${SERVER_DIR}/app && ${RUNSERVER_CMD}"
echo "End"
echo "Deploy complete"
```
이렇게 파일을 만들어주면 이제 번거로운 작업 없이 만든파일만 실행시켜주면 위의 작업들을 한번에 수행할 수 있다.

## User가 업로드한 파일과 DB

```python
Browser > runserver > static > 

Browswer > webserver > File (또는) [Django <-> DB]
```

### STATIC
static파일로 설정하면 요청이 들어 왔을때 웹서버에서 django까지 들어갈 필요 없이 static속성이면 요청 받은 파일을 바로 넘겨준다. static속성이 아니라면 django로 넘겨 처리하게 된다. 이렇게 하는 이유는 요청받은 파일들을 돌려주는게 생각보다 큰 작업이기 때문에 매번 django로 넘겨서 처리하게 되면 낭비가 너무 심하고 성능향상을 위해서 static파일은 django를 거치지 않는것이 좋다.

### STATIC설정하기
static으로 설정하기 위해서는 우선 settings.py에 몇가지 코드를 추가 해주어야 한다. 

```python
ROOT_DIR = os.path.diname(BASE_DIR)
STATIC_DIR = os.path.join(BASE_DIR, 'static')
```
Static

```python
STATICFILES_DIRS = [
    STATIC_DIR,
]
```
1./static/ -> STATIC_ROOT 경로에서 파일을 리턴하도록 설정
2.그 외 URL요청은 -> Django가 처리 후 Response하도록

## uWSGI
작동원리

```
- runserver
Browser -> EC2 -> runserver -> Django

배포를 할 때 갖춰야 할 요소
- WebServer, WSGI
Browswer -> EC2 -> WebServer -> (static)       -> STATIC_ROOT
                                                          (dynamic) -> WSGI -> Django


- runserver
Browser -> EC2                                        -> Django(runserver:8000)

- uWSGI
Browser -> EC2                   -> uWSGI:8000      -> Django

- Nginx, uWSGI
Browser -> EC2 -> Ngnix   -> uWSGI:80     -> DJango
```

### uWSGI 실행방법
uWSGI는 python WSGI서버중에 한가지 이다. python WSGI를 위해서 처음 개발되었지만, 더 많은 plugin을 지원한다.

우선 uwsgi를 설치해주어야 한다.

```python
pipenv install uwsgi
```

uwsgi로 작동하는 프로세스들을 삭제하는 코드.

```python
kill -9 $(lsof -t -i:8000)
```
서버에 띄우는 과정 - 개념설명

```python
- uWSGI
Browser -> EC2                   -> uWSGI:8000      -> Django
```

### uwsgi로 runserver실행하기
 
```python
--http :8000 \ #8000번 포트로 접속
--home /home/shape/.local/share/virtualenvs/ec2-deploy-owTGTtW1 \
--chdir /home/shape/projects/deploy/ec2-deploy/app \
--module config.wsgi
```

여기서 `http`는 8000번 포트로 접속한다는 뜻이다.`home`은 자신의 가상환경이 있는 위치이다. `chdir`은 위치를 자신이 있는 위치로 이동시킨다는 소리이다.`module`은 이동시킨 위치 안의 config안쪽에 있는 wsgi를 말한다.

## uwsgi 실행파일 만들어주기
위에 적힌 코드들을 외워서 사용하기란 어렵다. 그래서 코드들을 한곳에 묶어서 실행시킬 수 있다.
일딴 `app`폴더 밖에 `.config`폴더를 만들어 준다. 그후 `파일명.ini`로 된 파일을 생성해준다. pycharm 프로 버전의 경우 ini plugin이 기본적으로 설치되어 있는 경우도 있지만 커뮤니티 버전의 경우 설치가 안되어 있는 경우가 많다. 환경설정에서 plugin에 ini로 검색하면 ini4ldea라는 플러그인이 검색 되는데 이것을 설치해준다. 설치를 완료한 후에 ini확장자의 파일을 만들어 준다. 

```python
[uwsgi]
파일 상단에 이코드를 입력해 주어야 한다.
```
### 파이썬 프로젝트로 change directory
 
```python
chdir = 자신의 현재 위치 경로 
(터미널에 pwd입력시 확인가능)
```

### 가상환경 경로

```python
home = 설정한 가상환경의 경로
(pipenv --venv)입력시 확인가능
```

### chdir로 바꾼 파이썬 프로젝트에서 wsgi모듈의 경로

```python
module = config.wsgi:application
뒤에 :application이 붙는 이유는 wsgi.py에서 application이라는 변수에 get_wsgi_applicatio()함수를 할당해주었기 때문이다.
```

### http연결을 받으며, 8000번포트로 부터 받음

```python
http = :8000
```

이렇게 작성을 마친후 저장을 하고 터미널에서 실행시킬땐 가상환경에 들어간 상태에서 상위 폴더에서 아래의 코드를 실행시키면 된다. 

```python
uwsgi --ini .config/uwsgi_http.ini
```