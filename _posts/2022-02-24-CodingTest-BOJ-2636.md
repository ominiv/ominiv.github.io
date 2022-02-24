---
title: Python/BFS BOJ-2636 치즈
date: 2022-02-24 00:00:01
categories:
- CodingTest
tags:
- BFS
- 오답노트
---

# [Python/BFS] BOJ-2636 치즈

📌[문제링크](https://www.acmicpc.net/problem/2636) 

공기 중에서 치즈가 모두 녹아 없어지는 데 걸리는 시간, 녹기 한시간전에 남아있는 치즈조각의 칸의 수 구하는 문제다. <br> 치즈안에 구명은 공기라고 간주하지 않는다.

치즈안에 구멍과 외부 공기를 분리하는 게 중요하다.<br>무조건 0,0은 공기이므로 bfs(0,0)으로 외부공기를 체크해주면 된다.


---

## BFS solution
```python
import sys
input = sys.stdin.readline
from collections import deque

def outside(x,y):
    global visited
    queue = deque([(x,y)])
    board[x][y]=-1
    visited[x][y] = True
    while queue :
        x,y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0 <= nx <N and 0 <= ny <M :
                if board[nx][ny] != 1 and not visited[nx][ny] :
                    visited[nx][ny]=True
                    board[nx][ny]= -1
                    queue.append((nx,ny))

def bfs(x,y):
    global visited ,melt
    queue = deque([(x,y)])
    visited[x][y] = True
    while queue :
        x,y = queue.popleft()
        cnt=0
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0 <= nx <N and 0 <= ny <M :
                if board[nx][ny] == 1 and not visited[nx][ny] :
                    visited[nx][ny]=True
                    queue.append((nx,ny))
                if board[nx][ny]== -1 and not visited[nx][ny]: # 다음칸이 빈칸이라면 1시간 후에 치즈 녹음
                    cnt=1
        if cnt == 1: 
            melt.append((x,y))


if __name__ == '__main__' :
    N,M = map(int,input().split()) # 행 / 열
    board = [list(map(int,input().split())) for _ in range(N)]
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]
    time,cnt = 0,0 
    while True :
        time +=1
        melt=deque([])
        visited= [[False]*M for _ in range(N)]
        # 외부공기 체크
        outside(0,0)
        visited= [[False]*M for _ in range(N)]
        # 녹는 치즈 위치 체크
        for x in range(N):
            for y in range(M):
                if board[x][y] == 1 and not visited[x][y]:
                    bfs(x,y)
        if len(melt) == 0 :
            print(time-1)
            print(cnt)
            break
        else : 
            cnt = len(melt)
        # 녹이기
        for x,y in melt :
            board[x][y] = -1

```
