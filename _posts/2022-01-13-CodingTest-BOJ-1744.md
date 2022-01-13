---
title: Python/Greedy BOJ-1744 수묶기
date: 2022-01-13 00:00:01
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-1744 수묶기

📌[문제링크 ](https://www.acmicpc.net/problem/1744) [kyoung-jnn 님의 플이](https://kyoung-jnn.tistory.com/entry/%EB%B0%B1%EC%A4%801744%EB%B2%88%ED%8C%8C%EC%9D%B4%EC%8D%ACPython-%EC%88%98-%EB%AC%B6%EA%B8%B0)

***풀이링크 들어가셔서 보시면 됩니다.**

수열을 묶어 최대 합을 구하면된다. 전형적인 그리디 알고리즘을 활용하면 되는 문제다. <br>양수는 내림차순, 음수는 오름차순으로 정렬해서 차례로 곱하거나 더해주면된다.  <br>무조건 1의 경우 더하기를 해야하는 점이 포인트다.

---

## solution
```python
import sys
input = sys.stdin.readline
if __name__ == '__main__' :
    N = int(input())
    pos = []; neg=[]
    for _ in range(N) :
        tmp = int(input())
        if tmp > 0 : pos.append(tmp)
        else: neg.append(tmp)
    neg = sorted(neg)
    pos = sorted(pos, reverse=True)
    result=0    
    if len(neg) % 2 == 0 :
        for i in range(0,len(neg),2):
            result += neg[i] * neg[i+1]
    else :
        for i in range(0,len(neg)-1,2):
            result += neg[i] * neg[i+1]
        result += neg[len(neg)-1] # 마지막 숫자 더해주기 
    
    if len(pos) % 2 == 0 :
        for i in range(0,len(pos),2):
            if pos[i]==1 or pos[i+1]==1 : # 1인 경우 더하기
                result += (pos[i]+pos[i+1])
            else :
                result += pos[i] * pos[i+1]
    else :
        for i in range(0,len(pos)-1,2):
            if pos[i]==1 or pos[i+1]==1 : # 1인 경우 더하기
                result += (pos[i]+pos[i+1])
            else :
                result += pos[i] * pos[i+1]
        result += pos[len(pos)-1] # 마지막 숫자 더해주기 
    print(result)
```
