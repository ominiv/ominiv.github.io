---
title: Python/Greedy BOJ-1931 회의실 배정
date: 2021-12-28 23:30:09
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-1931 회의실 배정

📌[문제링크](https://www.acmicpc.net/problem/1931)

  <BR>

하나의 회의실에서 최대로 회의를 할 수 있는 경우를 출력하면된다.

✔ 가장 중요한 포인트는 **끝나는 시간, 시작하는 시간 순으로 오름차순 정렬**을 하면된다.<br>아래 예시를 보면 (4,4) -> (1,4) 회의는 진행 할 수 없지만, (1,4) -> (4.4) 회의는 진행 할 수 있다.<br>(4,4) <br>(1,4)

<br>

```python
N = int(input()) # 회의의 수
TimeTable = []
for _ in range(N):
    start, end = map(int,input().split())
    TimeTable.append([start, end])

# 끝나는 시간, 시작시간 순으로 정렬
TimeTable = sorted(TimeTable, key = lambda x : (x[1],x[0]))

cnt = 1
end =TimeTable[0][1]
for i in range(N-1):
    if TimeTable[i+1][0] >= end :
        end =TimeTable[i+1][1]    
        cnt +=1

print(cnt)
```

