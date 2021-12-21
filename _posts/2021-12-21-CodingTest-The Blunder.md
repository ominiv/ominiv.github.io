---
title: HackerRank/Oracle theblunder
date: 2021-12-20 23:30:09
categories:
- CodingTest
tags:
- oracle
- REPLACE
---

# [HackerRank/Oracle] the blunder

📌[문제링크](https://www.hackerrank.com/challenges/the-blunder/problem) 

<BR>

0을 제거한 숫자를 구하면 끝나는 문제다. 

`REPLACE( 열 , '찾는 문자' , '바꾸는 문자')`

<BR>

```sql
SELECT CEIL(AVG(SALARY) - AVG(REPLACE(SALARY,'0','')))
FROM EMPLOYEES;
```



