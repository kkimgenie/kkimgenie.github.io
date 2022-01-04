---
layout: post
title: "회원 관리 예제 - 백엔드 개발"
tags: [spring]
comments: true
# hidden: true
---
## 단축키
* Alt + Insert : 디렉터리, 패키지, 클래스 등 생성목록 보기
* Alt + 1 : 프로젝트 창 포커스
* Esc : 에디터 포커스
* Ctrl + E : 최근 실행파일 확인
* Ctrl + Shift + Enter : 하단줄로 이동
* sout + Tab : ``` System.out.println(); ```
* Shift + F6 : 변수명 rename 
* Ctrl + Alt + M : Extract method 
* Ctrl + Alt + v : 변수 추출하기
* Ctrl + Alt + p : 파라미터 추출하기  
<br>

## 회원 관리 예제 - 백엔드 개발  

#### 회원 도메인과 리포지토리 만들기  
일반적인 웹 애플리케이션 계층 구조  
![20210908_235334](https://user-images.githubusercontent.com/89087636/132533163-bc5c065c-5b64-41e4-8259-2e32438c9df4.png)

* 컨트롤러 : 웹MVC의 컨트롤러 역할
* 서비스 : 핵심 비즈니스 로직 구현
* 리포지토리 : DB접근, 도메인 객체를 DB에 저장하고 관리
* 도메인 : 비즈니스 도메인 객체, 예) 회원, 주문, 쿠폰 등등 주로 DB에 저장하고 관리됨
<br>
* 메모리 구현체를 구성할 때 여기서는 동시성 문제가 고려되어 있지 않음, 실무에서는 공유되는 변수일 경우 ConcurrentHashMap, AtomicLong 사용 고려  
<br>
* Optinal : null을 optional로 반환
```java
Optional<Member> findById(Long id);
Optional<Member> findByName(String name);
``` 
<br>
**q/** Long, long 차이?  
**a/**
<br>  

#### 회원 리포지토리 테스트 케이스 작성    
개발한 기능을 테스트 할 때 자바의 main 메서드를 통해서 실행하거나, 웹 애플리케이션의
컨트롤러를 통해서 해당 기능을 실행한다. 이는 오래걸리고 반복하기 어렵다는 단점이 있어서 JUnit이라는 프레임워크로 해결한다.

* @Test 를 테스트하려는 메서드 상단에 적으면 JUnit을 임포트해와서 해당 메서드만 또는 클래스 단위로 테스트 가능하다
* 결과 값을 매번 출력해서 확인하는게 아니라 하기 Assertions로 확인 가능  
  ```java
  Assertions.assertEquals(기대하는 값, 실제 값);

  Assertions.assertEquals(member, result);
  // 하기 문법이 더 편해서 많이 사용
  org.assertj.core.api.Assertions.assertThat(member).isEqualTo(result);

  // static import를 사용하면 더 편하게 사용 가능
  import static org.assertj.core.api.Assertions.*;
  assertThat(member).isEqualTo(result);
  ```
* 클래스 단위로 테스트할 때 메서드 테스트 순서는 랜덤으로 수행된다. -> 그렇기 때문에 각각 독립적으로 실행되어야하며 끝나고 데이터 클리어 해주는 부분이 필요하다. (@AfterEach를 사용하면 각 테스트가
종료될 때 마다 이 기능을 실행한다) 
```java
@AfterEach
 public void afterEach() {
    repository.clearStore();
 }
```
* TDD(Test Driven Development) : 테스트를 먼저 만들고 구현클래스를 만드는 방식   

#### 회원 서비스 개발  


#### 회원 서비스 테스트  
* 테스트 클래스 쉽게 만드는 방법 : Class 명 위에서 Ctrl + Shift + T
* 테스트 코드니까 함수명은 한글이어도 됨
* @BeforeEach : 각 테스트 실행 전에 호출된다. 테스트가 서로 영향이 없도록 항상 새로운 객체를 생성하고,
의존관계도 새로 맺어준다 -> DI(Dependency Injection)