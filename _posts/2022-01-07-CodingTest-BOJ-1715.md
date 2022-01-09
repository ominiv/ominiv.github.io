---
title: Python/Greedy BOJ-1715 카드정렬하기
date: 2022-01-07 00:00:01
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-1715 카드정렬하기

📌[문제링크 ](https://www.acmicpc.net/problem/1715)

최소한의 횟수를 구하는 문제다. <Br>리스트내에서 가장작은 2개 수를 비교하면된다.

데이터를 정렬된 상태로 저장하는 heapq모듈을 이용하면 편하다.<br>`heapq.heappop` : heap에서 가장 작은 원소를 pop & 리턴. 비어 있는 경우 IndexError가 호출됨.

---

## solution
```python
import sys,copy,heapq
input = sys.stdin.readline

if __name__=='__main__' :
    N = int(input())
    num = [int(input()) for _ in range(N)]
    num=sorted(num)
    q = copy.deepcopy(num)
    sumv,result = 0,0
    while len(q) >1 :
        # print(q)
        sumv = (heapq.heappop(q)+heapq.heappop(q))
        result += sumv
        q.append(sumv)
    print(result)
```

sorted를 2차례 써서인지 시간초과가 났다.
```python
import sys,copy
input = sys.stdin.readline

if __name__=='__main__' :
    N = int(input())
    num = [int(input()) for _ in range(N)]
    num=sorted(num,reverse=True)
    q = copy.deepcopy(num)
    sumv,result = 0,0
    while len(q) >1 :
        # print(q)
        sumv = (q.pop()+q.pop())
        result += sumv
        q.append(sumv)
        q = sorted(q,reverse=True)
    print(result)
```
