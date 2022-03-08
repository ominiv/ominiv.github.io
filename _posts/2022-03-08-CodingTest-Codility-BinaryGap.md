---
title: Python/Codility BinaryGap
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- Codility
- 오답노트

---

# [Python/Codility] BinaryGap

📌[문제링크](https://app.codility.com/programmers/trainings/9/binary_gap/) 

코딜리티는 testCase를 다 맞췄더라도 방심하면 안된다. <br>쉽게 코드를 제출했으나 결과는 엉망진창이였다. 꼼꼼하게 문제를 읽자

---

## solution
```python
def solution(N):
    N = bin(N)[2:]
    arr = []
    for idx, value in enumerate(N):
        if value=='1':
            arr.append(idx)
    arr2= []
    if len(arr) > 1:
        for i in range(len(arr)-1):
            arr2.append(arr[i+1]-arr[i]-1)
        return max(arr2)
    else : 
        return 0
```

## 다른사람 풀이
엄청나게 간단한 방법이다.<br>
가장 먼저 양끝 0 제거 -> 양끝 1 제거 ->  1로 split 한 후 max 길이 체크 

```python
def solution(N):
    return len(max(bin(N)[2:].strip('0').strip('1').split('1')))
```
