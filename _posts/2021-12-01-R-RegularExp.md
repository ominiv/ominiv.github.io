---
title: R regular expression
date: 2021-12-01 23:30:09
categories:
- R
tags:
- R
---

# 정규표현식

    1. \* 적어도 0번 이상
    2. \+ 적어도 1번 이상
    3. ? 0 or 1.
    4. . 무엇이든 한 글자를 의미
    5. ^ 시작 문자 지정 
    6. ex) ^[abc] abc중 한 단어 포함한 것으로 시작
    7. [^] 해당 문자를 제외한 모든 것 ex) [^abc] a,b,c 는 빼고
    8. $ 끝 문자 지정
    9. [a-z] 알파벳 소문자 중 1개
    10. [A-Z] 알파벳 대문자 중 1개
    11. [0-9] 모든 숫자 중 1개
    12. [a-zA-Z] 모든 알파벳 중 1개
    13. [가-힣] 모든 한글 중 1개
    14. [^가-힣] 모든 한글을 제외한 모든 것
    15. [[:punct:]] 구두점 문자, ! " # $ % & ’ ( ) * + , - . / : ; < = > ? @ [ ] ^ _ ` { |  } ~.
    16. [[:alpha:]] 알파벳 대소문자, 동등한 표현 [A-z]
    17. [[:lower:]] 영문 소문자, 동등한 표현 [a-z]
    18. [[:upper:]] 영문 대문자, 동등한 표현 [A-Z].
    19. [[:digit:]] 숫자, 0,1,2,3,4,5,6,7,8,9,
    20. [[:xdigit:]] 16진수 [0-9A-Fa-f]
    21. [[:alnum:]] 알파벳 숫자 문자, 동등한 표현[A-z0-9].
    22. [[:cntrl:]] \n, \r 같은 제어문자, 동등한 표현[\x00-\x1F\x7F].
    23. [[:graph:]] 그래픽 (사람이 읽을 수 있는) 문자, 동등한 표현
    24. [[:print:]] 출력가능한 문자, 동등한 표현
    25. [[:space:]] 공백 문자: 탭, 개행문자, 수직탭, 공백, 복귀문자, 서식이송
    26. [[:blank:]] 간격 문자, 즉 스페이스와 탭.
