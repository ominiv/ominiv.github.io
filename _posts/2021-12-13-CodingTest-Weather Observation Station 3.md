---
title: HackerRank/Oracle Weather Observation Station 3
date: 2021-12-13 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle] Weather Observation Station 3

π[λ¬Έμ λ§ν¬](https://www.hackerrank.com/challenges/weather-observation-station-3/problem)



oracle μ κ²½μ°, λλκΈ°λ MOD



```sql
SELECT DISTINCT CITY
FROM STATION
WHERE MOD(ID,2)=0;
```

