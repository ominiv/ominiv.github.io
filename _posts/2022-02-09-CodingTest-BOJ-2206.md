---
title: Python/BFS BOJ-2206 벽부수고 이동하기 
date: 2022-02-09 00:00:01
categories:
- CodingTest
tags:
- BFS
- 오답노트
---

# [Python/BFS] BOJ-2206 벽부수고 이동하기 

📌[문제링크](https://www.acmicpc.net/problem/2206)

맵이 주어졌을 때, 최단 경로를 구해 내는 문제다. 벽을 1번까지 부술 수 있다. (안부셔도 된다.) <br>3차원으로 접근하면 쉽게 풀 수 있다. 

---

## BFS solution
```python
import sys
from collections import deque
input = sys.stdin.readline
sys.setrecursionlimit(10**6)

def bfs(x,y,wall) :
    q =deque([(x,y,wall)])
    visited[x][y][wall] =1
    while q:
        x,y,wall = q.popleft()
        if x==N-1 and y ==M-1 :
            return visited[x][y][wall]
        for i in range(4):
            nx = x+ dx[i]
            ny = y+ dy[i]
            if 0 <= nx < N and 0<= ny < M and visited[nx][ny][wall]==0:
                if board[nx][ny]==0 : 
                    visited[nx][ny][wall] = visited[x][y][wall]+1
                    q.append((nx,ny,wall))
                # 벽을 부순적없고 다음칸이 벽인 경우
                elif board[nx][ny]==1 and wall==0 : 
                    visited[nx][ny][1] = visited[x][y][wall]+1
                    q.append((nx,ny,1))
    return -1


if __name__ =='__main__' :
    N,M = map(int,input().split()) # N 행 / M 열
    board = [list(map(int,input().rstrip())) for _ in range(N)]
    visited = [[[0]*2 for _ in range(M)] for _ in range(N)] 
    dx =[-1,1,0,0]
    dy =[0,0,-1,1]
    res= bfs(0,0,0)
    print(res)

```
---
## 회고
나는 너무 비효율적으로 접근했다ㅋㅋㅋㅋ<br>벽의 개수만큼 반복해서 각 벽을 없앤후 거리를 찾아서 최소거리를 계산했다. 결과는 볼 것 도없이 시간초과 ㅠ 음.. 알것같다고 무작정 덤비지 말고 더 좋은 방법이 있는지 고민하자. 
