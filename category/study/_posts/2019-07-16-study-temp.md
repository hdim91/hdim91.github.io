---
layout: post
title: 1학기정리_4주차_temp
description: >
    1학기 내용정리 스터디 _ 4주차 _ SPRING
excerpt_separator: <!--more-->
---

<!--more-->

## 웹 애플리케이션 컨테이너

> **웹 애플리케이션 컨테이너** : 웹 애플리케이션이 배포되는 공간
**웹 서버** : HTML과 같은 정적 파일들을 전달해 주는 역할을 하는 서버
**웹 애플리케이션 서버** : PHP, JSP, ASP와 같은 언어들을 사용해 동적인 페이지들을 생성하는 서버

### 클래스 로더
* JVM이 클래스를 실행하기 위해 클래스 로딩해주는 역할

#### 1. 계층적인 구조
* 상위 클래스 로더에서 하위 클래스 로더를 갖는 방식
* 최상위 클래스 로더는 `부트스트랩 클래스 로더`

#### 2. 클래스 로딩 위임 가능

#### 3. 가시적인 규약
* 자식은 클래스 로딩 요청 위임을 통해 부모가 로딩한 클래스 찾을 수 있음
* 반대의 경우는 불가능

#### 4. 클래스 언로딩 불가능
* GC가 동작하거나 WAS가 재시작할 때 초기화

![study-spring-01](../img/study-spring-01.png)
|||
|:---:|:---|
Bootstrap Class Loader|JVM 런타임 실행을 위해 기반이 되는 파일 로드   </br>  `rt.jar` 파일과 연관
Extension Class Loader|자바의 최상위 객체인 `Object`를 포함한 자바 API 로드   </br> 자바 홈 폴더 하위의 ext 폴더 하위의 JAR 파일들과 연관
System Class Loader|클래스패스에 포함된 클래스 로더
User-Defined Class Loader|독립적인 영역이 필요한 WAS의 경우 사용자 정의 로더를 만들어서 사용   </br> 대부분 톰캣 설치 위치를 CATALINA_HOME 으로 지정하는 이유

## WAR 파일 ( Web Application Archive / Web Application Resource )
> 로컬 실행 프로그램은 `JAR`로 패키징하고 웹은 `WAR`로 패키징
`WAR` = 압축 파일 + 자바 관련 규약 (`WEB-INF`)

* HTML, js, Css, JSP 등 브라우저에서 보여 줘야 하는 정적 자원을 관리하기 위한 폴더

```
web Archive
└ content subdirectory
  ├ file.html
  ├ file.js
  ├ file.css
  └ WEB-INF
    ├ web.xml
    └ classes           // 1. 먼저 검색해서 로딩
      ├ file.class
      └ libs            // 2. 클래스 파일 로딩 후 JAR 파일 로드
        └ jar   
```

____________

## Servlet Lifecycle
