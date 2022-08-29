---
layout: post
title: "[Spring]Spring fundamentals 03"
category: spring
tags: spring
sitemap: false
---
# Spring fundamentals - 3

## 3. Springboot 동작원리

### (1) 내장 톰켓을 가진다.

---

- **Socket통신**: 운영체제가 가지고 있는 것. 스레드가 계속 늘어나 부하가 크지만 끊기지 않으니 한 번 연결되면 계속 통신이 가능 가능하다.
    - 스레드: 시간을 timeslice해서 동시에 동작하는 것처럼 보일 수 있게 하는 방식
- **http통신**: 소켓을 기반으로 만든 문서전달통신. stateless 방식을 사용한다. 부하가 적지만 연결될 때 마다 새로운 사용자로 인식한다.
- 이런 단점들을 보완하면서 web server가 만들어졌다.

---

### 웹서버(WEB)

---

- request할 때는 IP주소와 URL이 필요하다. 갑은 을의 IP주소를 토대로 response한다(응답해주는 자원을 static자원 이라고 한다.) http방식은 연결이 끊기므로 을과 계속 연결되어 있기 위해서는 socket이 필요하다.
- 웹 브라우저 클라이언트로부터 HTTP요청을 받고, html문서 등을 응답하는 프로그램
- e.g. Apache web server

---

### 톰켓이란?(WAS, Web Application Server)

---

- Apache web server만 사용한다면 웹 브라우저가 jsp(java)로 된 파일을 읽을 수 없어서 톰켓을 같이 사용한다. 톰켓은 요청받은 자바 코드를 컴파일하고 html로 변환하여 돌려주는 작업을 한다.
- WAS란 웹 서버 + 웹 컨테이너(JSP와 Servlet구동 환경 제공)로서 인터넷 상에서 http를 통해 사용자 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)이다. 웹 애플리케이션 서버는 동적 서버 콘텐츠를 수행하는 것으로 일반적인 웹서버와 구별이 되며, 주로 데이터베이스 서버와 같이 수행이 된다.
- 웹 컨테이너는 클라이언트의 요청이 있을 때 내부의 프로그램을 통해 결과를 만들어내고 이것을 응답해준다.

---

### WEB vs WAS

---

- Web Container의 유무
- WEB: html 문서 등 정적 컨텐츠 처리(http protocol을 통해 읽힐 수 있는 문서)
- WAS: asp, php, jsp등 개발 언어를 읽고 처리하여 동적 컨텐츠, 웹 응용 프로그램 서비스를 처리

---

### (2) Servlet Container(톰켓)

---

- 서블릿 객체는 하나이다. 서블릿 컨테이너(톰켓)는 클라이언트가 요청할 시 스레드가 만들어지면서 공유하여 사용한다. 최종적으로 톰켓에서 Service(HttpServletRequest, HttpServletResponse)객체가 만들어진다.
- url: 자원 접근, uri: 식별자를 통해 접근, 특정한 파일 요청을 할 수 없고 요청시에는 무조건 자바를 거쳐야 한다. 스프링은 uri 접근만 지원한다. ⇒ 즉, 무조건 톰켓을 거쳐야 하는 구조이다.
- 요청이 들어올 때마다 새로운 스레드를 만들지만 서버 성능에 맞는 최대 생성 가능한 스레드 수가 정해져 있고 각 스레드를 재사용할 수 있다.

---

### (3) web.xml

---

- web.xml의 기능(문지기가 사용하는 관리자가 준 문서)
*. ServletContext의 초기 파라미터 설정
   - 한 번 설정해두면 어디서든 사용할 수 있음
*. Session의 유효시간 설정
   - 인증을 통해 들어와서 머무를 수 있는 유효시간
*. Servlet/JSP에 대한 정의 및 mapping
   - 방문자가 요청한 식별자의 위치를 안내해줌
*. Mime Type mapping
   - 방문자가 들고 방문한 데이터타입을 알아내는 것. 아무것도 안 들고 왔으면 GET방식(select)
*. Welcome File list
   - 목적지없이 방문한 사용자를 어디로 보낼지 설정
*. Error pages 처리
*. 리스너/필터 설정
   - 필터: 방문자의 신분 확인
   - 리스너: 새로운 대리인으로서 문지기와 동시에 방문자를 확인하여 특정 사용자를 찾아 데려감
*. 보안
- 여기서 Servlet/JSP mapping시(web.xml 직접 매핑 or @WebServlet 어노테이션 사용) 에 모든 클래스에 매핑을 적용시키기에는 코드가 너무 복잡해지기 때문에 FrontController pattern을 이용함

---

 

출처. [https://helloworld-88.tistory.com/71](https://helloworld-88.tistory.com/71) , 메타코딩 YouTube