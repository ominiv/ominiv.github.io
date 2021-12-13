---
title: oracle Weather Observation Station 3
date: 2021-12-13 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [oracle] Weather Observation Station 3

📌[문제링크](https://www.hackerrank.com/challenges/weather-observation-station-3/problem)



oracle 의 경우, 나누기는 MOD



```sql
SELECT DISTINCT CITY
FROM STATION
WHERE MOD(ID,2)=0;
```


