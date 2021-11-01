---
layout: post
title: "스프링 DB 접근 기술 - 2"
tags: [spring]
comments: true
# hidden: true
---

#### JPA
* JPA는 기존의 반복 코드는 물론이고, 기본적인 SQL도 JPA가 직접 만들어서 실행
* SQL과 데이터 중심의 설계 -> 객체 중심의 설계
* 1) build.gradle 파일에 JPA, h2 데이터베이스 관련 라이브러리 추가
  2) 스프링 부트에 JPA 설정 추가
  3) JPA 엔티티 매핑
  4) JPA 회원 리포지토리
  5) 서비스 계층에 트랜잭션 추가 : JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다/ 만약 런타임 예외가 발생하면 롤백한다
  6) JPA를 사용하도록 스프링 설정 변경
<br>

#### 스프링 데이터 JPA
* 반복 개발해온 기본 CRUD 기능도 스프링 데이터 JPA가 모두 제공
* 인터페이스를 통한 기본적인 CRUD
* findByName() , findByEmail() 처럼 메서드 이름 만으로 조회 기능 제공
* 페이징 기능 자동 제공
* 복잡한 동적 쿼리는 Querydsl이라는 라이브러리를 사용
<br>


#### AOP
* AOP: Aspect Oriented Programming
* 필요한 상황?
  * 모든 메소드의 호출 시간을 측정하고 싶다면?
  * 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)
  * 회원 가입 시간, 회원 조회 시간을 측정하고 싶다면?
<br>