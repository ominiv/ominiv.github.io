---
title: HackerRank/Oracle The PADs
date: 2021-12-16 23:30:09
categories:
- CodingTest
tags:
- oracle
---

# [HackerRank/Oracle]  The PADs 

ð[ë¬¸ì ë§í¬](https://www.hackerrank.com/challenges/the-pads/problem)

 

ë¬¸ìì´ì í©ì³ ì¶ë ¥íë ë¬¸ì ë¤.



ì¤ë¼í´ììë ë¬¸ì í©ì¹ ë  `||, CONCAT`ì ì¬ì©í  ì ìë¤.

ë ê°ì§ì ëí´ ììë³´ì.



## 1. || ì´ì©

```sql
SELECT NAME || '(' || SUBSTR(OCCUPATION,1,1) || ')'
FROM OCCUPATIONS
ORDER BY NAME;

SELECT 'There are a total of ' || COUNT(OCCUPATION) || ' '|| LOWER(OCCUPATION)|| 's.'
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION) , OCCUPATION;
```



## 2. CONCAT ì´ì©

ì¤ë¡ì§ **2ê° ììë§** ë°ì í©ì¹  ì ìê¸°ëë¬¸ì CONCAT ìì CONCATì ì ìí´ì£¼ë ê³¼ì ì´ íì

ë¬¸ìì´ì í©ì¹  ê² ë§ì¼ë©´ ë¶í¸í¨

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

