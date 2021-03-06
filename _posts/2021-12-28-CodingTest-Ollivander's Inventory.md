---
title: HackerRank/Oracle Ollivander's Inventory
date: 2021-12-27 23:30:09
categories:
- CodingTest
tags:
- oracle
- ROW_NUMBER
---

# [HackerRank/Oracle] Ollivander's Inventory

๐[๋ฌธ์ ๋งํฌ](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem) 

<BR>

๋ถ์น์ ํ ๋ฌธ์ ๋ค. 

non  evil์ธ ์งํก์ด๋ค ์ค power , age๋ฅผ ๊ธฐ์ค์ผ๋ก ๋ด๋ฆผ์ฐจ์์ผ๋ก ์ ๋ ฌํ๋ ๋ฌธ์ ๋ค. 

**์ถ๊ฐ๋ก ์งํก์ด age์ power๊ฐ ๋์ผํ ๊ฒฝ์ฐ ์ต์ gold galleons ์ธ ํ์ ์ ๋ณํด์ผํ๋ค.** 

<BR>

## 1. ROW_NUMBER ์ด์ฉ

๊ทธ๋ฃน๋ด ์์๋ฅผ ๊ฒฐ์ ํ๋ ํจ์๋ฅผ ํ์ฉํ์. 

`select row_number() over(partition by [๊ทธ๋ฃนํํ  ์ด] order by [์ ๋ ฌํ  ์ด]) from ํ์ด๋ธ๋ช;`

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

## 2. ๊ฒฐ๊ณผ

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



## 3. ๊ทธ์ธ ๊ทธ๋ฃน๋ด ์์ ๊ฒฐ์ ํ๋ ํจ์

์๋ ์ธ ํจ์๋ ์๊ฐ์ ์ฐจ์ด๊ฐ ์๋ค.

### 3-1 row_number()

1๋ฑ์ด 2๋ช์ด์ ์กด์ฌํ๋๋ผ๋ 1,2๋ฑ์ผ๋ก ๋๋ 1->2->3

`select row_number() over(partition by [๊ทธ๋ฃนํํ  ์ด] order by [์ ๋ ฌํ  ์ด]) from ํ์ด๋ธ๋ช;`

### 3-2 rank()

1๋ฑ์ด ๋๋ช์ด๋ฉด ๊ทธ ๋ค์ ์์์ธ 3๋ฑ์ด ๋๋ค. 1->1->3

`select rank() over(partition by [๊ทธ๋ฃนํํ  ์ด] order by [์ ๋ ฌํ  ์ด]) from ํ์ด๋ธ๋ช`

### 3-2 dense_rank()

1๋ฑ์ด ๋๋ช์ด๋ฉด ๋ค์์์๋ 2๋ฑ์ด ๋๋ค. 1->1->2

`select dense_rank() over(partition by [๊ทธ๋ฃนํํ  ์ด] order by [์ ๋ ฌํ  ์ด]) from ํ์ด๋ธ๋ช`
