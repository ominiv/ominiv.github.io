---
title: Python/Greedy BOJ-2217 ๋กํ
date: 2021-12-28 23:30:09
categories:
- CodingTest
tags:
- Greedy
---

# [Python/Greedy] BOJ-2217 ๋กํ

๐[๋ฌธ์ ๋งํฌ](https://www.acmicpc.net/problem/2217)

  <BR>

N๋ฒ์งธ๋ก ํฐ ์์ N์ ๊ณฑํ ๊ฐ์ ๊ณ์ฐํด์ ๊ฐ์ฅ ํฐ ๊ฐ์ ์ถ์ถ  ํ๋ฉด ๋๋ค.

์๋ฅผ๋ค์ด 15 rope์ 10 rope๊ฐ ์กด์ฌํ ๋ <br>15 rope๋ 15๋ฅผ ๋ฒํธ ์ ์๊ณ  10 rope์์๋ 10์ ๋ฒํฐ์ง ๋ชปํ๊ธฐ ๋๋ฌธ์ ์ต๋ ์ค๋์ 15์ด๋ค. <br>**10 rope๋ 10๋ฅผ ๋ฒํธ ์ ์๊ณ  15 rope์์๋ 10์ ๋ฒํธ ์ ์๊ธฐ ๋๋ฌธ์**  ์ต๋ ์ค๋์ 20์ด๋ค.

<br>

```python
N=int(input())
rope = []
for _ in range(N):
    rope.append(int(input()))
rope = sorted(rope, reverse=True)
result=0
for i in range(len(rope)) :
    tmp = rope[i]*(i+1)
    result = max(tmp,result)
print(result)
```

