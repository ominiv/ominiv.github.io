---
title: Python/BFS BOJ-2589 보물섬
date: 2022-02-24 00:00:01
categories:
- CodingTest
tags:
- BFS
- 오답노트
---

# [Python/BFS] BOJ-2589 보물섬

📌[문제링크](https://www.acmicpc.net/problem/2589) 

보물은 서로 간에 최단 거리로 이동하는데 있어 가장 긴 시간이 걸리는 육지 두 곳에 나뉘어 묻혀있다.<br>보물이 묻혀 있는 두 곳 간의 최단 거리로 이동하는 시간을 구하면된다. 

---

## BFS solution
```python
import sys
from collections import deque
input = sys.stdin.readline

def bfs(x,y) :
    visited = [[False]*M for _ in range(N)]
    visited[x][y] = 1
    queue = deque([(x,y)])
    while queue :
        x, y = queue.popleft()
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if 0 <= nx < N and 0 <= ny <M :
                if board[nx][ny]=='L' and not visited[nx][ny]:
                    visited[nx][ny] = visited[x][y]+1
                    queue.append((nx,ny))
    return visited[x][y]-1

if __name__ == '__main__':
    N, M = map(int,input().split())
    board = [list(map(str, input().rstrip())) for _ in range(N)]
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]
    result = -sys.maxsize
    for x in range(N):
        for y in range(M):
            if board[x][y]=='L' : # 각 위치에서 최장거리 체크
                result = max(bfs(x,y), result)
    print(result)

```
