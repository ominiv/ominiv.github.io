---
title: Python/BFS BOJ-4963 섬의개수
date: 2022-02-04 00:00:01
categories:
- CodingTest
tags:
- BFS
---

# [Python/BFS] BOJ-4963 섬의개수

📌[문제링크](https://www.acmicpc.net/problem/4963)

섬의 개수를 세는 문제다.<br>상하좌우 + **대각선 4방향**까지 고려해서 BFS로 탐색을 하면된다.

---

## BFS solution
```python
import sys
input = sys.stdin.readline

def bfs(x,y,cnt) :
    global visited
    visited[x][y]=cnt
    q = [(x,y)]
    while q :
        x,y = q.pop(0)
        for i in range(8) :
            nx = x + dx[i]
            ny = y + dy[i]
            if 0<=nx<H and 0<=ny<W and board[nx][ny]==1 :
                if not visited[nx][ny] :
                    visited[nx][ny]=cnt
                    q.append((nx,ny))


if __name__ == '__main__' :
    while 1:
        W,H = map(int,input().split())
        if W == 0 and H == 0 : # 프로그램 종료
            break
        board = [list(map(int,input().split())) for _ in range(H)]
        # 상하좌우 + 대각선 4방향
        dx = [-1,1,0,0,-1,-1,1,1]
        dy = [0,0,-1,1,1,-1,1,-1]
        visited = [[0]*W for _ in range(H)]
        cnt=0
        for x in range(H) :
            for y in range(W) :
                if board[x][y] and visited[x][y]==0 :
                    cnt +=1
                    bfs(x,y,cnt)
        print(cnt)
```
