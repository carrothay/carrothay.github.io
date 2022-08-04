---
layout: post
title: "Python: List Comprehension"
category: python
tags: python
sitemap: false
---
# 리스트 컴프리헨션

### 리스트 생성

1부터 10까지 정수를 가지고 있는 리스트 생성

```python
numbers = []
for n in range(1, 10+1):
    numbers.append(n)
print(numbers)
```

컴프리헨션 표기 (리스트 컴프리헨션)

```python
[x for x in range(10)]
```

### 조건 걸기

```python
even_numbers = []
for n in range(1, 10+1):
    if n % 2 == 0:
        even_numbers.append(n)
print(even_numbers)
```

컴프리헨션 표기

- if 키워드는 for문 다음에 위치함

```python
[x for x in range(1, 10+1) if x % 2 == 0]
```

### 중복 표현

컴프리헨션 내부에서 for 키워드와 if 키워드를 반복 사용할 수 있음
