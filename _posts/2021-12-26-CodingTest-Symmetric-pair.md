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

๐[๋ฌธ์ ๋งํฌ](https://www.hackerrank.com/challenges/symmetric-pairs/problem)  [ํ์ด์ฐธ๊ณ ](https://summa-cum-laude.tistory.com/21)

  <BR>

***ํ์ด์ฐธ๊ณ  ๋งํฌ ๋ค์ด๊ฐ์์ ๋ณด์๋ฉด ๋ฉ๋๋ค.**

self join ๋ฌธ์ ๋ค.  

x1==y2 & x2 ==y1 ์ธ ํ๋ค์ ์ถ์ถํ ํ x<=y์ธ ํ์ ๋จ๊ธฐ๋ฉด ๋๋ค. 

x<=y ์กฐ๊ฑด์ ๋ง์กฑ ์ํค๊ธฐ ์ํด์๋ = , < ๋ฅผ ๋ถ๋ฆฌํด์ having์ ์ ํ์ฉํ๋ค.



<BR>

## 1. INNER JOIN ์ด์ฉ

```sql
SELECT F1.X,F1.Y
FROM FUNCTIONS F1
INNER JOIN FUNCTIONS F2 ON F1.X = F2.Y AND F1.Y = F2.X
GROUP BY F1.X, F1.Y
HAVING COUNT(F1.X)>1 OR F1.X < F1.Y
ORDER BY F1.X;
```

<BR>

## 2. WHERE ์ด์ฉ

```sql
SELECT F1.X , F1.Y
FROM FUNCTIONS F1, FUNCTIONS F2
WHERE F1.X = F2.Y AND F1.Y = F2.X
GROUP BY F1.X , F1.Y
HAVING COUNT(F1.X) > 1 OR F1.X < F1.Y
ORDER BY F1.X;
```



