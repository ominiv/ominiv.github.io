---
title: Python/DFS-BFS BOJ-1012 유기농 배추
date: 2022-01-26 00:00:01
categories:
- CodingTest
tags:
- DFS
- BFS
---

# [Python/DFS-BFS] BOJ-1012 유기농 배추

📌[문제링크](https://www.acmicpc.net/problem/1012) 

BFS나 DFS 알고리즘을 알고있다면 쉬운 문제다.<br>x,y가 반대여서 헷갈렸다. BFS는 큐/ DFS는 재귀를 기억하자.

---

## BFS solution
```python
import sys
from collections import deque

def bfs(x,y,cnt):
    queue=deque()
    queue.append((x,y))
    visited[x][y] = cnt
    while queue:
        x,y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0<=nx<N and 0<=ny<M :
                if board[nx][ny] ==1 and visited[nx][ny] ==0:
                    visited[nx][ny]=cnt
                    queue.append((nx,ny))

input = sys.stdin.readline
if __name__ == '__main__':
    T = int(input())
    for _ in range(T):
        M,N,K= map(int,input().split()) # 가로/ 세로/배추수
        board = [[0]*M for i in range(N)]
        visited = [[0]*M for i in range(N)]
        for i in range(K):
            m,n = map(int,input().split())
            board[n][m]=1
        cnt = 0
        dx = [-1,1,0,0]
        dy = [0,0,-1,1]
        for x in range(N):
            for y in range(M):
                if board[x][y]==1 and visited[x][y]==0:
                    cnt = cnt+1
                    bfs(x,y,cnt)
        print(cnt)

```

---

## DFS solution
```python
import sys 
sys.setrecursionlimit(100000) # 재귀 limit 늘려주기
input = sys.stdin.readline

def dfs(x,y,cnt):
    visited[x][y]=cnt
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0<=nx<N and 0<=ny<M :
            if board[nx][ny] ==1 and visited[nx][ny] ==0:
                visited[nx][ny]=cnt
                dfs(nx,ny,cnt)

if __name__ == '__main__':
    T = int(input())
    for _ in range(T):
        M,N,K= map(int,input().split()) # 가로/ 세로/배추수
        board = [[0]*M for i in range(N)]
        visited = [[0]*M for i in range(N)]
        for i in range(K):
            m,n = map(int,input().split())
            board[n][m]=1
        cnt = 0
        dx = [-1,1,0,0]
        dy = [0,0,-1,1]
        for x in range(N):
            for y in range(M):
                if board[x][y]==1 and visited[x][y]==0:
                    cnt = cnt+1
                    # bfs(x,y,cnt)
                    dfs(x,y,cnt)
        print(cnt)


```