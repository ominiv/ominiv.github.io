---
title: Python/DFS-BFS BOJ-1260 DFS์ BFS
date: 2022-01-25 00:00:01
categories:
- CodingTest
tags:
- DFS
- BFS
---

# [Python/DFS-BFS] BOJ-1260 DFS์ BFS

๐[๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/1260) [jokerldg๋์ ํ์ด๋งํฌ](https://jokerldg.github.io/algorithm/2021/03/22/dfs-bfs.html)<br>***ํ์ด๋งํฌ ๋ค์ด๊ฐ์์ ๋ณด์๋ฉด ๋ฉ๋๋ค.**

DFS ์ BFS์ ์ฐจ์ด์ ์ ์ ์ ์๋ ๊ฐ๋จํ ๋ฌธ์ ๋ค. <br>์ฒ์์ input์ด ๊ทธ๋ํ ํํ๊ฐ ์๋๋ผ์ ๋นํฉํด์ ๊ตฌ๊ธ๋ง์ ํ๋ค. ^-^z<br>**์ธ์ ํ๋ ฌ**์ ๋ง๋ค์ด์ ์ซ์์ ์ฐ๊ฒฐ์ ์ฒดํฌํ๋ฉด ๋๋ค. 

**์์ ๋๋ถ๋ถ์ ์ ๊ทผํ ๋๋ collections.deque๋ฅผ ์ฌ์ฉํ์.<br>list์ pop๋ณด๋ค ๋น ๋ฅด๋ค.**

---

## solution
```python
from collections import deque
import sys
input = sys.stdin.readline

def dfs(start_v, visited=[]):
    global board
    visited.append(start_v)
    print(start_v,end=' ')
    for w in range(len(board[start_v])):
        if board[start_v][w]==1 and w not in visited:
            dfs(w,visited)

def bfs(start_v):
    global board
    visited = [start_v]
    queue=deque()
    queue.append(start_v)
    while queue :
        v = queue.popleft() #0๋ฒ์งธ ์์ ๋ฑ๊ธฐ
        print(v, end=' ')
        for w in range(len(board[v])):
            if board[v][w]==1 and w not in visited:
                visited.append(w)
                queue.append(w)

if __name__ =='__main__':
    N,M,V = map(int,input().split())
    board = [[0]*(N+1) for _ in range(N+1)]
    for i in range(M) :
        a,b = map(int,input().split())
        board[a][b],board[b][a]=1,1
    dfs(V)
    print()
    bfs(V)

```
