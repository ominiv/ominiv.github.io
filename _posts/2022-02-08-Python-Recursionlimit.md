---
title: Python RecursionLimit Setting
date: 2022-02-08 00:00:01
categories:
- Python
tags:
- 재귀
---

# [Python] 재귀 깊이 제한 늘리기
파이썬은 기본 재귀 깊이가 1000으로 매우 얕다. <br>그렇기에 재귀로 스크립트를 짤때는 꼭 `setrecursionlimit`을 지정해야한다.

런타임에러가 뜰 경우, 내가 재귀 깊이를 늘려줬는가를 체크하자.
 
```python
import sys
sys.setrecursionlimit(10**6)
```