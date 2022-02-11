---
title: MongoDB
date: 2022-02-11 00:00:01
categories:
- DB
tags:
- MongoDB

---

# MongoDB 

Mongo DB 는 NoSQL 중 하나로 Document Oriented 데이터 베이스이다.

Document Oriented라는 말은 쉽게 말해서 JSON 형식이나 XML 형식으로 DB에 데이터를 저장하는 것을 말한다. Mongo DB 는 key : value 로 이루어진 JSON 의 형태로 데이터를 저장한다.

RDBMS 의 한 **row** 를 MongoDB 에서는 **Document** 라고 표현을 하고 **table** 을 **Collection** 이라고 한다. 그리고 Collection 들의 집합은 Database 이다. 개념은 동일하고 용어는 좀 다르니 가볍게 생각하자.

https://www.mongodb.com/try/download/community


---
## 장점

1. 속도가 빠르다.
2. 스키마가 없다.

## 단점

1. join 사용 불가
2. 메모리 사용량 큼

---
## 환경설정

1. 시스템 환경 변수 설정 > 환경변수 > Path 추가

   C:\Program Files\MongoDB\Server\4.4\bin

2. C 드라이브 에 C:/data/db/ 폴더 생성

3. cmd에서 MongoDB 실행  > mongd를 입력

4. 웹브라우져에서 127.0.0.1:27017 쳐보면 실행되는 것을 확인 할 수 있음

5. 종료하고 싶으면 mongod 를 실행한 cmd 창에서 

   ctrl + c 를 이용하여 종료하면 몽고디비 서비스가 종료된다

    



