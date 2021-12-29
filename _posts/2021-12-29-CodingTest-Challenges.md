---
title: HackerRank/Oracle Challenges
date: 2021-12-28 23:30:09
categories:
- CodingTest
tags:
- oracle
- JOIN
---

# [HackerRank/Oracle] Challenges

📌[문제링크](https://www.hackerrank.com/challenges/challenges/problem) 

<BR>

복잡한 문제였는데 아직 Basic 단계다.

학생별 challenge count를 출력하는 쿼리를 작성하면 된다. <br>여기서 challenge count = Max(challenge count)  or  challenge count 중복이 존재하면 안된다.

<BR>

## 1. JOIN, IN이용

```sql
SELECT  H.HACKER_ID, H.NAME, COUNT(C.CHALLENGE_ID) AS CNT
FROM    CHALLENGES C
LEFT OUTER JOIN HACKERS H ON C.HACKER_ID = H.HACKER_ID
GROUP BY H.HACKER_ID, H.NAME
	   /*challenge count == Max(challenge count)인 경우 선별*/
HAVING COUNT(C.CHALLENGE_ID) = (SELECT  MAX(CNT)
              FROM    (SELECT COUNT(*) AS CNT
                       FROM CHALLENGES 
                       GROUP BY HACKER_ID 
                       ORDER BY COUNT(*) DESC))
        /*challenge count가 중복이 없는 경우 선별*/
        OR COUNT(C.CHALLENGE_ID) IN (SELECT  CNT 
                                    FROM    (SELECT COUNT(*) AS CNT 
                                             FROM CHALLENGES 
                                             GROUP BY HACKER_ID)
                                    GROUP BY CNT 
                                    HAVING COUNT(CNT)=1)
ORDER BY COUNT(C.CHALLENGE_ID) DESC, H.HACKER_ID;

```

<BR>

## 2. 결과

```txt
5120 Julia 50 
18425 Anna 50 
20023 Brian 50 
33625 Jason 50 
41805 Benjamin 50 
52462 Nicholas 50 
64036 Craig 50 
69471 Michelle 50 
77173 Mildred 50 
94278 Dennis 50 
96009 Russell 50 
96716 Emily 50 
72866 Eugene 42 
37068 Patrick 41 
12766 Jacqueline 40 
86280 Beverly 37 
19835 Joyce 36 
38316 Walter 35 
29483 Jeffrey 34 
23428 Arthur 33 {-truncated-}
```



