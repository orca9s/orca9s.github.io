---
title: Nginx와 Apache
description: <center> Apache & Nginx </center>
categories:
 - Nginx
tags:
---

## Apache와 nginx

> Apache

- 쓰레드 /프로세스 기반 구조로 요청 하나당 쓰레드 하나가 처리하는 구조
- 사용자가 많으면 많은 쓰레드 생성, 메모리 및 CPU 낭비가 심함
- 하나의 쓰레드: 하나의 클라이언트라는 구조

> nginx

- 비동기 Event-Driven기반 구조
- 다수의 연결을 효과적으로 처리가능
- 대부분의 코어 모듈이 Apache보다 적은 리소스로 더 빠르게 동작가능
- 더 작은 쓰레드로 클라이언트의 요청들을 처리가능

## nginx역할
트래픽이 많은 사이트의 확장성을 위해 설계한 비동기 이벤트 기반구조의 웹서버 소프트웨어
<br>
<br>
> 정적 파일을 처리하는 HTTP서버로서의 역할
<br>

웹서버의 역할은 HTML, CSS, Javascript, 이미지와 같은 정보를 웹 브라우저에 전송하는 역할을 한다.

>응용프로그램 서버에 요청을 보내는 리버스 프록시로서의 역할
<br>

리버스 프록시로서 역할은 클라이언트가 가짜 서버에 요청을 하면, 프록시 서버가 배후 서버(reverse server)로부터 데이터를 가져오는 역할을 한다. 여기서 프록시 서버가 `nginx` 리버스 서버가 응용프로그램 서버 `django`를 말한다.
<br>
<br>
웹 응용프로그램 서버에 리버스 프록시를 사용하는 이유는 요청에 대한 버퍼링이 있기 때문이다. 사용자가 직접 `django`에 요청을 하면 프로세스 1개가 응답 대기 상태가 되기 때문에 프록시 서버를 사용함으로 요청을 배분하게 된다.

### nginx는 비동기 처리 방식을 채택
동기: 요청이 있을때, 요청에 대한 응답을 주어야 다른 요청을 처리가능
<br>
<br>
비동기: 하나의 요청이 끝나지 않아도 다른 요청이 처리가능


