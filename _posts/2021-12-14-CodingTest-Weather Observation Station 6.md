---
title: HackerRank/Oracle Weather Observation Station 6
date: 2021-12-13 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle] Weather Observation Station 6

π[λ¬Έμ λ§ν¬](https://www.hackerrank.com/challenges/weather-observation-station-6/problem)



μ κ·μμ μ΄μ©νλλ‘ νμ.

**REGEXP_LIKE(VALUE , 'μ κ·μ')**



## 1. OR μ΄μ©

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE ('A%') OR CITY LIKE ('E%') OR CITY LIKE ('I%') OR  CITY LIKE ('O%')OR CITY LIKE ('U%') ;

SELECT DISTINCT CITY
FROM STATION
WHERE UPPER(CITY) LIKE ('A%') OR UPPER(CITY) LIKE ('E%') OR UPPER(CITY) LIKE ('I%') OR  UPPER(CITY) LIKE ('O%')OR UPPER(CITY) LIKE ('U%') ;

```

## 2. μ κ·μ μ΄μ©

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE REGEXP_LIKE(CITY, '^A|^E|^I|^O|^U');
```

