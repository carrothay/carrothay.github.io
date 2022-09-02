---
layout: post
title: "[Spring]Spring fundamentals 05"
category: spring
tags: spring
sitemap: false
---
# Spring fundamentals - 5

## 3. Springboot 동작원리(3)

### (8) Handler Mapping: 요청 주소에 따른 적절한 컨트롤러 요청

- Get요청 ex) http://localhost:8080/post/1
- 디스패쳐가 사용자 요청을 받아서 핸들러 매핑에게 어떤 컨트롤러를 찾아야 하는지 임무를 위임
- 요청응답 시 디스패쳐가 뷰 리졸버에 응답을 전달 후에 뷰 리졸버가 결과를 출력

### (9) 응답

html파일 응답 - ViewResolver(jsp→html로 변환)

Data응답 - MessageConverter (json)

출처. 메타코딩 YouTube