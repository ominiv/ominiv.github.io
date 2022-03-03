---
title: Python/BFS BOJ-1963 소수 경로
date: 2022-03-03 00:00:01
categories:
- CodingTest
tags:
- BFS
- 오답노트
---

# [Python/BFS] BOJ-1963 소수 경로

📌[문제링크](https://www.acmicpc.net/problem/1963) 

두 소수 사이의 변환에 필요한 최소 회수를 출력하면 된다.<br> 4자리 수가 고정되어있기 때문에 각 자리수에 들어가 조건에 맞는 수를 큐에 넣음.

**소수 체크하는 함수는 꼭 외워둘것 (에라토스테네스의 체)**


---

## BFS solution
```python
import sys
from collections import deque
input = sys.stdin.readline


def is_prime(B):
    if B == 2 or B==3 :
        return True
    elif B % 2 == 0 or B < 2 : 
        return False
    else :
        for i in range(3,int(B**0.5)+1,2):
            if B % i == 0 :
                return False
        return True

def bfs():
    queue = deque([A])
    visited[A]=1
    while queue :
        x_num = queue.popleft()
        for i in range(4):
            x = list(str(x_num))
            if i == 0 : # 첫째자리수 1-9
                for j in range(1,10):
                    x[i]=str(j); nx = int(''.join(x))
                    if is_prime(nx) and visited[nx]==0:
                        queue.append(nx)
                        visited[nx] = visited[x_num]+1
            elif i > 0 : # 2-4째자리수 0-9
                for j in range(0,10):
                    x[i]=str(j); nx = int(''.join(x))
                    if is_prime(nx) and visited[nx]==0:
                        queue.append(nx)
                        visited[nx] = visited[x_num]+1
        if x_num == B :
            return visited[B]-1
    return 'Impossible'

if __name__ =='__main__':
    T = int(input())
    for _ in range(T):
        A,B =map(int,input().split())
        visited = [0]*10000
        if A==B :
            print(0)
        elif 1000<= int(A) <= 9999 and 1000<= int(B) <= 9999 :
            print(bfs())
        else :
            print('Impossible')

```
---
## 회고
bfs를 시작하기 전에 꼭 `visited[시작점]=1`을 방문한 것으로 두자.<br>
에라토스테네스의 체 : 소수인지 판별하고자 하는 숫자의 제곱근 내에 있는 수들의 배수를 걸러낸다. 시간 복잡도는 O(n log log n)이다.