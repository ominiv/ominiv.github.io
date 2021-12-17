---
title: Input vs. sys.stdin.readline 차이점
date: 2021-12-16 23:30:09
categories:
- Python
tags:
- 입출력
---

# Input vs. sys.stdin.readline 차이점



백준 문제를 풀며 틀렸습니다 보다 시간초과를 해결하기 더 어려웠었다....

그럴때 마다 종종 문제가 되었던 input() 과 sys. stdin 에 대해 알아보자!





## input ()

input() 은 파이썬의 내장 함수이다.

> ***If the prompt argument is present, it is written to standard output without a trailing newline. The function then reads a line from input, converts it to a string (stripping a trailing newline), and returns that**. When EOF is read, [`EOFError`](https://docs.python.org/3/library/exceptions.html#EOFError) is raised. Example:*
>
> 
>
> prompt argument가 존재한다면 개행 없이 쓰여짐.
>
> *input() 는  `사용자로부터 입력값을 읽고` -> `문자로 변환 (개행 제거)` ->  `반환 함`*



## sys.stdin



> *[File objects](https://docs.python.org/3.10/glossary.html#term-file-object) used by the interpreter for standard input, output and errors:*
>
> - *`stdin` is used for all interactive input (including calls to [`input()`](https://docs.python.org/3.10/library/functions.html#input));*
> - *`stdout` is used for the output of [`print()`](https://docs.python.org/3.10/library/functions.html#print) and [expression](https://docs.python.org/3.10/glossary.html#term-expression) statements and for the prompts of [`input()`](https://docs.python.org/3.10/library/functions.html#input);*
> - *The interpreter’s own prompts and its error messages go to `stderr`.*
>
> 
>
> stdin은 모든 대화식 입력에 사용된다는 의미는 우리가 흔히 키보드로 입력하는 행위 뿐만 아니라 파일 등의 넓은 범위의 입력을 의미한다. 그리고 주목해야 할 점은 stdin에 input() 호출을 포함하고 있단 사실이다.







## stdin.readline()과 input()함수간의 속도차이



1) Prompt 출력여부

2) 한번에 읽어와 버퍼에 저장하는 stdin.readline()가 
하나씩 누를 때마다 데이터를 버퍼에 보관하는 input() 보다 처리 속도가 빠르다. 
즉, 버퍼 사이즈 차이로 입력이 반복될 수록 **stdin.readline()**이 우위를 가진다.





## Reference

https://docs.python.org/3/library/functions.html#input

https://docs.python.org/3.10/library/sys.html#sys.stdin

https://green-leaves-tree.tistory.com/12

https://countingalaxy.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%9D%98-%EC%9E%85%EB%A0%A5%EA%B3%BC-%EC%B6%9C%EB%A0%A5

