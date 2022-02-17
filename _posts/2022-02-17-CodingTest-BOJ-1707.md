---
title: Python/DFS-BFS BOJ-1707 이분그래프
date: 2022-02-17 00:00:01
categories:
- CodingTest
tags:
- DFS
- BFS
- 오답노트
---

# [Python/DFS-BFS] BOJ-1707 이분그래프

📌[문제링크](https://www.acmicpc.net/problem/1707)

이분그래프인지 아닌지 판단하는 문제다.<br> 여기서 이분그래프란, 그래프 정점들을 두 그룹으로 나누었을때 각 그룹내 간선이 존재하지 않는 경우다. **각 그룹내 간선이 존재하는 지 아닌 지를 판단하자.**

---

## DFS solution
```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**9)

def dfs(i,num):
    visited[i]=num
    for b in board[i]:
        if visited[b]==0:
            dfs(b,-num)
    return

if __name__ =='__main__' :
    K = int(input())
    for _ in range(K):
        V,E = map(int,input().split()) # 정점/ 간선
        board = [[] for _ in range(V)]
        visited = [0]*V
        pos = [1]*V
        for i in range(E):
            x,y = map(int,input().split())
            board[x-1].append(y-1)
            board[y-1].append(x-1)
        for i in range(V):
            if visited[i] == 0 :
                dfs(i,1)
        flag=[]
        for i in range(V):
            for j in board[i] :
                if visited[i]==-visited[j]:
                    flag.append(True)
                else :
                    flag.append(False)
        if all(flag) : 
            print('YES')
        else :
            print('NO')

```
## BFS solution
```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**9)

def bfs(x):
    visited[x] = 1
    queue = [x]
    while queue :
        nx = queue.pop(0)
        for b in board[nx]:
            if visited[b]==0:
                visited[b]=-visited[nx]
                queue.append(b)
            elif visited[b]==visited[nx]:
                return False
    return True

if __name__ =='__main__':
    K = int(input())
    for _ in range(K) :
        V,E = map(int,input().split())
        board= [[] for _ in range(V)]
        visited = [0]*V
        for i in range(E):
            x,y = map(int,input().split())
            board[x-1].append(y-1)
            board[y-1].append(x-1)
        res= 'YES'
        for x in range(V):
            if visited[x]==0 :
                if not bfs(x) :
                    res='NO'
                    break
        print(res)
```