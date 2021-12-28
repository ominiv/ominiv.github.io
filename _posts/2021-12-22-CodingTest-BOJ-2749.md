---
title: Python/피사노주기 BOJ-2749 피보나치 3
date: 2021-12-21 23:30:09
categories:
- CodingTest
tags:
- 피사노주기
---

# [Python/피사노주기] BOJ-2749 피보나치 3

📌[문제링크](https://www.acmicpc.net/problem/2749) [풀이참고](https://kyun2da.github.io/2020/08/30/fibonacci/)

  <BR>

***풀이참고 링크 들어가셔서 보시면 됩니다.** 

<BR>

피사노 주기를 이용하자.

`피사노 주기 : 피보나치수를 K로 나눈 나머지는 항상 주기를 가짐`

이때 K=10^n이면, 피사노주기는 15*10^(n-1)이 된다.

<BR>

  ```python
  N = int(input())
  
  mod = 1000000
  fibo = [0, 1]
  p = mod//10*15
  
  for i in range(2,p):
      fibo.append(fibo[i-1]+fibo[i-2])
      fibo[i] %= mod
  
  print(fibo[N%p])
  ```



## 회고

피보나치하면 재귀만 생각했던 나 반성하자 ^_^ㅠ 

번외로 피보나치 문제를 풀때 memoization 방법 사용하기도 한다. 단 본 문제에서는 N이 매우 크기때문에 적합하지 않다.

