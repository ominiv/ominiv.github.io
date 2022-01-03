---
title: HackerRank/Oracle Print Prime Numbers
date: 2021-12-30 00:00:01
categories:
- CodingTest
tags:
- oracle
- LISTAGG
- 
---

# [HackerRank/Oracle] Print Prime Numbers

📌[문제링크](https://www.hackerrank.com/challenges/print-prime-numbers/problem) [풀이참고](https://yurimyurim.tistory.com/16?category=951967)

<BR>

***풀이참고 링크에 들어가셔서 보시면 됩니다.**

1000이하 소수를 출력하면 된다.<BR>제곱근 범위 나누기법을 활용하자.

> **제곱근 범위 나누기법**<bR>소수 여부를 검사할 수에 대해 그 값의 제곱근을 기준으로 대칭적으로 계산되므로 제곱근 이하의 작은 값까지만 검사흘 하면 나머지는 검사할 필요가 없다. *(검사할 데이터의 개수를 줄일 수 있음)*

-------

##  LISTAGG 이용

`LISTAGG([합칠컬럼명] ,'구분자') WITHIN GROUP(ORDER BY [정렬컬럼명])`

```sql
WITH NUMBERS AS (SELECT  LEVEL AS NUM
FROM    DUAL
WHERE   LEVEL > 1
CONNECT BY LEVEL <=1000)
SELECT  LISTAGG(N.NUM, '&') WITHIN GROUP(ORDER BY N.NUM)
FROM    NUMBERS N
WHERE   NOT EXISTS (SELECT  E.NUM
                    FROM    NUMBERS E
                    WHERE   E.NUM <= SQRT(N.NUM)
                    AND MOD(N.NUM , E.NUM)= 0);
```

---------

## 결과

```txt
2&3&5&7&11&13&17&19&23&29&31&37&41&43&47&53&59&61&67&71&73&79&83&89&97&101&103&107&109&113&127&131&137&139&149&151&157&163&167&173&179&181&191&193&197&199&211&223&227&229&233&239&241&251&257&263&269&271&277&281&283&293&307&311&313&317&331&337&347&349&353&359&367&373&379&383&389&397&401&409&419&421&431&433&439&443&449&457&461&463&467&479&487&491&499&503&509&521&523&541&547&557&563&569&571&577&587&593&599&601&607&613&617&619&631&641&643&647&653&659&661&673&677&683&691&701&709&719&727&733&739&743&751&757&761&769&773&787&797&809&811&821&823&827&829&839&853&857&859&863&877&881&883&887&907&911&919&929&937&941&947&953&967&971&977&983&991&997
```

