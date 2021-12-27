---
title: HackerRank/Oracle Symmetric Pairs
date: 2021-12-25 23:30:09
categories:
- CodingTest
tags:
- oracle
- JOIN
---

# [HackerRank/Oracle] Symmetric Pairs

📌[문제링크](https://www.hackerrank.com/challenges/symmetric-pairs/problem)  [풀이참고](https://summa-cum-laude.tistory.com/21)

  <BR>

***풀이참고 링크 들어가셔서 보시면 됩니다.**

self join 문제다.  

x1==y2 & x2 ==y1 인 행들을 추출한 후 x<=y인 행을 남기면 된다. 

x<=y 조건을 만족 시키기 위해서는 = , < 를 분리해서 having절을 활용한다.



<BR>

## 1. INNER JOIN 이용

```sql
SELECT F1.X,F1.Y
FROM FUNCTIONS F1
INNER JOIN FUNCTIONS F2 ON F1.X = F2.Y AND F1.Y = F2.X
GROUP BY F1.X, F1.Y
HAVING COUNT(F1.X)>1 OR F1.X < F1.Y
ORDER BY F1.X;
```

<BR>

## 2. WHERE 이용

```sql
SELECT F1.X , F1.Y
FROM FUNCTIONS F1, FUNCTIONS F2
WHERE F1.X = F2.Y AND F1.Y = F2.X
GROUP BY F1.X , F1.Y
HAVING COUNT(F1.X) > 1 OR F1.X < F1.Y
ORDER BY F1.X;
```



