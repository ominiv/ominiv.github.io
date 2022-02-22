---
title: Python/DFS BOJ-9019 DSLR
date: 2022-02-22 00:00:01
categories:
- CodingTest
tags:
- BFS
- 오답노트
---

# [Python/DFS] BOJ-9019 DSLR

📌[문제링크](https://www.acmicpc.net/problem/9019) 

A를 B러 바꾸는 최소한의 명령어를 생성하는 문제다. <br>시간초과로 골치아팠던 문제다. 

A,B는 0 - 10000미만이므로 1차원 배열을 생성해서 방문체크를 하고 명령어를 누적하면된다. 

---

## BFS solution
```python
from collections import deque
import sys 
input = sys.stdin.readline

if __name__ == '__main__':
    T =  int(input())
    for _ in range(T):
        A,B = map(int,input().split())
        queue = deque([(A,'')])
        visited = [False for _ in range(10000)]
        visited[A]= True
        while queue:
            s,result = queue.popleft()
            if s == B :
                break
            ns = (2*s)%10000
            if  not visited[ns] : # D
                queue.append((ns,result+ 'D'))
                visited[ns]= True
            ns = (s-1)%10000
            if  not visited[ns] : # s
                queue.append((ns,result+ 'S'))
                visited[ns]=True
            ns = (s%1000)*10 + s//1000
            if not visited[ns] : #L 왼쪽으로 회전
                queue.append((ns,result+ 'L'))
                visited[ns]=True
            ns = (s%10)*1000 + s//10
            if not visited[ns] : # R 오른쪽으로 회전
                queue.append((ns,result+ 'R'))
                visited[ns]=True
        print(result)
```

## 회고

처음엔 왼쪽/오른쪽 회전의 경우, 숫자를 문자로 바꾸고 pop -> join을 하는 방법을 선택했었다. 그랬더니 바로 시간초과 ^_^ ; 
