---
title: Python/Greedy BOJ-2217 로프
date: 2021-12-28 23:30:09
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-2217 로프

📌[문제링크](https://www.acmicpc.net/problem/2217)

  <BR>

N번째로 큰 수에 N을 곱한 값을 계산해서 가장 큰 값을 추출  하면 된다.

예를들어 15 rope와 10 rope가 존재할때 <br>15 rope는 15를 버틸 수 있고 10 rope에서는 10을 버티지 못하기 때문에 최대 중량은 15이다. <br>**10 rope는 10를 버틸 수 있고 15 rope에서도 10을 버틸 수 있기 때문에**  최대 중량은 20이다.

<br>

```python
N=int(input())
rope = []
for _ in range(N):
    rope.append(int(input()))
rope = sorted(rope, reverse=True)
result=0
for i in range(len(rope)) :
    tmp = rope[i]*(i+1)
    result = max(tmp,result)
print(result)
```

