---
title: Python/재귀-BFS BOJ-1697 숨바꼭질
date: 2022-02-04 00:00:01
categories:
- CodingTest
tags:
- 재귀
- BFS
---

# [Python/재귀-BFS] BOJ-1697 숨바꼭질

📌[문제링크](https://www.acmicpc.net/problem/1697) [nearhome님의 풀이링크](https://nearhome.tistory.com/45)<br>***풀이링크 들어가셔서 보시면 됩니다.**

동생을 찾는 가장 빠른 시간을 출력하는 문제다.<br>1차원 배열으로 방문여부를 체크하면 쉽게 풀 수 있다.

---

## BFS solution
```python
import sys
input = sys.stdin.readline

if __name__ == '__main__':
    N,K = map(int,input().split())
    visited= [0]*100001 
    queue = [N]
    if N==K :
        visited[K]=0
    else :
        while queue and not visited[K] :
            q = queue.pop(0)
            for i in range(3) :
                if i == 0 :
                    nx = q+1
                elif i==1 : 
                    nx = q-1
                else :
                    nx = q*2
                if 0<=nx<100001 and not visited[nx] : #다음칸 크기확인 & 방문여부 체크
                    visited[nx] = visited[q]+1
                    queue.append(nx)
    
    print(visited[K])
```

---

## 재귀 solution

```python
import sys
input = sys.stdin.readline

def recursive(N,K) :
    if N >=K :
        return N-K
    elif K==1 :
        return 1
    elif K%2 :
        return 1+(min(recursive(N,K-1), recursive(N,K+1)))
    else :
        return min(K-N, 1+recursive(N,K//2))

if __name__ == '__main__':
    N,K = map(int,input().split())
    print(recursive(N,K))
```