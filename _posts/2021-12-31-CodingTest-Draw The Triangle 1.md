---
title: HackerRank/Oracle Draw The Triangle 1
date: 2021-12-30 23:30:09
categories:
- CodingTest
tags:
- oracle
- CONNECT BY
- RPAD
---

# [HackerRank/Oracle] Draw The Triangle 1

📌[문제링크](https://www.hackerrank.com/challenges/draw-the-triangle-1/problem) [풀이참고](https://techybilli.com/hackerrank-challenge-draw-the-triangle-1/)

<BR>

***풀이참고 링크에 들어가셔서 보시면 됩니다.**

별찍는 문제인데 SQL에서는 도저히 생각이 안나서 답을 찾아봤다. <BR>

-------

##  CONNECT BY, RPAD이용

RPAD 함수는 지정한 길이 만큼 오른쪽부터 특정문자로 채워준다.<BR>`RPAD ('값', '총문자길이', '채울문자')`

```sql
SELECT  RPAD('*', x*2, ' *')
FROM    (SELECT LEVEL x
FROM DUAL CONNECT BY LEVEL <=20
ORDER BY LEVEL DESC);
```

<BR>

---------

## 결과

```txt
* * * * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * *
* * * * * * * * * * * * * *
* * * * * * * * * * * * *
* * * * * * * * * * * *
* * * * * * * * * * *
* * * * * * * * * *
* * * * * * * * *
* * * * * * * *
* * * * * * *
* * * * * *
* * * * *
* * * *
* * *
* *
*
```

--------

## LEVEL에 대해 알아보자

LEVEL은 오라클 내에서 실행되는 쿼리내에서 사용가능한 가상의 열이다.<BR>트리 내에서 어떤 LEVEL에 위치하는지를 나타내는 정수값이다. <BR>만약 계층형 쿼리가 아니라면 LEVEL은 모두 0이다.

**LEVEL에 대한 조건절을 이용할때는 `CONNECT BY`를 이용하면된다.**
