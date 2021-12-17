---
title: HackerRank/Oracle Occupations
date: 2021-12-15 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle] Occupations

📌[문제링크](https://www.hackerrank.com/challenges/occupations/problem) [풀이참고](https://yurimyurim.tistory.com/11)

 

occupation 열을 pivot하는 문제다. 



## 1. DECODE/MIN 이용

DECODE함수는 프로그래밍에서의 if else 와 비슷한 기능을 수행함

`DECODE(컬럽, 조건1, 결과1, 조건2, 결과2)`

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





## 2. PIVOT 이용

Oracle 11g 이상 버전의 경우 PIVOT함수를 사용 할 수있음

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





## 3. 추가로 알아야 할 것

오라클에서 분석 함수를 사용 할때 PARTITION BY를 사용하여 그룹으로 묶어서 연산을 할 수 있다.

GROUP BY를 사용하지않고, 조회된 각 행에 그룹으로 집계된 값을 표시 할때 OVER절과 PARTITION BY 절을 사용하면된다.

`분석함수([칼럼]) OVER(PARTITION BY 칼럼1, 칼럼2... [ORDER BY 절] [WINDOWING 절])`



여기서는 ROW_NUMBER & OVER & PARTITION BY 를 이용해 직업별 이름 순으로 순번을 표기했다.

