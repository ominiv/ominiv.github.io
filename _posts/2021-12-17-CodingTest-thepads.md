---
title: HackerRank/Oracle The PADs
date: 2021-12-17 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle]  The PADs 

📌[문제링크](https://www.hackerrank.com/challenges/the-pads/problem)

 

문자열을 합쳐 출력하는 문제다.



오라클에서는 문자 합칠때  [||] ,[CONCAT]을 사용할 수 있다.

두 가지에 대해 알아보자.



## 1. || 이용

```sql
SELECT NAME || '(' || SUBSTR(OCCUPATION,1,1) || ')'
FROM OCCUPATIONS
ORDER BY NAME;

SELECT 'There are a total of ' || COUNT(OCCUPATION) || ' '|| LOWER(OCCUPATION)|| 's.'
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION) , OCCUPATION;
```



## 2. CONCAT 이용

오로지 **2개 요소만** 받아 합칠 수 있기때문에 CONCAT 안에 CONCAT을 정의해주는 과정이 필요

문자열을 합칠 게 많으면 불편함

```sql
SELECT  CONCAT(
            CONCAT( 
                CONCAT(NAME ,'('),SUBSTR(OCCUPATION,1,1)
                  )
            ,')')
FROM OCCUPATIONS
ORDER BY NAME ;

SELECT CONCAT(CONCAT(
        CONCAT(
            CONCAT('There are a total of ', COUNT(OCCUPATION)), ' '
             ),LOWER(OCCUPATION)),'s.')
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION), OCCUPATION;
```

