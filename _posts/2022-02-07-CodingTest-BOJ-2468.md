---
title: Python/BFS BOJ-2468 안전영역
date: 2022-02-07 00:00:01
categories:
- CodingTest
tags:
- BFS
---

# [Python/BFS] BOJ-2468 안전영역

📌[문제링크](https://www.acmicpc.net/problem/2468)

비의 양에 따른 모든 경우를 조사해 물에 잠기지 않는 안전한 영역의 개수 중에서 최대인 경우를 구하는 문제다. <br>내릴 수 있는 비의 양 만큼 반복하여 최대영역을 구하면 된다.

비가 오지 않을 경우를 놓지지말자!

---

## BFS solution
```python
import sys ,copy
input = sys.stdin.readline

def bfs(x,y,cnt):
    global cboard
    cboard[x][y] = cnt
    visited[x][y] =1
    q = [(x,y)]
    while q :
        x,y=q.pop(0)
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0<=nx<N and 0<=ny<N :
                if cboard[nx][ny] != 0 and visited[nx][ny]==0 :
                    cboard[nx][ny] = cnt
                    visited[nx][ny] =1
                    q.append((nx,ny))

if __name__ == '__main__' :
    N = int(input())
    board = [list(map(int, input().split())) for _ in range(N)]
    maxv= board[0][0]
    result = 0
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]
    # 높이 최대값 찾기
    for i in board:
        if maxv < max(i):
            maxv = max(i)
    # 높이만큼 반복 (1-100) 
    # 비가 안올경우 0 추가해주기
    for i in range(maxv,-1,-1): 
        cboard = copy.deepcopy(board)
        visited = [[0]*N for _ in range(N)]
        zerocnt=0
        # 잠기는 장소 체크
        for x in range(N) :
            for y in range(N) :
                if cboard[x][y] <= i :
                    zerocnt +=1
                    cboard[x][y] = 0
        if zerocnt==N*N :
            cnt = 0
        elif zerocnt==0 :
            cnt = 1
        else :
            # 최대영역 체크
            cnt=0 
            for x in range(N) :
                for y in range(N) :
                    if cboard[x][y] != 0 and visited[x][y]==0 :
                        cnt+=1
                        bfs(x,y,cnt)
        result=max(result,cnt)
    print(result)

```
