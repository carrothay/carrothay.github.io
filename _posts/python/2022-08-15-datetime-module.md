---
layout: post
title: "[Python] datetime module"
category: python
tags: python
sitemap: false
---
# datetime module

- `import datetime` 날짜와 시간을 사용하게 해주는 라이브러리이다.
1. date: 날짜만 저장
2. datetime: 날짜와 시간을 함께 저장
3. time, timedelta…

### 현재 시간 구하기(now)

```python
import datetime

today = datetime.date.today()
todaytime = datetime.datetime.now()
print(today)
print(todaytime)
print(todaytime.year,'년')

#2022-08-15
#2022-08-15 15:16:19.570146
#2022 년
```

### datetime 객체 구하기

```python
import datetime

firstday = datetime.date(2015,8,3)
#시간까지 지정 가능
firstday2 = datetime.datetime(2015,8,3,2,2,2)
```

### strftime() 메서드로 원하는 형식으로 출력(날짜 → 문자)

%w: 요일을 숫자로 표시 (**strftime의 0은 일요일이다.**)

%d: 날 출력

%m: 월 출력

%Y: 년 출력

%x: Local version의 날짜만 출력 외 다수

reference:

[Python strftime reference cheatsheet](https://strftime.org/)

### datetime 끼리의 연산도 가능

결과는 timedelta 객체 형태로 반환

```python
import datetime

total = d - firstday2
print(total)
#2569 days, 13:21:24.282112
```

### 요일 출력하기

datetime 의 weekday() 메서드는 0부터 6까지 리턴하며, **0은 월요일이다.**

```python
import datetime
days = ['월요일','화요일','수요일','목요일','금요일','토요일','일요일']
b=days[datetime.date(2022,8,15).weekday()]
print(b)
#월요일 출력
```

### 달력 출력하기

```python
import calendar
#2022년 달력 출력
print(calendar.calendar(2022))
#원하는 달만 출력
calendar.prmonth(2022, 8)
```

### timedelta 클래스

- 시간의 연산을 가능하게 해준다.
- 지금으로부터 100일 후 날짜

```python
import datetime

hundred = datetime.timedelta(days = 100)
print(hundred)
after = datetime.datetime.now() + hundred
print(after)

#100 days, 0:00:00
#2022-11-23 15:32:42.605404
```