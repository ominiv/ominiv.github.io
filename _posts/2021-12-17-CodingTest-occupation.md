---
title: HackerRank/Oracle Occupations
date: 2021-12-16 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle] Occupations

๐[๋ฌธ์ ๋งํฌ](https://www.hackerrank.com/challenges/occupations/problem) [ํ์ด์ฐธ๊ณ ](https://yurimyurim.tistory.com/11)

 

occupation ์ด์ pivotํ๋ ๋ฌธ์ ๋ค. 



## 1. DECODE/MIN ์ด์ฉ

DECODEํจ์๋ ํ๋ก๊ทธ๋๋ฐ์์์ if else ์ ๋น์ทํ ๊ธฐ๋ฅ์ ์ํํจ

`DECODE(์ปฌ๋ฝ, ์กฐ๊ฑด1, ๊ฒฐ๊ณผ1, ์กฐ๊ฑด2, ๊ฒฐ๊ณผ2)`

```sql
SELECT  MIN(DECODE(OCCUPATION, 'Doctor',NAME)) Doctor,
        MIN(DECODE(OCCUPATION, 'Professor',NAME)) Professor,
        MIN(DECODE(OCCUPATION, 'Singer',NAME)) Singer,
        MIN(DECODE(OCCUPATION, 'Actor',NAME)) Actor
FROM    (
        SELECT OCCUPATION, NAME, ROW_NUMBER() OVER(PARTITION BY OCCUPATION ORDER BY NAME) RN
        FROM OCCUPATIONS
        )
GROUP BY RN
ORDER BY 1,2,3,4;
```





## 2. PIVOT ์ด์ฉ

Oracle 11g ์ด์ ๋ฒ์ ์ ๊ฒฝ์ฐ PIVOTํจ์๋ฅผ ์ฌ์ฉ ํ  ์์์

```sql
SELECT  Doctor, Professor, Singer, Actor 
FROM (
    SELECT OCCUPATION, NAME, ROW_NUMBER() OVER(PARTITION BY OCCUPATION ORDER BY NAME)RN
    FROM OCCUPATIONS
)
PIVOT(
    MIN(NAME) FOR OCCUPATION IN ('Doctor' AS Doctor
                                 ,'Professor' AS Professor
                                 ,'Singer' AS Singer
                                 , 'Actor' AS Actor )
)
ORDER BY 1,2,3,4;
```





## 3. ์ถ๊ฐ๋ก ์์์ผ ํ  ๊ฒ

์ค๋ผํด์์ ๋ถ์ ํจ์๋ฅผ ์ฌ์ฉ ํ ๋ PARTITION BY๋ฅผ ์ฌ์ฉํ์ฌ ๊ทธ๋ฃน์ผ๋ก ๋ฌถ์ด์ ์ฐ์ฐ์ ํ  ์ ์๋ค.

GROUP BY๋ฅผ ์ฌ์ฉํ์ง์๊ณ , ์กฐํ๋ ๊ฐ ํ์ ๊ทธ๋ฃน์ผ๋ก ์ง๊ณ๋ ๊ฐ์ ํ์ ํ ๋ OVER์ ๊ณผ PARTITION BY ์ ์ ์ฌ์ฉํ๋ฉด๋๋ค.

`๋ถ์ํจ์([์นผ๋ผ]) OVER(PARTITION BY ์นผ๋ผ1, ์นผ๋ผ2... [ORDER BY ์ ] [WINDOWING ์ ])`



์ฌ๊ธฐ์๋ ROW_NUMBER & OVER & PARTITION BY ๋ฅผ ์ด์ฉํด ์ง์๋ณ ์ด๋ฆ ์์ผ๋ก ์๋ฒ์ ํ๊ธฐํ๋ค.

