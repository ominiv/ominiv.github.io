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

๐[๋ฌธ์ ๋งํฌ](https://www.hackerrank.com/challenges/the-report/problem) 

<BR>

ํน์  ๊ฐ์ ๋ฒ์๋ฅผ ํ์ฉํด grade๋ฅผ ๊ตฌํ๋ ๋ฌธ์ ๋ค. 

join์ key๊ฐ ์๋ ๋ฒ์๋ก๋ ์ฌ์ฉํ  ์ ์๋ค.

โ join ๊ณผ between์ ํ์ฉํ์

<BR>

## 1. LEFT OUTER JOIN ์ด์ฉ

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

## 2. ๊ฒฐ๊ณผ

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





