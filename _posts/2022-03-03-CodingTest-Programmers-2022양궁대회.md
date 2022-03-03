---
title: Python/프로그래머스 2022 양궁대회
date: 2022-03-03 00:00:01
categories:
- CodingTest
tags:
- 오답노트
- 구현
- DFS
- 프로그래머스
---

# [Python/프로그래머스] 2022 양궁대회

📌[문제링크](https://programmers.co.kr/learn/courses/30/lessons/92342) [풀이참고](https://velog.io/@jadenkim5179/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%EC%96%91%EA%B6%81%EB%8C%80%ED%9A%8C)

*풀이참고 링크에 들어가서 보시면 됩니다.

라이언은 어피치를 가장 큰 점수 차이로 이기기 위해서 n발의 화살을 어떤 과녁 점수에 맞혀야 하는지를 구하면된다.<br> 라이언이 쏘는 모든 경우의 수를 이용해 어피치를 이길 수 있는지를 체크한다. `from itertools import combinations_with_replace` 이용

---

## 구현 solution
```python

from itertools import combinations_with_replacement
from collections import Counter

def solution(n,info):
    max_score = 0; max_comb={}
    answer=[]
    for comb in combinations_with_replacement(range(11),n):
        a_score, r_score = 0,0
        cnt = Counter(comb)
        for i in range(1,11):
            if info[10-i] < cnt[i]:
                r_score+=i
            elif info[10-i] == cnt[i] and info[10-i] >0 and cnt[i]>0 : # 비긴 경우, 어피치가 점수 가짐
                a_score+=i
            elif info[10-i] > cnt[i] :
                a_score+=i
        diff = r_score - a_score
        if diff > max_score:
            max_comb = cnt
            max_score = diff
    if max_score > 0:
        answer=[0]*11
        for n in max_comb:
            answer[10-n] = max_comb[n]
        return answer
    else :
        answer = [-1]
        return answer
```
---
## DFS 풀이
전체순회를 하는 위 풀이보다 DFS로 일부의 경우만 탐색하는 것이 더 효율적이다. (과녁의 수가 10개 밖에 안되어서 시간초과없이 풀이가 가능하다.)<br> 각 점수의 과녁에 대해 라이언은 어피치보다 하나 더 맞추거나 아예 안맞추거나 둘 중 하나를 선택 해야한다.

```python
from copy import deepcopy
max_diff , max_board = 0,[]
def solution(n,info):
    def dfs(a_score, r_score, cnt, idx, board):
        global max_diff,max_board
        if cnt > n:
            return
        if idx > 10 :
            diff = r_score - a_score
            if diff > max_diff:
                board[10] = n-cnt
                max_board=board
                max_diff = diff
            return
        if cnt < n :  
            board2=deepcopy(board)
            board2[10-idx] = info[10-idx]+1
            dfs(a_score,r_score+idx,cnt+info[10-idx]+1,idx+1,board2)
        board3 = deepcopy(board)
        if info[10-idx] >0:
            dfs(a_score+idx, r_score, cnt, idx+1,board3)
        else :
            dfs(a_score, r_score, cnt, idx+1,board3)
    dfs(0,0,0,0,[0]*11)
    return max_board if max_board else [-1]
```