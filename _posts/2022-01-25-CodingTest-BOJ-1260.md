---
title: Python/DFS-BFS BOJ-1260 DFS와 BFS
date: 2022-01-25 00:00:01
categories:
- CodingTest
tags:
- DFS
- BFS
---

# [Python/DFS-BFS] BOJ-1260 DFS와 BFS

📌[문제링크](https://www.acmicpc.net/problem/1260) [jokerldg님의 풀이링크](https://jokerldg.github.io/algorithm/2021/03/22/dfs-bfs.html)<br>***풀이링크 들어가셔서 보시면 됩니다.**

DFS 와 BFS의 차이점을 알 수 있는 간단한 문제다. <br>처음엔 input이 그래프 형태가 아니라서 당황해서 구글링을 했다. ^-^z<br>**인접행렬**을 만들어서 숫자의 연결을 체크하면 된다. 

**요소 끝부분을 접근할때는 collections.deque를 사용하자.<br>list의 pop보다 빠르다.**

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
        v = queue.popleft() #0번째 요소 뱉기
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
