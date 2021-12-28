---
title: HackerRank/Oracle Ollivander's Inventory
date: 2021-12-27 23:30:09
categories:
- CodingTest
tags:
- oracle
- row_number
- 순위함수
---

# [HackerRank/Oracle] Ollivander's Inventory

📌[문제링크](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem) 

<BR>

불친절한 문제다. 

non  evil인 지팡이들 중 power , age를 기준으로 내림차순으로 정렬하는 문제다. 

**추가로 지팡이 age와 power가 동일할경우 최소 gold galleons 인 행을 선별해야한다.** 

<BR>

## 1. ROW_NUMBER 이용

그룹내 순위를 결정하는 함수를 활용하자. 

`select row_number() over(partition by [그룹핑할 열] order by [정렬할 열]) from 테이블명;`

```sql
SELECT ID, AGE, COINS_NEEDED, POWER
FROM(
    SELECT  W.ID, WP.AGE, W.COINS_NEEDED, W.POWER, ROW_NUMBER() OVER (PARTITION BY W.POWER, WP.AGE ORDER BY W.COINS_NEEDED) RN
    FROM    WANDS W
    LEFT OUTER JOIN (SELECT * FROM Wands_Property) WP ON W.CODE= WP.CODE
    WHERE WP.IS_EVIL = 0 
    ORDER BY W.POWER DESC, WP.AGE DESC
)
WHERE RN = 1;
```

<BR>

## 2. 결과

```txt
1038 496 4789 10
1130 494 9439 10
1315 492 4126 10
9 491 7345 10
858 483 4352 10
1164 481 9831 10
1288 464 4952 10
861 462 8302 10
```



## 3. 그외 그룹내 순위 결정하는 함수

아래 세 함수는 악간의 차이가 있다.

### 3-1 row_number()

1등이 2명이상 존재하더라도 1,2등으로 나눔 1->2->3

`select row_number() over(partition by [그룹핑할 열] order by [정렬할 열]) from 테이블명;`

### 3-2 rank()

1등이 두명이면 그 다음 순위인 3등이 된다. 1->1->3

`select rank() over(partition by [그룹핑할 열] order by [정렬할 열]) from 테이블명`

### 3-2 dense_rank()

1등이 두명이면 다음순위는 2등이 된다. 1->1->2

`select dense_rank() over(partition by [그룹핑할 열] order by [정렬할 열]) from 테이블명`
