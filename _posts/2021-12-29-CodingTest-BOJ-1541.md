---
title: Python/Greedy BOJ-1541 잃어버린 괄호
date: 2021-12-28 23:30:09
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-1541 잃어버린 괄호

📌[문제링크](https://www.acmicpc.net/problem/1541)

  <BR>

'-'를 기준으로 문자열을 나눈다. <br>

'-' 이전의 값은 더하고 이후의 값은 빼주면된다.

<br>

```python
arr = input().split('-')

result=0
for i in arr[0].split('+'):
    result+=int(i)
for i in arr[1:]:
    for j in i.split('+'):
        result-=int(j)    
print(result)
```

