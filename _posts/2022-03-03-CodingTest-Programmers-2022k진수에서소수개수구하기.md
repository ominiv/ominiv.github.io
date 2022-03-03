---
title: Python/프로그래머스 2022 k진수에서 소수개수 구하기
date: 2022-03-03 00:00:01
categories:
- CodingTest
tags:
- 프로그래머스
- 오답노트
---

# [Python/프로그래머스] 2022 k진수에서 소수개수 구하기

📌[문제링크](https://programmers.co.kr/learn/courses/30/lessons/92335) 

n을 k진수로 변경 한 값을 가지고 0 을 기준으로 숫자를 뽑는다.<br>이때 뽑은 숫자가 소수일 경우 개수를 세면 된다.
`split(0)`를 활용하자.
---

## solution
```python
from collections import deque
def convert_k_num(n,k):
    ret=''
    while n > 0 :
        ret += str(n%k) # 나머지
        n=n//k # 몫
    return ''.join(reversed(ret))

def is_prime(k):
    if k==2 or k==3 : return True # 2 or 3 은 소수
    if k%2 ==0 or k<2 : return False # 2의 배수이거나 0,1은 소수가 아님
    for i in range(3,int(k**0.5)+1,2): # 3부터 sqrt(k)까지 2씩 증가하며 확인
        if k % i ==0 :
            return False
    return True

def solution(n, k):
    answer = -1
    k_num = convert_k_num(n,k)
    k_num_list = deque(list(k_num))
    k_num_list.append('0')
    result=[];tmp=''
    while k_num_list:
        x = k_num_list.popleft()
        if x !='0':
            tmp += x
        if x =='0':
            if tmp!='' and is_prime(int(tmp)):
                result.append(tmp)
            tmp = ''
    answer = len(result)
    return answer

```
