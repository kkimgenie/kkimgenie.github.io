---
layout: post
title: "스프링 빈과 의존관계, 회원 관리 예제 - 웹MVC 개발"
tags: [spring]
comments: true
# hidden: true
---


## 스프링 빈과 의존관계  
* 컴포넌트 스캔
* 자바 코드로 직접 등록

#### 컴포넌트 스캔과 자동 의존관계 설정
컨트롤러가 리포지토리를 사용할 수 있게 의존관계 준비(DI (Dependency Injection), 의존성 주입)
<br>

```java
@Controller // 스프링이 뜰 때 컨트롤러 객체를 생성해서 가지고 있음 = 컨테이너에서 빈(녹색 땅콩..)이 관리된다
public class MemberController {
    private final MemberService memberService;
    
    @Autowired // 생성자에 붙이며, 이걸 보고 memberService 를 컨테이너에 연결시켜줌
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}
```
<br>  

* ```helloController ---(@Autowired)---> memberService ---(@Autowired)---> memberRepository```  <br>
memberService 와 memberRepository 가 스프링 컨테이너에 스프링 빈으로 등록됨
<br>

* @Component 가 있으면 스프링 빈으로 자동 등록
* @Controller 컨트롤러가 스프링 빈으로 자동 등록된 이유도 컴포넌트 스캔 때문
* @Component 를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록
  * @Controller
  * @Service
  * @Repository

<br>
* 스프링은 스프링 컨테이너에 스프링 빈을 등록할 때, 기본으로 싱글톤으로 등록
<br>

#### 자바 코드로 직접 스프링 빈 등록하기

```java
@Configuration
public class SpringConfig {
    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository());
    }
    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```
* 다만 Controller는 위와 같이 관리할 수 없음
* 실무에서는 주로 정형화된 컨트롤러, 서비스, 리포지토리 같은 코드는 컴포넌트 스캔을 사용
  상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록
<br>
<br>

## 회원 관리 예제 - 웹 MVC 개발
#### 회원 웹 기능 - 홈 화면 추가
* static > index.html 아닌 templates > home.html로 메인이 불려옴 : 이유는? 컨트롤러가 정적 파일보다 우선순위가 높다
<br>

#### 회원 웹 기능 - 등록
home.html  
-> 회원가입 버튼 MemberController : ```@GetMapping(value = "/members/new")```  
-> ```return "members/createMemberForm"```  
-> createMemberForm.html : ```<form action="/members/new" method="post">```  
-> ```@PostMapping(value = "/members/new")```  
<br>

#### 회원 웹 기능 - 조회
home.html   
-> 회원목록 버튼 MemberController : ```@GetMapping(value = "/members")```  
-> ```return "members/memberList"```  
-> memberList.html : ```<tr th:each="member : ${members}">```  
위 경우가 가능한건 아래 "members"를 이름으로 List 형태로 넘겨주기 때문  
```java
List<Member> members = memberService.findMembers();
model.addAttribute("members", members);
```