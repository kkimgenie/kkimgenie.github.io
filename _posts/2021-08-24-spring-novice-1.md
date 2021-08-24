---
layout: post
title: "install, 프로젝트 환경설정, 스프링 웹 개발 기초"
tags: [spring]
comments: true
# hidden: true
---

#### Spring ?
Java 플랫폼을 위한 오픈소스 애플리케이션 프레임워크
동적 웹사이트를 개발하기 위해 여러가지 서비스를 제공

#### 간단한 웹 애플리케이션 개발
* 스프링 프로젝트 생성
* 스프링 부트로 웹 서버 실행
* 회원 도메인 개발
* 웹 MVC 개발
* DB연동 - JDBC, JPA, 스프링 데이터 JPA
* 테스트케이스 작성

#### 사전 준비물
* [Java JDK 11 설치](https://www.oracle.com/java/technologies/javase-downloads.html)
* IDE: [IntelliJ](https://www.jetbrains.com/ko-kr/idea/download/#section=windows) 또는 Eclipse 설치


#### 프로젝트 환경설정

* https://start.spring.io
* maven / gradle : 필요한 라이브러리를 땡겨오고, 빌드 라이프사이클 관리해주는 툴
* @SpringBootApplication : 톰캣 서버를 내장하고 있어서 스프링부트가 같이 올라옴
* 