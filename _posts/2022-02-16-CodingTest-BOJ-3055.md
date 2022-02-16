---
title: Python/BFS BOJ-3055 탈출
date: 2022-02-15 00:00:01
categories:
- CodingTest
tags:
- BFS
- 오답노트
---

# [Python/BFS] BOJ-3055 탈출

📌[문제링크](https://www.acmicpc.net/problem/3055)

고슴도치가 비버굴에 가는 최소시간을 구하는 문제다. 추가로 매분마다 인접한 빈곳으로 물이 차오른다. 

1. 물이 차오르는 시간 계산
2. 시간을 고려해 고슴도치가 비버굴에 가는 최소시간을 계산

---

## BFS solution
```python
import sys
from collections import deque

if __name__ =='__main__':
    R,C = map(int,input().split())
    board = [list(map(str, input().rstrip())) for _ in range(R)]
    visited = [[False]*C for _ in range(R)]
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]
    queue = deque()
    for x in range(R):
        for y in range(C):
            if board[x][y]=='D':
                goal = [x,y]
                board[x][y] = sys.maxsize
            elif board[x][y]=='S':
                start = [x,y,0]
                board[x][y]=0
            elif board[x][y]=='*':
                board[x][y]=0
                queue.append([x,y,0])
            elif board[x][y]=='X':
                visited[x][y]=True
    # 물이 차오르는 시간체크
    while queue:
        x,y,cnt = queue.popleft()
        for i in range(4):
            nx = x +dx[i]
            ny = y +dy[i]
            if 0<= nx < R and 0 <= ny < C and board[nx][ny]=='.':
                board[nx][ny] = cnt +1
                queue.append([nx,ny,cnt+1])
    # 고슴도치 이동경로 체크
    queue.append(start)
    visited[start[0]][start[1]] =True
    flag= False
    while queue :
        x,y,cnt = queue.popleft()
        if goal == [x,y]:
            flag=True
            break
        for i in range(4):
            nx = x +dx[i]
            ny = y +dy[i]
            if 0<= nx < R and 0 <= ny < C and not visited[nx][ny]:
                if board[nx][ny] == '.' or board[nx][ny] > cnt+1 :
                    visited[nx][ny]=True
                    queue.append([nx,ny,cnt+1])
    if flag:
        print(cnt)
    else :
        print('KAKTUS')
```
