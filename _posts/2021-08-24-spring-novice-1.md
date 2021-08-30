---
layout: post
title: "install, 프로젝트 환경설정, 스프링 웹 개발 기초"
tags: [spring]
comments: true
# hidden: true
---

##### Spring ?
Java 플랫폼을 위한 오픈소스 애플리케이션 프레임워크   
동적 웹사이트를 개발하기 위해 여러가지 서비스를 제공

##### Goal
* 스프링 프로젝트 생성
* 스프링 부트로 웹 서버 실행
* 회원 도메인 개발
* 웹 MVC 개발
* DB연동 - JDBC, JPA, 스프링 데이터 JPA
* 테스트케이스 작성

##### 프로젝트 환경설정

*사전준비물*
* [Java JDK 11 설치](https://www.oracle.com/java/technologies/javase-downloads.html)
* IDE: [IntelliJ](https://www.jetbrains.com/ko-kr/idea/download/#section=windows) 또는 Eclipse 설치

*환경설정*
* https://start.spring.io
  *  Project : Gradle
  *  Springboot : 정식버전(영어가 붙어있지 않은 버전이 정식 버전)
  *  Lang : Java
  *  Packaging : Jar
  *  Java : 11
* maven / gradle : 필요한 라이브러리를 땡겨오고, 의존관계를 관리. 빌드 라이프사이클 관리 툴
* @SpringBootApplication : 톰캣 서버를 내장하고 있어서 스프링부트가 같이 올라옴
* 실행속도 높이기 : Preference -> Build -> Build Tools -> Gradle : Build and run (Gradle -> IntelliJ IDEA)

issue/ java: warning: source release 11 requires target release 11
sol/ https://hothoony.tistory.com/1105

q/ jar, war 차이?
a/

*라이브러리 살펴보기*
스프링 부트 라이브러리
* spring-boot-starter-web
  * spring-boot-starter-tomcat: 톰캣 (웹서버)
  * spring-webmvc: 스프링 웹 MVC
* spring-boot-starter-thymeleaf: 타임리프 템플릿 엔진(View)
* spring-boot-starter(공통): 스프링 부트 + 스프링 코어 + 로깅
  * spring-boot
    * spring-core
* spring-boot-starter-logging
  * logback, slf4j

테스트 라이브러리
* spring-boot-starter-test
  * junit: 테스트 프레임워크
  * mockito: 목 라이브러리
  * assertj: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
  * spring-test: 스프링 통합 테스트 지원


Welcome Page
* static/index.html
* @GetMapping : Http GET Method
  * @GetMapping("hello") : 새로 생긴 url이 hello
  * 해당 함수 리턴 값이 resources/templates 폴더 내 일치하는 html을 찾아가서 렌더링 하라고 처리

빌드 및 실행
* Linux
  * ./gradle build
  * cd build/libs
  * java -jar hello-spring-0.0.1-SNAPSHOT.jar   
* Windows
  * ./gradlew -> gradlew.bat
  * gradlew (gradlew.bat을 실행하기 위해서)
  * gradlew build


##### 스프링 웹 개발 기초
*정적 컨텐츠*
* static/hello-static.html

*MVC와 템플릿 엔진*
* thymeleaf 장점 : 절대경로로 서버없이 껍데기 확인가능
* localhost:8080/hello-mvc?name=spring!!!!!! : controller 중 hello-mvc라는 메소드의 name 인자에 spring!!!!!! 값을 전달(변환)

*API*
* @ResponseBody : 응답부에 return 을 직접 넘겨줌. viewResolver 대신에 HttpMessageConverter 동작
* localhost:8080/hello-string?name=wow : wow 문자열 그대로 넘겨줌(html코드가 따로 없음)
* json : key - value 구조
* 문자처리는 'StringHttpMessageConverter'
* 객체처리는 'MappingJackson2HttpMessageConverter'
* 기타 처리는 여러'HttpMessgageConverter'가 기본으로 등록돼 있음


![20210831_003434](https://user-images.githubusercontent.com/89087636/131365043-af4ca916-ef69-4b79-bdf4-3d2761136aff.png)
