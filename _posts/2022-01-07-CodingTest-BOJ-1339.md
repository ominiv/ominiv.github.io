---
title: Python/Greedy BOJ-1339 단어 수학
date: 2022-01-07 00:00:01
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-1339 단어 수학

📌[문제링크 ](https://www.acmicpc.net/problem/1339) [풀이참고](https://suri78.tistory.com/183)

***풀이참고 링크들어가셔서 보시면됩니다**
후엥.. 골머리 아팠다. 

N개의 단어가 주어질때 그 수의 합이 최대인 경우를 구하는문제다. <Br>단어별 자리수를 만든다음 9-0숫자를 부여해서 최대값을 구하면된다. 

AB 와 BA가 주어졌을때 <br> A=10x1 , B=1 / B=10x1, A=1 으로 나타난다. <br> A=11 B=11 으로 최종 결과 값은 99+88 = 187이 된다. 

---

## solution
```python
import sys,copy
input = sys.stdin.readline

if __name__ == '__main__' :
    N = int(input())
    # ord() 문자를 아스키코드값으로 변경 a=65
    word = [list(map(lambda x: ord(x)-65, input().rstrip())) for _ in range(N)]
    alpha = [0]*26
    
    for i in range(N) :
        j = 0
        for w in word[i][::-1]:
            alpha[w]+=(10**j)
            j+=1
    alpha.sort(reverse=True)
    ans,t=0,9
    for i in range(26):
        if alpha[i] == 0 :
            break
        ans+=(t*alpha[i])
        t-=1
    print(ans)
```
