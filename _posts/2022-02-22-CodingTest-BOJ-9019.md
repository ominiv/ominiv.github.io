---
title: Python/DFS BOJ-9019 DSLR
date: 2022-02-22 00:00:01
categories:
- CodingTest
tags:
- BFS
- ์ค๋ต๋ธํธ
---

# [Python/DFS] BOJ-9019 DSLR

๐[๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/9019) 

A๋ฅผ B๋ฌ ๋ฐ๊พธ๋ ์ต์ํ์ ๋ช๋ น์ด๋ฅผ ์์ฑํ๋ ๋ฌธ์ ๋ค. <br>์๊ฐ์ด๊ณผ๋ก ๊ณจ์น์ํ ๋ ๋ฌธ์ ๋ค. 

A,B๋ 0 - 10000๋ฏธ๋ง์ด๋ฏ๋ก 1์ฐจ์ ๋ฐฐ์ด์ ์์ฑํด์ ๋ฐฉ๋ฌธ์ฒดํฌ๋ฅผ ํ๊ณ  ๋ช๋ น์ด๋ฅผ ๋์ ํ๋ฉด๋๋ค. 

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
            if not visited[ns] : #L ์ผ์ชฝ์ผ๋ก ํ์ 
                queue.append((ns,result+ 'L'))
                visited[ns]=True
            ns = (s%10)*1000 + s//10
            if not visited[ns] : # R ์ค๋ฅธ์ชฝ์ผ๋ก ํ์ 
                queue.append((ns,result+ 'R'))
                visited[ns]=True
        print(result)
```

## ํ๊ณ 

์ฒ์์ ์ผ์ชฝ/์ค๋ฅธ์ชฝ ํ์ ์ ๊ฒฝ์ฐ, ์ซ์๋ฅผ ๋ฌธ์๋ก ๋ฐ๊พธ๊ณ  pop -> join์ ํ๋ ๋ฐฉ๋ฒ์ ์ ํํ์๋ค. ๊ทธ๋ฌ๋๋ ๋ฐ๋ก ์๊ฐ์ด๊ณผ ^_^ ; 
