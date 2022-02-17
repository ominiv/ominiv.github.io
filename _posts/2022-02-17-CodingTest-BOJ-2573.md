---
title: Python/BFS BOJ-2573 빙산
date: 2022-02-17 00:00:01
categories:
- CodingTest
tags:
- BFS
---

# [Python/BFS] BOJ-2573 빙산

📌[문제링크](https://www.acmicpc.net/problem/2573)

빙산이 두개로 이상으로 분리될때의 시간을 구하면 된다.<BR>여기서 관건은 빙산은 바다와 인접한 면의 수 만큼 녹는다. 그러므로 BFS로 각 빙산을 방문해서 녹일위치와 녹일 양을 체크하면되는 된다!

---

## BFS solution
```python
from collections import deque
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**9)

def melt(x,y):
    queue = deque([(x,y)])
    visited[x][y]= True
    while queue:
        x,y = queue.popleft()
        cnt =0
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0<=nx < N and 0 <= ny <M and not visited[nx][ny] :
                if board[nx][ny]==0 :
                    cnt +=1
                if board[nx][ny]>0:
                    visited[nx][ny]=True
                    queue.append([nx,ny])
        melt_region.append((x,y,cnt))
    return 1

if __name__ =='__main__':
    N,M = map(int,input().split())
    board = [list(map(int,input().split())) for _ in range(N)]
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]
    time =0
    while True :
        visited = [[False]*M for _ in range(N)]
        melt_region = []
        # 녹일위치 확인 & 영역 세기
        res=0
        for x in range(N):
            for y in range(M):
                if board[x][y] > 0 and not visited[x][y]:
                    res+=melt(x,y)
        # 녹이기
        for x,y,cnt in melt_region:
            if board[x][y] < cnt :
                board[x][y] = 0
            else :
                board[x][y] -=cnt
        if res > 1 : # 2개 이상으로 분리된 경우 
            print(time)
            break
        elif res==0 : # 다 녹을때 까지 분리가 되지 않는 경우
            print(0)
            break
        time +=1

```
