---
title: Python/BFS BOJ-7569 토마토 3차원
date: 2022-02-08 00:00:01
categories:
- CodingTest
tags:
- BFS
---

# [Python/BFS] BOJ-7569 토마토 3차원

📌[문제링크](https://www.acmicpc.net/problem/7569)


창고에 보관된 토마토들이 며칠이 지나면 다 익게 되는지, 그 최소 일수를 구하는 문제다.<bR>
3차원이라 어렵게 느껴지지만 쉽게 풀수있다.

**2차원과 마찬가지로 박스에 완숙토마토 위치를 큐에 담아서 진행하면된다. (x,y,z)를 체크!**

---

## BFS solution
```python
from collections import deque
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**6)

def bfs():
    global board
    global visited
    while q :
        z,x,y = q.popleft()
        for i in range(6):
            nx = x + dx[i]
            ny = y + dy[i]
            nz = z + dz[i]
            if 0 <= nx < N and 0 <= ny < M and 0 <= nz < H :
                if board[nz][nx][ny] == 0 and visited[nz][nx][ny]==0 :
                    board[nz][nx][ny] = board[z][x][y] + 1
                    visited[nz][nx][ny] = 1
                    q.append((nz,nx,ny))

if __name__ == '__main__' :
    M,N,H = map(int,input().split()) # M 열 / N 행 / H 높이
    board = [[list(map(int,input().split())) for _ in range(N)] for _ in range(H)]
    visited = [[[0]*M for _ in range(N)] for _ in range(H)]
    result =0
    # 위 아래 상 하 좌 우
    dx = [0,0,-1,1,0,0]
    dy = [0,0,0,0,-1,1]
    dz = [1,-1,0,0,0,0]
    q =deque()
    # 완숙 토마토 위치 찾기
    for z in range(H):
        for x in range(N):
            for y in range(M) :
                if board[z][x][y] == 1 :
                    visited[z][x][y] = 1 
                    q.append((z,x,y))
    bfs()
    # 토마토를 채우는데 소요한 시간 체크
    for z in range(H):
        for x in range(N):  
            for y in range(M) :
                # 익지않은 토마토 존재할 경우 -1 뱉기
                if board[z][x][y] == 0 :
                    print(-1)
                    exit(0)
            result = max(result,max(board[z][x]))
    print(result-1)

```
