---
title: Python/BFS BOJ-2573 ๋น์ฐ
date: 2022-02-17 00:00:01
categories:
- CodingTest
tags:
- BFS
---

# [Python/BFS] BOJ-2573 ๋น์ฐ

๐[๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/2573)

๋น์ฐ์ด ๋๊ฐ๋ก ์ด์์ผ๋ก ๋ถ๋ฆฌ๋ ๋์ ์๊ฐ์ ๊ตฌํ๋ฉด ๋๋ค.<BR>์ฌ๊ธฐ์ ๊ด๊ฑด์ ๋น์ฐ์ ๋ฐ๋ค์ ์ธ์ ํ ๋ฉด์ ์ ๋งํผ ๋น๋๋ค. ๊ทธ๋ฌ๋ฏ๋ก BFS๋ก ๊ฐ ๋น์ฐ์ ๋ฐฉ๋ฌธํด์ ๋น์ผ์์น์ ๋น์ผ ์์ ์ฒดํฌํ๋ฉด๋๋ ๋๋ค!

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
        # ๋น์ผ์์น ํ์ธ & ์์ญ ์ธ๊ธฐ
        res=0
        for x in range(N):
            for y in range(M):
                if board[x][y] > 0 and not visited[x][y]:
                    res+=melt(x,y)
        # ๋น์ด๊ธฐ
        for x,y,cnt in melt_region:
            if board[x][y] < cnt :
                board[x][y] = 0
            else :
                board[x][y] -=cnt
        if res > 1 : # 2๊ฐ ์ด์์ผ๋ก ๋ถ๋ฆฌ๋ ๊ฒฝ์ฐ 
            print(time)
            break
        elif res==0 : # ๋ค ๋น์๋ ๊น์ง ๋ถ๋ฆฌ๊ฐ ๋์ง ์๋ ๊ฒฝ์ฐ
            print(0)
            break
        time +=1

```
