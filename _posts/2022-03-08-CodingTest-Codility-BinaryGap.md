---
title: Python/Codility BinaryGap
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- Codility
- ์ค๋ต๋ธํธ

---

# [Python/Codility] BinaryGap

๐[๋ฌธ์ ๋งํฌ](https://app.codility.com/programmers/trainings/9/binary_gap/) 

์ฝ๋๋ฆฌํฐ๋ testCase๋ฅผ ๋ค ๋ง์ท๋๋ผ๋ ๋ฐฉ์ฌํ๋ฉด ์๋๋ค. <br>์ฝ๊ฒ ์ฝ๋๋ฅผ ์ ์ถํ์ผ๋ ๊ฒฐ๊ณผ๋ ์๋ง์ง์ฐฝ์ด์๋ค. ๊ผผ๊ผผํ๊ฒ ๋ฌธ์ ๋ฅผ ์ฝ์

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

## ๋ค๋ฅธ์ฌ๋ ํ์ด
์์ฒญ๋๊ฒ ๊ฐ๋จํ ๋ฐฉ๋ฒ์ด๋ค.<br>
๊ฐ์ฅ ๋จผ์  ์๋ 0 ์ ๊ฑฐ -> ์๋ 1 ์ ๊ฑฐ ->  1๋ก split ํ ํ max ๊ธธ์ด ์ฒดํฌ 

```python
def solution(N):
    return len(max(bin(N)[2:].strip('0').strip('1').split('1')))
```
