---
layout: post
title: "스프링 DB 접근 기술 - 1"
tags: [spring]
comments: true
# hidden: true
---

## 스프링 DB 접근 기술
* H2 데이터베이스 설치
  * 개발이나 테스트 용도로 가볍고 편리한 DB, 웹 화면 제공
* 순수 JDBC
  * JDBC : 애플리케이션 서버와 DB를 연결하는 기술
  * 20년전 개발자들이 썼던 방법..
* 스프링 JdbcTemplate
  * 순수 JDBC 보다 편리
* JPA
  * DB에 객체를 쿼리 없이 저장 가능
* 스프링 데이터 JPA
  * JPA를 더 편리하게 쓸 수 있도록 한번 감싼 것  
<br>

#### H2 데이터베이스 설치
* https://www.h2database.com
* 연결 URL
  * 첫 연결은 jdbc:h2:~/test
  * 이후부터는 jdbc:h2:tcp://localhost/~/test
  * 파일 직접접근이 아닌 소켓을 통한 접근. 그렇지 않을 경우 웹애플리케이션과 충돌 발생할 수 있음.
* Java(Long) - DB(bigint)
* 상위dir > sql > ddl.sql : ddl문 관리 목적  
<br>

#### 순수 JDBC
* build.gradle 파일에 jdbc, h2 데이터베이스 관련 라이브러리 추가
* 스프링 부트 데이터베이스 연결 설정 추가
<br>

* 연결이나 데이터를 가져올 때 하나하나 구현해야하고, 나중에 자원을 역순으로 릴리즈해줘야 함. 그렇지 않으면 데이터커넥션이 계속 쌓여서 뻑날 수 있음.
* 스프링 DI (Dependencies Injection)을 사용하면 기존 코드 수정 없이 설정만으로 구현 클래스를 변경 가능

![20211004_224238](https://user-images.githubusercontent.com/89087636/135862296-70c3a3b3-af44-4b33-8894-c8aa148782b2.png)

#### 스프링 통합 테스트
* 애플리케이션과 DB를 통합한 테스트 케이스 작성 및 테스트
* @SpringBootTest : 스프링 컨테이너와 테스트를 함께 실행한다.
* @Transactional : 테스트 케이스에 이게 있으면, 테스트 시작 전에 랜잭션을 시작하고, 테스트 완료 후에 항상 롤백한다. 이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다. -> 이전 TC 작성 시 사용했던 afterEach()가 필요없음  
<br>

#### 스프링 JdbcTemplate
* 순수 Jdbc와 동일한 환경설정
* 스프링 JdbcTemplate과 MyBatis 같은 라이브러리는 JDBC API에서 본 반복 코드를 대부분 제거해주지만 SQL은 직접 작성해야 함
* 순수 JDBC와 비교했을 때 코드양 차이가 큼.

