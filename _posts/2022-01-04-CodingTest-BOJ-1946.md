---
title: Python/Greedy BOJ-1946 신입사원
date: 2022-01-04 00:00:01
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-1946 신입사원

📌[문제링크 ](https://www.acmicpc.net/problem/1946) 

문제가 잘 이해가 안되었다.

다른 모든 지원자와 비교했을 때 서류심사 성적과 면접시험 성적 중 적어도 하나가 다른 지원자보다 떨어지지 않는 자만 선발한다는 원칙만 이해하면된다. <BR>여기서 포인트는 A의 성적이 B의 면접점수와 서류점수보다 낮다면 A는 신입으로 뽑히지 않는다.

1차 서류면접 점수가 가장 높은 사람 a 의 면접점수를 초기값으로 두고<br>  나머지 사람들과 비교했을때 a의 면접점수보다 높은 사람을 체크한다.

<br>

## solution

```python
import sys
input = sys.stdin.readline

if __name__ == '__main__':
    T = int(input())
    for i in range(T) :
        result=1
        N = int(input())
        score = [list(map(int,input().split())) for _ in range(N)]
        score = sorted(score, key=lambda x : x[0]) # 1차 서류점수로 정렬
        minv = score[0][1]
        for j in range(1,N) :
            if score[j][1] < minv: # 서류 점수는 낮지만 면접점수는 높은 사람 체크
                minv = score[j][1]
                result+=1
        print(result)
```

