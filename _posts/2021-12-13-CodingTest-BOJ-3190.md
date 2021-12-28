---
title: Python/구현 BOJ-3190 뱀
date: 2021-12-13 23:30:09
categories:
- CodingTest
tags:
- 구현
---

# [Python/구현] BOJ-3190 뱀

📌[문제링크](https://www.acmicpc.net/problem/3190) [풀이참고](https://jjangsungwon.tistory.com/27)



사과의 위치와 뱀의 이동경로가 주어질때 이 게임이 몇초에 끝나는지 계산하라.



```python
from collections import deque

N = int(input())
K = int(input())
arr = [[0]*N for _ in range(N)]
for _ in range(K):
    a, b = map(int,input().split())
    arr[a-1][b-1] = 1 

L = int(input())
times = {}
for i in range(L):
    X, C = input().split()
    times[int(X)] = C

# 동 북 서 남
dx = [0,-1,0,1]
dy = [1,0,-1,0]

def change(direction, cnt):
    if cnt == 'L' : #왼쪽 (동 북 서 남)
        direction = (direction + 1) % 4 
    else : #오른쪽 (동 남 서 북)
        direction = (direction - 1) % 4 
    return direction

def start():
    direction = 0 # 초기방향 오른쪽
    time = 1
    x,y =0,0 # 초기 뱀 위치
    visited =deque([[x,y]])
    arr[x][y]=2 
    while True :
        x,y = x + dx[direction] , y + dy[direction]
        if 0<=x <N and 0<= y <N and arr[x][y]!=2:
            if arr[x][y] == 0 : # 사과가 없는경우
                tmp_x, tmp_y = visited.popleft()
                arr[tmp_x][tmp_y] = 0
            arr[x][y] = 2
            visited.append([x,y])
            if time in times.keys():
                direction = change(direction, times[time])
            time +=1
        else : #게임 종료
            return time

print(start())
```



