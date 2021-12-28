---
title: Python/Greedy BOJ-2839 설탕 배달
date: 2021-12-27 23:30:09
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-2839 설탕 배달

📌[문제링크](https://www.acmicpc.net/problem/2839)

  <BR>

최소 바구니 수를 구하는 문제다. Greedy algorithm을 활용하자

5kg 바구니와 3kg 바구니가 존재한다. <br>최소 바구니수를 구하는 문제이므로 5kg을 우선적으로 고려하자.

<br>

```python
import sys
input = sys.stdin.readline

N = int(input())
18
cnt = 0
while 1 :
    if N%5 == 0:
        cnt += N//5
        break
    N-=3
    cnt+=1
    if N < 0 :
        cnt = -1
        break
```

