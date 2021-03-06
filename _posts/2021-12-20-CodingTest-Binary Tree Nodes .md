---
title: HackerRank/Oracle Binary Tree Nodes
date: 2021-12-19 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle] Binary Tree Nodes

๐[๋ฌธ์ ๋งํฌ](https://www.hackerrank.com/challenges/binary-search-tree-1/problem) [ํ์ด์ฐธ๊ณ ](https://yurimyurim.tistory.com/15) 

  

*ํ์ด ์ฐธ๊ณ  ๋งํฌ์ ๋ค์ด๊ฐ์์ ๋ณด์๋ฉด ๋ฉ๋๋ค.   

์ด์ง ํธ๋ฆฌ์ ๋ธ๋ ์ ํ์ ์ฐพ๋ ์ฟผ๋ฆฌ๋ฅผ ์์ฑํ๋ ๋ฌธ์ ๋ค.   



## 1. Oracle ๋ด์ฅํจ์

*Solution*

1. ๊ณ์ธต๊ตฌ์กฐ ์ฟผ๋ฆฌ์ START WITH์ ์์๋ ๋ฃจํธ๋ก ์ฌ์ฉ๋  ํ์ ์ ํ๋ค.

   `ROOT ๋ธ๋๋ ๋ถ๋ชจ๊ฐ์ด NULL์ธ ํ`

2. CONNECT BY PRIOR ์ ์ ์์๊ณ์ธต๊ณผ ํ์๊ณ์ธต์ ๊ด๊ณ๋ฅผ ๊ท์ ํจ

   `์์์ปฌ๋ผ = ๋ถ๋ชจ์ปฌ๋ผ ์ผ๋ก ์ง์ ํ์ฌ ๋ถ๋ชจ์์ ์์์ผ๋ก TOP DOWN ํธ๋ฆฌ๋ฅผ ๊ตฌ์ฑํจ`

3. LEVEL์ ๊ณ์ธต ๊ตฌ์กฐ ์ฟผ๋ฆฌ์์ ์ํ๊ฒฐ๊ณผ์ Depth๋ฅผ ํํํ๋ Pseudocolumn์

   `LEVEL = 1 ์ธ ํ์ ROOT๋ก ์ง์ `

4. CONNECT_BY_ISLEAF ๋ ๊ณ์ธต๊ตฌ์กฐ ์ฟผ๋ฆฌ์์ ์ตํ์ ๋ ๋ฒจ ์ฌ๋ถ๋ฅผ ๋ฐํํ๋ค.

   `CONNECT_BY_ISLEAF = 1์ธ ํ์ LEAF๋ก ์ง์ `

   

```sql
SELECT N,   CASE WHEN LEVEL = 1 THEN 'Root'
            WHEN CONNECT_BY_ISLEAF=1 THEN 'Leaf'
            ELSE 'Inner'
            END
FROM   BST
START WITH P IS NULL
CONNECT BY PRIOR N=P
ORDER BY N;
```

   



## 2. ๋ค๋ฅธ ํ์ด

LEAF๋ ๋ถ๋ชจ์ ์ํ์ง ์๋ ํน์ง์ ์ด์ฉํด์  ์๋์ ๊ฐ์ด ํ ์์๋ค. 

```SQL
SELECT  N, CASE WHEN N NOT IN (SELECT DISTINCT P FROM BST WHERE P IS NOT NULL) THEN 'Leaf'
                WHEN P IS NULL THEN 'Root'
                ELSE 'Inner'
                END
FROM BST
ORDER BY N;
```

  

## 3. ๊ฒฐ๊ณผ

```txt
S1 Leaf
2 Inner
3 Leaf
4 Inner
5 Leaf
6 Inner
7 Leaf
8 Leaf
9 Inner
10 Leaf
11 Inner
12 Leaf
13 Inner
14 Leaf
15 Root
```

