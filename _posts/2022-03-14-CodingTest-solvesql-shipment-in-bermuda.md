---
title: SQLite/solvesql 버뮤다 삼각지대에 들어가버린 택배
date: 2022-03-14 00:00:01
categories:
- CodingTest
tags:
- SQLite
- 오답노트

---

# [SQLite/solvesql] 버뮤다 삼각지대에 들어가버린 택배

📌[문제링크](https://solvesql.com/problems/shipment-in-bermuda/) 

SQLite에서는 date format을 맞출때 `strftime('%Y',column)` 을 사용하면 된다.

---

## solution
```sql
select dt as delivered_carrier_date,count(*) as orders
from (select  strftime('%Y-%m-%d', order_delivered_carrier_date) as dt ,
              order_id, 
              order_delivered_customer_date, 
              order_delivered_carrier_date
      from olist_orders_dataset
      where order_delivered_customer_date is null and order_delivered_carrier_date is not null)
where strftime('%Y-%m',dt) = '2017-01'
group by dt
order by dt 
```
