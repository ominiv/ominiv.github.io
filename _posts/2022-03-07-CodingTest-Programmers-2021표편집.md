---
title: Python/프로그래머스 2021 표 편집
date: 2022-03-07 00:00:01
categories:
- CodingTest
tags:
- 프로그래머스
- 오답노트
- linked_list
---

# [Python/프로그래머스] 2021 표 편집

📌[문제링크](https://programmers.co.kr/learn/courses/30/lessons/81303) [링크드리스트_참고](https://ckd2806.tistory.com/entry/%ED%8C%8C%EC%9D%B4%EC%8D%AC-python-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%ED%91%9C-%ED%8E%B8%EC%A7%91
)

처음엔 list로 접근했다가 insert, pop로 인해 시간초과가 났다.<Br>결국 못풀고 구글링을 해보니 linked list를 이용하면 되더라.<Br>여기서 포인트는 1의 Prev는 마지막 숫자이다. 그리고 마지막숫자의 Next는 1임을 명심하자.

*example)* <br>`Prev - 1 - Next` -> `Prev - 2 - Next` -> `Prev - 3 - Next` -> `Prev - 4 - Next` -> `Prev - 5 - Next`<br>
`5 - 1 - 2` -> `1 - 2 - 3` -> `2 - 3 - 4` -> `3 - 4 - 5` -> `4 - 5 - 1`

---

## solution
```python
def solution(n, k, cmd):
    answer = ''
    # 앞뒤가 연결되어있는 1-n까지의 연결리스트
    linked_list ={1:[n,2]}
    for i in range(2,n+1):
        if i == n:
            linked_list[i] = [i-1,1]
        else :
            linked_list[i] = [i-1,i+1] 
    # 정답을 판별하기 위한 OX배열
    OX =['O' for i in range(1,n+1)]
    # 삭제한것을 되돌리기 위한 stack
    stack=[]
    k+=1

    for c in cmd :
        if c[0]=='D':
            for _ in range(int(c[2:])):
                k = linked_list[k][1]
        elif c[0]=='U':
            for _ in range(int(c[2:])):
                k = linked_list[k][0]
        elif c[0]=='C':
            prev, next = linked_list[k]
            linked_list[prev][1]=next
            linked_list[next][0]=prev
            stack.append([prev,next,k])
            OX[k-1]='X'
            if next == 1 :
                k = linked_list[k][0]
            else :
                k = linked_list[k][1]
        elif c[0]=='Z':
            prev, next, now = stack.pop()
            linked_list[prev][1]=now
            linked_list[next][0]=now
            OX[now-1] = 'O'
    return ''.join(OX)

```
