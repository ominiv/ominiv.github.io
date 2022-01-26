---
title: Python/DFS-BFS BOJ-2606 바이러스
date: 2022-01-26 00:00:01
categories:
- CodingTest
tags:
- DFS
- BFS
---

# [Python/DFS-BFS] BOJ-2606 바이러스

📌[문제링크](https://www.acmicpc.net/problem/2606) 

BFS나 DFS 알고리즘을 알고있다면 쉬운 문제다. 인접행렬을 만들어보자<br> 그리고 BFS는 큐/ DFS는 재귀를 기억하자.

---

## BFS solution
```python
import sys
input = sys.stdin.readline

if __name__ == '__main__':
    N=int(input())
    M=int(input())
    board = [[0]*(N+1) for _ in range(N+1)] # index 맞추기위해서 N+1 만큼 생성
    for i in range(M):
        a,b=map(int,input().split())
        board[a][b],board[b][a] = 1,1
    visited=[1]
    queue=[1]
    while queue :
        r = queue.pop(0)
        for c in range(len(board[r])):
            if board[r][c]==1 and c not in visited:
                visited.append(c)
                queue.append(c)
    print(len(visited)-1) #1번 컴퓨터 제외
```

---

## DFS solution
```python
import sys
input = sys.stdin.readline

def dfs(r,visited):
    global board
    visited.append(r)
    for c in range(len(board[r])):
        if board[r][c] == 1 and c not in visited :
            dfs(c,visited)
    return visited

if __name__ == '__main__':
    N=int(input())
    M=int(input())
    board = [[0]*(N+1) for _ in range(N+1)] # index 맞추기위해서 N+1 만큼 생성
    for i in range(M):
        a,b=map(int,input().split())
        board[a][b],board[b][a] = 1,1
    visited= dfs(1,visited=[])
    print(len(visited)-1) #1번 컴퓨터 제외

```