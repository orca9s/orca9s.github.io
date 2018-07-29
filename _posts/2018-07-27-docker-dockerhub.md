---
title: dockerhub사용하기
description: <center> dockerhub에 base만들기 </center>
categories:
 - docker
tags:
---

### dockerhub
dockerhub는 github과 비슷하지만 여기선 base이미지 등등을 미리 만들어서 올려놓고 사용할 수 있다.

우선 docker에 가입을하고 `hub.docker.com`으로 접속하여 Create Repository를 사용해서 저장소를 생성할 수 있다.

docker이미지를 저장소에 올리기 위해선 우선 tag를 달아 주어야 한다.

```
docker tag 원본이 되는 이미지 계정이름/저장소 이름

docker tag eb-docker:base oraca9s/fc-8th-eb-docker:base
```

이렇게 만들면 docker images를 입력하면
tag는 base인데 이름이 다른 base가 하나 더 생긴다.

만들고 난 후 

```
docker push orca9s/fc-8th-eb-docker:base
```
이렇게 입력하면 자신이 만든 저장소로 올라가게 된다.

이제 base이미지는 매번 코드를 치지 않고 dockerhub에서 가져다 사용할 수 있다. 다만 Pipfile에 수정사항이 생기면 base이미지도 항상 수정해서 올려주어야 한다.