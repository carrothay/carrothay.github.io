---
layout: post
title: "[Spring]Spring fundamentals 04"
category: spring
tags: spring
sitemap: false
---
# Spring fundamentals - 4

## 3. Springboot 동작원리(2)

### (4) FrontController 패턴

---

- 웹서버(아파치로)를 통해 요청이(request) 들어올 때, 최초 요청이 URI 혹은 자바파일이면 이 요청은 톰켓으로 보내진다. 톰켓이 request(요청데이터)와 response(응답데이터)객체를 memory에 자동생성한다.
- web.xml에서 .do(특정주소)는 모두 FrontController로 보낸다. 해당 자원에 접근하기 위해 request를 보낸다. 이 때, 새로운 요청데이터 객체를 생성해야 하는데, 기존의 request를 덮어씌우게 된다. 이를 방지하기 위해 나온것이 RequestDispatcher이다.
- 최초 앞단에서 web.xml을 대신(다 정의하기에 너무 복잡해서) request를 받아서 필요한 클래스에 넘겨준다. 이때 새로운 요청이 생기기 때문에 request와 response가 새롭게 new될 수 있다. 그래서 아래의 RequestDispatcher가 필요하다.

---

### (5) RequestDispatcher

---

- 필요한 클래스 요청이 도달했을 때 FrontController에 도착한 request와 response를 그대로 유지시켜준다. (기존 데이터를 들고 페이지를 이동할 수 있는 기법)

---

### (6) DispatcherServlet

---

- 스프링에서는 (4)FrontController 패턴을 직접 짜거나, (5)RequestDispatcher를 직접 구현할 필요가 없다. DispatcherServlet은 FrontController pattern + RequestDispatcher 이다. (JSP에서는 직접 구현해야 한다.)
- DispatcherServlet이 자동생성될 때 수많은 객체가 생성(IoC)된다. 보통 필터들(또는 컨트롤러, 리포지토리, 서비스, 컴포넌트, 빈 등)이다. 해당 필터들은 내가 직접 등록할 수도 있고 기본적으로 필요한 필터들은 자동 등록 되어진다.

---

### (7) Spring Container

---

- DispatcherServlet에 의해 생성되는 수많은 객체들은 어디서 관리될까?
- 컨테이너란, 특정 객체의 생성과 관리를 담당하며 객체 운용에 필요한 다양한 기능을 제공한다. 스프링 컨테이너는 <bean> 저장소에 해당하는 XML 설정 파일을 참조하여 <bean>의 생명주기를 관리하고 여러가지 서비스를 제공한다.
- request를 받은 web.xml 에서 DispatcherServlet으로 보내지기 전, ContextLoaderListerner가 root-applicationContext를 읽는다.

---

1.__ApplicationContext__

DispatcherServlet이 컴포넌트 스캔할 때 객체들이 ApplicationContext에 등록된다. 이것을 IoC라 하며 스프링이 직접 객체를 관리하고 필요할 시 DI를 이용한다. ApplicationContext는 싱글톤으로 관리되기 때문에 어디서 접근하든 동일한 객체를 보장한다.

ApplicationContext에는 두 가지 종류가 있다.

    1) servlet-applicationContext

웹 관련 어노테이션 스캔(메모리에 로딩) Controller, RestController
객체 생성 ViewResolver, Interceptor, MultipartResolver 등
DispatcherServlet에 의해 실행됨

    2) root-applicationContext

기타 어노테이션 스캔 Service, Repository 등
DB관련 객체 생성
ContextLoaderListener에 의해 실행됨 - 이것은 web.xml이 실행해주는 파일로, servlet-applicationContext보다 먼저 로드됨. 따라서 servlet-applicationContext는 root-applicationContext가 로드한 객체를 참조할 수 있지만 그 반대는 불가능함

![Untitled](https://user-images.githubusercontent.com/85178486/187167443-66f8d709-d37f-407a-89fa-985e255861cc.png){:.lead width="800" height="100" loading="lazy"}

1. 웹 애플리케이션 실행하면 Tomcat(WAS)에 의해 web.xml loading
2. web.xml에 등록되어있는 ContextLoaderListern(Java Class) 생성. ContextLoaderListener class는 ServletContextListern 인터페이스를 구현하고 있으며, ApplicationContext를 생성하는 역할이다.
3. 생성된 ContextLoaderListerner는 root-context.xml을 loading (보통 DB와 관련)
4. root-context.xml에 등록되어 있는 Spring Container구동. 이 때 개발자가 작성한 비즈니스 로직에 대한 부분과 DAO, VO 객체들 생성
5. 클라이언트의 웹 애플리케이션 요청
6. DispatcherServlet(Servlet)이 생성됨. 이는 FrontController의 역할을 수행하며, 클라이언트 요청메시지를 분석하여 해당되는 PageController에게 전달하고 응답을 받아 어떤 응답을 할지 결정한다. 실질적인 작업은 PageController에서 이루어지며, 이런 클래스들을 HandlerMapping, ViewResolver class 라고 한다.
7. DispatcherServlet은 servlet-context.xml을 loading한다.
8. 두 번째 Spring Container가 구동되며 응답에 맞는 PageController들이 동작한다. 이 때 첫번째 Spring Container가 구동되면서 생성된 DAO, VO, ServiceImpl 클래스들과 협업하여 알맞은 작업을 처리하게 된다.
{:.figcaption}



2.__BeanFactory__

@Bean 어노테이션으로 메소드를 통하여 메모리에 필요한 객체를 로드할 수 있다. 클라이언트의 요청이 있을때만 객체를 생성한다(lazy loading.)a

---

출처. 메타코딩 YouTube, [https://asfirstalways.tistory.com/334](https://asfirstalways.tistory.com/334)