---
title: Python/DFS 15683 감시
date: 2021-12-15 23:30:09
categories:
- CodingTest
tags:
- DFS
---

# [Python/DFS] 15683 감시

📌[문제링크](https://www.acmicpc.net/problem/15683) [풀이참고](https://gingerkang.tistory.com/111)



나는 cctv별 회전했을 때 방향을 다 리스트에 넣고 진행하는 방법을 선택했다. 

dfs를 이용해서 최소의 사각지대의 수를 출력하면 된다. 

 **1~5 CCTV / 6 벽 / 0 빈공간**



```python

from copy import deepcopy 
import sys
input=sys.stdin.readline
INF=sys.maxsize
# 상 하 좌 우
dx = [-1,1,0,0]
dy = [0,0,-1,1]
directions = [
    [],
    [[3],[1],[2],[0]],    # 우 / 우 - 하 - 좌 - 상
    [[2,3],[0,1]],    # 좌 우 / 좌 우 - 상 하 
    [[0,3],[1,3],[1,2],[0,2]],    # 상 우 / 상 우 - 우 하 - 좌 하 - 상 좌
    [[0,2,3],[1,2,3],[0,1,2]],    # 상 좌 우 / 상 우 하 - 우 하 좌 - 상 좌 하
    [[0,1,2,3]]    # 상 하 좌 우 
]

N,M = map(int,input().split())
board = [list(map(int,input().split())) for _ in range(N)]
MIN=INF

def dfs(start,board,cctv):
    global MIN
    if start == len(cctv):
        cnt = sum([_.count(0) for _ in board])
        MIN = min(MIN, cnt)
        return
    num,x,y = cctv[start]
    for dir in directions[num]:
        tmp = deepcopy(board)
        for i in dir:
            nx,ny= x+dx[i], y+dy[i]
            while 0<=nx<N and 0<=ny<M :
                if tmp[nx][ny] == 6 :
                    break
                elif tmp[nx][ny] == 0 :
                    tmp[nx][ny] = '#'
                nx,ny= nx+dx[i], ny+dy[i]
        dfs(start+1,tmp,cctv)

cctv = []
block_cnt = 0
for x in range(N):
    for y in range(M):
        if 1<=board[x][y] <=5:
            cctv.append([board[x][y], x, y])
        elif board[x][y] == 6 :
            block_cnt+=1

dfs(0,board,cctv)
print(MIN)
```



