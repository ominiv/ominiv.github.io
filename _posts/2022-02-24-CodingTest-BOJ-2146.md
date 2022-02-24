---
title: Python/BFS BOJ-2146 다리만들기
date: 2022-02-24 00:00:01
categories:
- CodingTest
tags:
- BFS

---

# [Python/BFS] BOJ-2146 다리만들기

📌[문제링크](https://www.acmicpc.net/problem/2146) 

섬들간의 최단 거리의 다리를 만들면 된다. 

1. 각 섬들을 label을 붙여준다. (섬을 구분할 수 있도록)
2. 현재 위치한 섬에서 다른 섬까지의 최소 0의 수를 구한다.

---

## BFS solution
```python
import sys
input = sys.stdin.readline
from collections import deque

def bfs(x,y,name):
    queue = deque([(x,y)])
    visited = [[False]*N for _ in range(N)]
    visited[x][y] = 1
    while queue :
        x,y =queue.popleft()
        for i  in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0<= nx < N and 0<= ny < N :
                if not visited[nx][ny] and board[x][y]==0 and board[nx][ny]!=name and board[nx][ny] > 0: # 다른섬에 도착한 경우 멈춤
                    return visited[x][y]-1
                if not visited[nx][ny] and board[nx][ny]==0: 
                    visited[nx][ny]=visited[x][y]+1
                    queue.append((nx,ny))
    return visited[x][y]-1

def label(x,y,cnt):
    global visited
    queue = deque([(x,y)])
    board[x][y]=cnt
    visited[x][y] = True
    while queue :
        x,y =queue.popleft()
        for i  in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0<= nx < N and 0<= ny < N :
                if not visited[nx][ny] and board[nx][ny]==1:
                    visited[nx][ny]=True
                    board[nx][ny]=cnt
                    queue.append((nx,ny))


if __name__ == '__main__':
    N = int(input())
    board = [list(map(int,input().split())) for _ in range(N)]
    dx =[-1,1,0,0]
    dy =[0,0,-1,1]
    res = sys.maxsize
    visited = [[False]*N for _ in range(N)]
    # 섬 라벨링
    cnt = 0 
    for x in range(N):
        for y in range(N):
            if board[x][y]==1 and not visited[x][y]:
                cnt+=1
                label(x,y,cnt)
    # 최소 0 체크
    for x in range(N):
        for y in range(N):
            if board[x][y]>0:
                tmp = bfs(x,y,board[x][y]) # x,y,섬라벨
                if tmp > 0 :
                    res= min(res, tmp)
    print(res)

```
