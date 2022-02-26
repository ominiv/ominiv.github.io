---
title: Python/프로그래머스 2022 신고 결과 받기
date: 2022-02-26 00:00:01
categories:
- CodingTest
tags:
- 오답노트
---

# [Python/프로그래머스] 2022 신고 결과 받기

📌[문제링크](https://programmers.co.kr/learn/courses/30/lessons/92334) 

k번이상 신고된 유저는 게시판이용이 정지되고, 해당유저를 신고한 모든 유저에게 정지사실을 메일로 발송하면된다. <br> 이때 각 유저가 받는 메일 수를 결과롤 뱉으면 된다. <br>본능적으로 dictionary를 써야한다고 생각이 들었다. 

한 사람이 특정 사람을 여러번 신고할 경우 1회 신고한 것으로 간주하므로 `set(report)`를 활용하면 편하다.

---

## solution
```python
def solution(id_list, report, k):
    answer = [0]*len(id_list)
    dicReport ={id:0 for id in id_list}
    # 신고 당한 횟수 체크
    for r in set(report):
        blocked = r.split()[1]
        dicReport[blocked]+=1
    # 유저별 받는 메일의 수 체크
    for r in set(report):
        inform, blocked = r.split()
        if dicReport[blocked] >= k : # k번 이상 신고 당한 경우
            answer[id_list.index(inform)]+=1
    return answer
```
