---
title: Python/DFS BOJ-2667 단지번호 붙이기
date: 2022-01-24 00:00:01
categories:
- CodingTest
tags:
- DFS
- Heapq
---

# [Python/DFS] BOJ-2667 단지번호 붙이기

📌[문제링크 ](https://www.acmicpc.net/problem/2667)

총 단지수 와 각 단지내 집의 수를 오름차순 출력하는 문제다.<br>DFS, BFS 둘다 풀어도된다.

---

## solution
```python

import sys
input = sys.stdin.readline

def bfs(x,y,total):
    global board,visited,dx,dy,num
    for i in range(4):
        nx = x+dx[i]
        ny = y+dy[i]
        if 0<=nx<N and 0<=ny<N :
            if board[nx][ny] == 1 and visited[nx][ny]==0:
                visited[nx][ny] = total; num+=1
                bfs(nx,ny,total)

if __name__ =='__main__':
    N = int(input())
    board = [list(map(int,input().rstrip())) for _ in range(N)]
    visited = [[0]*N for _ in range(N)]
    dx=[-1,1,0,0]; dy=[0,0,-1,1];total=0
    num_list=[]
    for x in range(N):
        for y in range(N):
            if board[x][y] == 1 and visited[x][y]==0:
                total +=1 #단지 수 체크
                num=1 # 단지내 집의 수 체크
                visited[x][y] = total
                bfs(x,y,total)
                num_list.append(num)
    num_list.sort() #오름차순 정렬
    print(total)
    for i in range(total):
        print(num_list[i]) 

```
