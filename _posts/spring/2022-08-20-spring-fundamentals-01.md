---
layout: post
title: "[Spring]Spring fundamentals 01"
category: spring
tags: spring
sitemap: false
---
# Spring fundamentals - 1

## 1. 스프링이란?

### Spring is a framework.

- IoC container를 통해 bean들을 singleton으로 관리하고 필요에 따라 DI 해주는 framework

### 스프링은 오픈소스이다.

### IoC(Inversion of Control)

- Singleton으로 bean을 관리하는 container
- instance를 클래스 멤버처럼 하나의 heap 메모리 공간에 딱 한 번만 로딩해놓고(싱글톤) DI라는 의존성 주입을 통해 객체가 필요할 때마다 호출 시 DI를 통해 주입한다.

class: 설계도 (예) 가구)

object: 실체화가 가능한 것 (예) 의자, 침대)

Instance: 실체화 된 것 (예) 특정 의자, 특정 침대)

### DI(Dependency Injection)

- Instance 생성 시 IoC container에서 singleton으로 관리하는 bean들을 변수에 의존성 주입

### 스프링은 많은 필터를 가지고 있다.

- 권한체크
- 예) tomcat의 필터: web.xml, spring container의 필터: intercepter(AOP) 등

### 스프링은 많은 어노테이션을 가지고 있다.

- 컴파일체킹: 예) 상속된 클래스의 메서드를 컴파일체킹하여 해당되는 메서드가 없을 때 에러 발생 등
- 어노테이션을 통한 객체 생성:
    - `@component`: 해당 클래스를 메모리에 로딩. IoC가 스캔 시 이 어노테이션을 보면, 해당 클래스를 heap memory에 로딩한다.
    - `@autowired`: 로딩된 객체를 해당 변수에 주입. 스캔하여 같은 타입의 객체가 없다면 null, 있다면 주입한다.
- 리플렉션: 분석하는 기법 → 런타임시 분석 (메서드, 필드, 어노테이션 체킹)

### 스프링은 MessageConverter를 가지고 있다. 기본값은 현재 Json이다.

- MessageConverter: 요청, 응답 시 양쪽 언어를 이해시켜주는 중간 언어. 초기에는 xml이었지만 현재는 Json데이터 이다. (보통 Jackson을 이용한다.)

### BufferedReader와 BufferedWriter를 편하게 이용할 수 있다.

- 영어 한 글자는 8bit (256가지) → 통신최소단위는 1byte이다. 단위를 통일하기 위해 유니코드 utf-8을 사용한다(기본 3byte 단위)
- Byte Stream을 통해 요청(request)할 때, Java에서 InputStream을 쓰면 바이트 단위로 읽게 되는데, 이를 문자로 변환해 읽는 것이 InputStreamReader이다. 그러나 정해진 크기의 배열을 읽어야 해서 메모리 낭비가 발생한다. 이를 대신하여 BufferedReader를 쓴다.
- BufferedReader와 BufferedWriter(=PrintWriter)는 가변길이의 문자열을 수신 및 발신한다. BufferedReader는 JSP의 request.getReader(), BufferedWriter는 JSP의 out 내장객체와 동일한 기능을 한다.
- `@ResponseBody` → BufferedWriter `@RequestBody` → BufferedReader

출처. 메타코딩 YouTube