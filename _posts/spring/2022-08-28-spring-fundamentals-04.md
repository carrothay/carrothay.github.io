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

출처. 메타코딩 YouTube