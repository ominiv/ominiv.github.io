---
title: Python/Greedy BOJ-1026 보물
date: 2021-12-28 23:30:09
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-1026 보물

📌[문제링크](https://www.acmicpc.net/problem/1026)

  <BR>

S 값을 최소로 하기 위해 A의 수를 재배열 하자<br>`S = A[0]B[0] + ---  A[N-1]B[N-1] `

**A를 오름차순으로 정렬,  B를 내림차순으로 정렬**한 값을 이용하면 최소값을 얻을 수 있다.

<br>

```python
if __name__ == '__main__' :
    N = int(input())
    A = list(map(int,input().split()))
    B = list(map(int,input().split()))
    A.sort()
    B.sort(reverse=True)
    print(sum([A[i]*B[i] for i in range(N)]))
```

