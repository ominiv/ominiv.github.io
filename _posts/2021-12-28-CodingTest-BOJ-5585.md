---
title: Python/Greedy BOJ-5585 거스름돈
date: 2021-12-27 23:30:09
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-5585 거스름돈

📌[문제링크](https://www.acmicpc.net/problem/5585)

  <BR>

단위가 큰 화폐부터 차감하면서 거스름돈 수를 세면 된다.

<br>

```python
cost = int(input())
380

N = (1000 - cost) ; cnt=0
while 1 :
    if N >= 500 :
        cnt += N // 500
        N = N%500
    elif N >= 100 :
        cnt += N // 100
        N = N%100
    elif N >= 50 :
        cnt += N // 50
        N = N%50    
    elif N >= 10 :
        cnt += N // 10
        N = N%10
    elif N >= 5 :
        cnt += N // 5
        N = N%5
    elif N >= 1 :
        cnt += N // 1
        N = N%1
    if N==0 :
        break
print(cnt)

```

