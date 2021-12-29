---
title: HackerRank/Oracle Contest Leaderboard
date: 2021-12-28 23:30:09
categories:
- CodingTest
tags:
- oracle
- JOIN
---

# [HackerRank/Oracle] Contest Leaderboard

📌[문제링크](https://www.hackerrank.com/challenges/challenges/problem) 

<BR>

각 challenge별 hack의 최대값을 구한 후, hacker_id 기준으로 총합을 구하면 된다.

<BR>

## 1. JOIN, IN이용

```sql
SELECT S.HACKER_ID, H.NAME, SUM(S.TOTAL)
/*각 challenge별 hack의 최대값을 추출*/
FROM    (SELECT  HACKER_ID,CHALLENGE_ID,MAX(SCORE) AS TOTAL
        FROM    SUBMISSIONS
        GROUP BY HACKER_ID,CHALLENGE_ID) S
LEFT OUTER JOIN HACKERS H ON H.HACKER_ID = S.HACKER_ID
GROUP BY S.HACKER_ID, H.NAME
HAVING SUM(S.TOTAL)>0
ORDER BY SUM(S.TOTAL) DESC , S.HACKER_ID;
```

<BR>

## 2. 결과

```txt
76971 Ashley 760 
84200 Susan 710 
76615 Ryan 700 
82382 Sara 640 
79034 Marilyn 580 
78552 Harry 570 
74064 Helen 540 
78688 Sean 540 
83832 Jason 540 
72796 Jose 510 
76216 Carlos 510 
90304 Lillian 500 
88507 Patrick 490 
72505 Keith 480 
88018 Dennis 480 
78918 Julia 470 
85319 Shawn 470 
71357 Bobby 460 
72047 Elizabeth 460 
74147 Jason 460 
{-truncated-}
```

