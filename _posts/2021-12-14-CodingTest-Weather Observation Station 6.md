---
title: Oracle Weather Observation Station 6
date: 2021-12-13 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [Oracle] Weather Observation Station 6

📌[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-6/problem)



정규식을 이용하도록 하자.

**REGEXP_LIKE(VALUE , '정규식')**



## 1. OR 이용

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE ('A%') OR CITY LIKE ('E%') OR CITY LIKE ('I%') OR  CITY LIKE ('O%')OR CITY LIKE ('U%') ;

SELECT DISTINCT CITY
FROM STATION
WHERE UPPER(CITY) LIKE ('A%') OR UPPER(CITY) LIKE ('E%') OR UPPER(CITY) LIKE ('I%') OR  UPPER(CITY) LIKE ('O%')OR UPPER(CITY) LIKE ('U%') ;

```

## 2. 정규식 이용

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(CITY, '^A|^E|^I|^O|^U');
```

