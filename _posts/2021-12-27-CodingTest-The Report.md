---
title: HackerRank/Oracle The Report
date: 2021-12-25 23:30:09
categories:
- CodingTest
tags:
- oracle
- JOIN
---

# [HackerRank/Oracle] The Report

📌[문제링크](https://www.hackerrank.com/challenges/the-report/problem) 

<BR>

특정 값의 범위를 활용해 grade를 구하는 문제다. 

join을 key가 아닌 범위로도 사용할 수 있다.

✔ join 과 between을 활용하자

<BR>

## 1. LEFT OUTER JOIN 이용

```sql
SELECT  
        CASE
            WHEN GRADE <= 7 THEN NULL
            WHEN GRADE > 7 THEN STUDENTS.NAME
        END, GRADE, STUDENTS.MARKS
FROM STUDENTS 
LEFT OUTER JOIN GRADES ON STUDENTS.MARKS BETWEEN GRADES.MIN_MARK AND GRADES.MAX_MARK
ORDER BY GRADE DESC, STUDENTS.NAME ASC, STUDENTS.MARKS ASC; 
```

<BR>

## 2. 결과

```txt
Britney 10 95
Heraldo 10 94
Julia 10 96
Kristeen 10 100
Stuart 10 99
Amina 9 89
Christene 9 88
Salma 9 81
Samantha 9 87
Scarlet 9 80
Vivek 9 84
Aamina 8 77
Belvet 8 78
Paige 8 74
Priya 8 76
Priyanka 8 77
NULL 7 64
NULL 7 66
NULL 6 55
NULL 4 34
NULL 3 24
Contest Calendar
```





