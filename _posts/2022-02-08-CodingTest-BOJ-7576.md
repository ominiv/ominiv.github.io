---
title: Python/BFS BOJ-7576 토마토
date: 2022-02-08 00:00:01
categories:
- CodingTest
tags:
- BFS
- 3차원
---

# [Python/BFS] BOJ-7576 토마토

📌[문제링크](https://www.acmicpc.net/problem/7576)


창고에 보관된 토마토들이 며칠이 지나면 다 익게 되는지, 그 최소 일수를 구하는 문제다.<bR>
정수 1은 익은 토마토, 정수 0은 익지 않은 토마토, 정수 -1은 빈곳을 의미한다.

**박스에 완숙토마토 위치를 큐에 담아서 진행하면된다.**

---

## BFS solution
```python

import sys
from collections import deque
sys.setrecursionlimit(10 ** 6)
input = sys.stdin.readline

def bfs() :
    global board
    global visited
    global result
    while q  :
        x,y = q.popleft()
        for i in range(4) :
            nx = x + dx[i]
            ny = y + dy[i]
            if 0 <= nx < M and 0 <= ny < N :
                if board[nx][ny] == 0 and visited[nx][ny]==0:
                    # **토마토를 익히는데 시간은 1일이 걸린다.
                    board[nx][ny] =  board[x][y] + 1
                    visited[nx][ny]= 1
                    q.append((nx,ny))


if __name__ == '__main__' :
    N,M = map(int,input().split()) # M 행 / N 열  
    board = [list(map(int,input().split())) for _ in range(M)]
    visited = [[0]*N for _ in range(M)]
    dx = [-1,1,0,0]
    dy=[0,0,-1,1]
    result = 0
    q = deque()
    for x in range(M):
        for y in range(N):
            if board[x][y]==1 :
                visited[x][y]=1
                q.append((x,y))
    bfs()

    # 토마토를 채우는데 소요한 시간 체크
    for b in board :
        for i in b :
            if i == 0 :
                # 익지않은 토마토가 있는경우 -1 뱉음
                print(-1)
                exit(0)
        result = max(result, max(b))
    print(result-1)

```
