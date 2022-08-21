---
layout: post
title: "[Spring]Spring fundamentals 02"
category: spring
tags: spring
sitemap: false
---
# Spring fundamentals - 2

## 2. JPA란?

### Java Persistence API이다.

- Java프로그래밍을 할 때 영구적으로 데이터를 저장하기 위해 필요한 인터페이스
    - 자바의 데이터를 영구히 기록할 수 있는 환경을 제공하는 API
- Persistence: 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성. 영속성은 파일 시스템, 관계형 데이터베이스 또는 객체 데이터베이스 등을 활용하여 구현한다.
    - RAM: 휘발성 메모리
    - Java는 하드디스크 내 일정 공간을 DBMS로 관리 및 기록
- API: Application Programming Interface. 상하관계가 존재하는 약속
    - 프로토콜: 동등한 관계에 있는 약속(예) 인터넷)

### ORM기술이다.

- Object Relational Mapping, ORM은 나의 하인!
- Object를 DB에 연결하는 방법론
- 모델링: 모델class를 만드는 일. 추상적인 것에서 현실로 뽑아내는 것
    - Java와 DB의 Type이 다르기 때문에 class를 통해 DB세상의 데이터를 Java세상에 모델링
- JPA는 이를 역전시켜 1)Class를 먼저 만들고 2)DB의 table을 자동 설계해준다. 이 기법을 ORM(JPA의 interface)이라고 한다.

### 반복적인 CRUD작업을 생략하게 해준다.

- select, select all(output)/ delete, update, insert(input, DML)
- Java - DB간 connection 생성(세션 오픈), 쿼리 전송, DB data를 받을 때 Java Object로 타입 변경 등 모든 단순 반복 로직들을 JPA를 사용하여 일련의 작업들을 한번에 처리할 수 있다.

### 영속성 컨텍스트를 가지고 있다.

- Java와 DB가 서로간 데이터를 전달할 때 중간에 있는 영속성 컨텍스트를 통한다. 자동으로 데이터를 동기화 시켜준다.

### DB와 OOP의 불일치성을 해결하기 위한 방법론을 제공한다.(DB는 객체저장 불가능)

- DB에서 각각의 컬럼들이 가질 수 있는 자료형은 기본 자료형이다. :Object형 불가
- Java에서는 모델링 class안에 object형을 가질 수 있다. 이는 DB의 type과 다르다. → ORM을 통해 구현 가능, JPA가 자동으로 FK를 매핑해줌.

### OOP관점에서 모델링을 할 수 있게 해준다.(상속, 컴포지션, 연관관계)

### 방언 처리가 용이하여 Migration과 유지보수에 편리하다.

- 추상화객체를 사용하여 Oracle, MariaDB, Postgre, MsSql 등 다양한 방언을 지원한다.

출처. 메타코딩 YouTube