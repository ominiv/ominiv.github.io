---
title: Python/BFS BOJ-2178 미로탐색
date: 2022-01-24 00:00:01
categories:
- CodingTest
tags:
- BFS
---

# [Python/BFS] BOJ-2178 미로탐색

📌[문제링크 ](https://www.acmicpc.net/problem/2178) [chancoding 님의 플이](https://chancoding.tistory.com/64)<br>***풀이링크 들어가셔서 보시면 됩니다.**

(N,M)위치 까지 도달할 최소의 칸 수를 구하는 문제다. <br>BFS방식 사용을 위해 visited matrix를 생성하고 Queue를 통해 구현을 했다. 

---

## solution
```python
import sys
input= sys.stdin.readline

if __name__=='__main__':
    N,M=map(int, input().split())
    board = [list(input().rstrip())for _ in range(N)]
    visited = [M*[0] for _ in range(N)]
    
    dx=[-1,1,0,0]
    dy=[0,0,-1,1]
    
    visited[0][0]=1
    queue=[(0,0)]
    while queue:
        x,y = queue.pop(0)
        if x==N-1 and y==M-1 :
            print(visited[x][y])
            break
        for i in range(4):
            nx=x+dx[i]
            ny=y+dy[i]
            if 0<=nx < N and 0<=ny<M :
                if visited[nx][ny]==0 and board[nx][ny]=='1':
                    print(nx,ny,visited[x][y]+1)
                    visited[nx][ny]=visited[x][y]+1
                    queue.append((nx,ny))

```
