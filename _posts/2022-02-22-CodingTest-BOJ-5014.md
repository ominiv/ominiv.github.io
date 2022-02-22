---
title: Python/DFS BOJ-5014 스타트링크
date: 2022-02-22 00:00:01
categories:
- CodingTest
tags:
- BFS
- 오답노트
---

# [Python/DFS] BOJ-5014 스타트링크

📌[문제링크](https://www.acmicpc.net/problem/5014) 

S층에서 G층까지 버튼을 몇번 누르면 되는지 구하는 문제다. <br> S층과 G층이 동일할경우를 놓치지 말자.

---

## BFS solution
```python
import sys
from collections import deque
input = sys.stdin.readline

if __name__ == '__main__':
    F,S,G,U,D = map( int, input().split())
    queue = deque([S])
    visited = [False]*(1000001)
    visited[S]=1
    while queue :
        s = queue.popleft()
        if s == G :
            break
        ns = s + U # 올라가는 경우
        if U > 0 and 1<=ns<=F :
            if not visited[ns] :
                queue.append(ns)
                visited[ns] = visited[s]+1
        ns = s - D # 내려가는 경우
        if D > 0 and 1<=ns<=F:
            if not visited[ns] :
                queue.append(ns)
                visited[ns] = visited[s]+1
    if visited[G] == False:
        print('use the stairs')
    else : 
        print(visited[G]-1)
```
