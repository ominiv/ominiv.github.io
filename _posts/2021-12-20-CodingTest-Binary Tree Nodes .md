---
title: HackerRank/Oracle Binary Tree Nodes
date: 2021-12-19 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle] Binary Tree Nodes

📌[문제링크](https://www.hackerrank.com/challenges/binary-search-tree-1/problem) [풀이참고](https://yurimyurim.tistory.com/15) 

  

*풀이 참고 링크에 들어가셔서 보시면 됩니다.   이진 트리의 노드 유형을 찾는 쿼리를 작성하는 문제다.   



## 1. Oracle 내장함수

*Solution*

1. 계층구조 쿼리의 START WITH절에서는 루트로 사용될 행을 정한다.

   `ROOT 노드는 부모값이 NULL인 행`

2. CONNECT BY PRIOR 절에 상위계층과 하위계층의 관계를 규정함

   `자식컬럼 = 부모컬럼 으로 지정하여 부모에서 자식으로 TOP DOWN 트리를 구성함`

3. LEVEL은 계층 구조 쿼리에서 수행결과의 Depth를 표현하는 Pseudocolumn임

   `LEVEL = 1 인 행을 ROOT로 지정`

4. CONNECT_BY_ISLEAF 는 계층구조 쿼리에서 최하위 레벨 여부를 반환한다.

   `CONNECT_BY_ISLEAF = 1인 행을 LEAF로 지정`

   

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

   



## 2. 다른 풀이

LEAF는 부모에 속하지 않는 특징을 이용해서  아래와 같이 풀 수있다. 

```SQL
SELECT  N, CASE WHEN N NOT IN (SELECT DISTINCT P FROM BST WHERE P IS NOT NULL) THEN 'Leaf'
                WHEN P IS NULL THEN 'Root'
                ELSE 'Inner'
                END
FROM BST
ORDER BY N;
```

  

## 3. 결과

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

