---
title: HackerRank/Oracle 15 Days of Learning SQL
date: 2021-12-30 23:30:09
categories:
- CodingTest
tags:
- oracle
- SubQuery
- ์ค๋ต๋ธํธ
---

# [HackerRank/Oracle] 15 Days of Learning SQL

๐[๋ฌธ์ ๋งํฌ](https://www.hackerrank.com/challenges/placements/problem) 

<BR>

๋ฌธ์  ์ดํด๋ฅผ ํ๊ธฐ๊ฐ ์ด๋ ค์ ์.  ๋ค์ํ์ด๋ณด์.

์๋ ๋๊ฐ์ง ์ฟผ๋ฆฌ๋ง ๋ง๋ค๋ฉด ๋๋ค. 1๋ฒ ์ฟผ๋ฆฌ์ ๊ฒฝ์ฐ ๊ณจ์น์ํ ๋ค.<Br>**1. ๊ฐ ์ผ์๋ณ ๋งค์ผ 1ํ์ด์ ์ ์ถํ ํด์ปค์ ์ธ์์<br>**2. ๊ฐ ์ผ์๋ณ ์ต๋ ์ ์ถ์๋ฅผ ๊ธฐ๋กํ ํด์ปคid

<BR>

-------

##  SubQuery

```sql
SELECT A.SUBMISSION_DATE, A.CNT, B.HACKER_ID, C.NAME
  FROM 
  /*๊ฐ ์ผ์๋ณ ๋งค์ผ 1ํ์ด์ ์ ์ถํ ํด์ปค์ ์ด ์ธ์์*/
  (
        SELECT SUBMISSION_DATE
             , COUNT(DISTINCT HACKER_ID) CNT
          FROM SUBMISSIONS S
         WHERE (SELECT COUNT(DISTINCT SUBMISSION_DATE)
                  FROM SUBMISSIONS SS
                 WHERE SS.SUBMISSION_DATE < S.SUBMISSION_DATE
                   AND SS.HACKER_ID = S.HACKER_ID
               ) = (S.SUBMISSION_DATE - TO_DATE('2016-03-01'))
         GROUP BY SUBMISSION_DATE
       ) A
       /*๊ฐ ์ผ์๋ณ ์ต๋ ์ ์ถ์๋ฅผ ๊ธฐ๋กํ hacker_id*/
     , (SELECT SUBMISSION_DATE
             , HACKER_ID
             , ROW_NUMBER() OVER(PARTITION BY SUBMISSION_DATE ORDER BY CNT DESC, HACKER_ID) RN
          FROM (
                SELECT SUBMISSION_DATE
                     , HACKER_ID
                     , COUNT(1) OVER(PARTITION BY SUBMISSION_DATE, HACKER_ID) CNT
                  FROM SUBMISSIONS S
               )
       ) B
       /*hacker name*/
     , HACKERS C
 WHERE B.RN = 1
   AND A.SUBMISSION_DATE = B.SUBMISSION_DATE
   AND B.HACKER_ID = C.HACKER_ID

```

<BR>

---------

## ๊ฒฐ๊ณผ

```txt
2016-03-01 112 81314 Denise
2016-03-02 59 39091 Ruby
2016-03-03 51 18105 Roy
2016-03-04 49 533 Patrick
2016-03-05 49 7891 Stephanie
2016-03-06 49 84307 Evelyn
2016-03-07 35 80682 Deborah
2016-03-08 35 10985 Timothy
2016-03-09 35 31221 Susan
2016-03-10 35 43192 Bobby
2016-03-11 35 3178 Melissa
2016-03-12 35 54967 Kenneth
2016-03-13 35 30061 Julia
2016-03-14 35 32353 Rose
2016-03-15 35 27789 Helen
```

