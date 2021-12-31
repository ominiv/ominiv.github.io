---
title: HackerRank/Oracle 15 Days of Learning SQL
date: 2021-12-30 23:30:09
categories:
- CodingTest
tags:
- oracle
- SubQuery
---

# [HackerRank/Oracle] 15 Days of Learning SQL

📌[문제링크](https://www.hackerrank.com/challenges/placements/problem) 

<BR>

문제 이해를 하기가 어려웠음.  다시풀어보자.

아래 두가지 쿼리만 만들면 된다. 1번 쿼리의 경우 골치아팠다.<Br>**1. 각 일자별 매일 1회이상 제출한 해커의 인원수<br>**2. 각 일자별 최대 제출수를 기록한 해커id

<BR>

-------

##  SubQuery

```sql
SELECT A.SUBMISSION_DATE, A.CNT, B.HACKER_ID, C.NAME
  FROM 
  /*각 일자별 매일 1회이상 제출한 해커의 총 인원수*/
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
       /*각 일자별 최대 제출수를 기록한 hacker_id*/
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

## 결과

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

