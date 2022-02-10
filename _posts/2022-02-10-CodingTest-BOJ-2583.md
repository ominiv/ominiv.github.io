---
title: Python/BFS BOJ-2583 영역 구하기 
date: 2022-02-10 00:00:01
categories:
- CodingTest
tags:
- BFS
---

# [Python/BFS] BOJ-2583 영역 구하기 

📌[문제링크](https://www.acmicpc.net/problem/2583)

board에 블록이 위치한 장소만 잘 체크하면 된다. <br>
결과를 오름차순으로 정렬하면 되서 굳이 영역을 예시와 동일하게 만들 필요는 없다. (상하좌우 대칭 상관없이 풀이가능)

---

## BFS solution
```python
from collections import deque
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**6)

def bfs(x,y):
    global board
    global visited
    q = deque([(x,y)])
    visited[x][y] = 1
    cnt =0
    while q:
        x,y = q.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0 <= nx < M and 0<=ny < N :
                if board[nx][ny]==0 and visited[nx][ny]==0 :
                    #넓이를 구해야되므로 새로운 곳 방문할때 마다 +1 
                    cnt +=1 
                    board[nx][ny] = cnt
                    visited[nx][ny]=1
                    q.append((nx,ny))
    return board[x][y]+1

if __name__ == '__main__' :
    M,N,K =map(int,input().split()) # M 행 / N 열 
    points = deque([]) 
    for _ in range(K):
        x0,y0,x1,y1= map(int,input().split())
        points.append((x0,y0,x1,y1))
    board = [[0]*N for _ in range(M)]
    visited = [[0]*N for _ in range(M)]
    # board에 영역 채우기
    while points:
        x0,y0,x1,y1 = points.popleft()
        for x in range(M):
            for y in range(N):
                if x0 <= y < x1 and y0 <= x < y1 :
                    board[(M-1)-x][y]=1
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]
    res = []
    # 빈 영역이 몇개고 넓이가 얼마인지 체크
    for y in range(N):
        for x in range(M):
            if board[x][y]==0 and visited[x][y]==0 :
                res.append(bfs(x,y))
    print(len(res))
    res = sorted(res)
    for _ in res :
        print(_, end = ' ')

```
