---
title: Python/프로그래머스 2022 주차요금계산
date: 2022-02-26 00:00:01
categories:
- CodingTest
tags:
- 프로그래머스
---

# [Python/프로그래머스] 2022 주차요금계산

📌[문제링크](https://programmers.co.kr/learn/courses/30/lessons/92334) 

차량 번호가 작은 자동차부터 청구할 주차 요금을 차례대로 뱉으면 된다.

---

## solution
```python
from collections import deque
import math
import copy

def solution(fees, records):
    answer = []
    queue= []
    for r in records :
        a,b,c =r.split()
        queue.append([a,b,c])
    # 차번호, 시간 순으로 정렬
    queue = deque(sorted(queue, key = lambda x : (x[1],x[0])))
    dictReport = {}
    while queue :
        time, car, status = queue.popleft()
        if len(queue)== 0 : 
            next_time, next_car, next_status = '23:59', copy.copy(car), 'last'
        else : 
            next_time, next_car, next_status  = queue.popleft()
        if car not in dictReport.keys(): 
            total=0
            dictReport[car] = total
        # 시간 계산
        if car == next_car and status != next_status:
            total += (int(next_time.split(':')[0]) - int(time.split(':')[0]))*60 +  (int(next_time.split(':')[1]) - int(time.split(':')[1]))
        else :
            total += (23 - int(time.split(':')[0]))*60 +  (59 - int(time.split(':')[1]))
            queue.appendleft([next_time, next_car, next_status])
        # 비용 계산
        cost = int(fees[1] + (math.ceil((total-fees[0])/fees[2]))*fees[3])
        # 기본요금 보다 작게 나올 경우에도 기본요금 부과
        if cost < fees[1] : 
            cost = fees[1]
        dictReport[car] = cost
    answer = list(dictReport.values())
    return answer

```
