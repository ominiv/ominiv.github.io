---
title: Python/heap BOJ-1655 가운데를 말해요
date: 2021-12-08 23:30:09
categories:
- CodingTest
tags:
- heap
---

# [Python/heap] BOJ-1655 가운데를 말해요 



쉬운 문제라고 생각했다.

sorted 함수로 정렬후 중간값을 뱉으면 된다고 생각했는데, 시간초과가 났다. 



이 문제의 경우,  두개의 힙을 활용해 중간값을 추출해야한다. 



## 시간초과 났던 경우

```python
N = int(input())
num_list = [int(input()) for _ in range(N)]

tmp_list=[]
for i in range(N):
    tmp_list.append(num_list[i])
    sorted_list = sorted(tmp_list)
    if i == 0:
        print(num_list[i])
    elif i / 2 == 0 : #홀수
        print(sorted_list[(i//2)+1])
    else : #짝수
        print(sorted_list[(i//2)])
```



## heap 이용한 경우

```python
import heapq
import sys
input = sys.stdin.readline

N = int(input())
max_h, min_h = [],[]

for i in range(N):
    num = int(input())
    if len(max_h) == len(min_h):
        heapq.heappush(max_h,-num)
    else :
        heapq.heappush(min_h, num)
    
    if len(max_h) >=1 and len(min_h)>=1 and max_h[0]*-1 > min_h[0] :
        max_value = heapq.heappop(max_h)*-1
        min_value = heapq.heappop(min_h)
        
        heapq.heappush(max_h, min_value*-1)
        heapq.heappush(min_h, max_value)
    print(max_h[0]*-1)

```



## 회고

나는 input() 함수와 sys.stdin.readline() 의 차이를 몰랐었다. ಥ_ಥ

input() 내장함수는 prompt message를 출력하고, 개행 문자를 삭제한 값을 리턴하기 때문에 느리다. 

시간을 줄이기 위해서는 sys.stdin.readline()를 꼭 이용하도록 하자.



## Reference

문제 : https://www.acmicpc.net/problem/1655

풀이참고 : https://velog.io/@uoayop/BOJ-1655-%EA%B0%80%EC%9A%B4%EB%8D%B0%EB%A5%BC-%EB%A7%90%ED%95%B4%EC%9A%94Python



