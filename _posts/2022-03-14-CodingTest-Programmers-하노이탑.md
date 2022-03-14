---
title: Python/프로그래머스 하노이탑
date: 2022-03-14 00:00:01
categories:
- CodingTest
tags:
- 프로그래머스
- 오답노트
---

# [Python/프로그래머스] 하노이탑

📌[문제링크](https://programmers.co.kr/learn/courses/30/lessons/81303) 

1번 기둥에 있는 원판들을 3번 원판으로 최소로 옮기는 방법을 return 하면 된다.

하노이탑은 전형적인 dfs 문제다. <Br>
A, B, C 탑이 있고 A:시작, B:경유, C:목적지 라고 생각해보자. <br>
1. A에서 마지막 원판만 남기고 B로 옮김<br>
2. 마지막 원판은 가장 큰 사이즈므로 C로 바로 옮김<br>
3. B에서 마지막 원판만 남기고 A로 옮김

---

## solution
```python
def move(frm, to ,mid, n, answer) :
    if n ==1 :
        answer.append([frm,to])
        return
    move(frm,mid,to,n-1,answer) # a에서 b로 이동
    answer.append([frm,to]) # a 에서 c로 이동 
    move(mid,to,frm,n-1,answer) # b에서 a로 이동

def solution(n):
    answer = []
    move(1,3,2,n,answer)
    return answer

```
