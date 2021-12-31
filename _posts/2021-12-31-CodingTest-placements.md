---
title: HackerRank/Oracle placements
date: 2021-12-30 23:30:09
categories:
- CodingTest
tags:
- oracle
- JOIN
---

# [HackerRank/Oracle] placements

📌[문제링크](https://www.hackerrank.com/challenges/placements/problem) 

<BR>

친구의 SALARY가 더 높은 경우를 선별하고 친구 연봉기준으로 정렬하면 된다.

<BR>

-------

##  JOIN이용

```sql
SELECT  S.NAME
FROM    (SELECT  F.ID, F.FRIEND_ID,P.SALARY AS F_SAL
        FROM    FRIENDS F
        LEFT OUTER JOIN PACKAGES P ON F.FRIEND_ID = P.ID) F
LEFT OUTER JOIN STUDENTS S ON F.ID = S.ID
LEFT OUTER JOIN PACKAGES P ON F.ID = P.ID
WHERE P.SALARY < F.F_SAL 
ORDER BY F.F_SAL ;

```

<BR>

---------

## 결과

```txt
Stuart
Priyanka
Paige
Jane
Julia
Belvet
Amina
Kristeen
Scarlet
Priya
Meera
```

