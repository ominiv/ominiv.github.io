---
title: Mongo DB 쿼리 옵션 
date: 2022-02-11 00:00:01
categories:
- DB
tags:
- MongoDB
- OpenAPI
---

# Mongo DB 쿼리 옵션 : lt , lte , gt , gte
공공데이터를 이용하다가 처음보는 Parameter를 만났다. <br>알고보니 MonogoDB 쿼리옵션이였다.


|prameter| description|
|----|------------|
|cond[baseDate::EQ]| **동일** <br>즉 2022-02-11를 불러온다. <br>`{ <field>: { $eq: 2022-02-11 } }`|
|cond[baseDate::LT]| **미만** <br>즉 2022-02-11 제외 이전 데이터를 불러온다. <br>`{ <field>: { $lt: 2022-02-11 } }`|
|cond[baseDate::LTE]| **이하** <br>즉 2022-02-11 포함 이전 데이터를 불러온다. <br>`{ <field>: { $lte: 2022-02-11 } }`|
|cond[baseDate::GT]| **초과**<br>즉 2022-02-11 제외 이후 데이터를 불러온다. <br>`{ <field>: { $gt: 2022-02-11 } }`|
|cond[baseDate::GTE]| **이상** <br>즉 2022-02-11 포함 이후 데이터를 불러온다. <br>`{ <field>: { $gte: 2022-02-11 } }`|

---
## Refernce
- [MongoDB Document](https://docs.mongodb.com/manual/reference/operator/query/eq/)
