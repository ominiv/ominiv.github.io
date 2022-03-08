---
title: SQLite/solvesql 가구 판매의 비중이 높았던 날 찾기
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- SQLite

---

# [SQLite/solvesql] 가구 판매의 비중이 높았던 날 찾기

📌[문제링크](https://solvesql.com/problems/blog-counter/) 

sqlite의 경우, 숫자를 나눴을때 정수로 나오는 문제가 있었다. <Br>이럴 땐 +0.00을 더해보자. 

order_date 기준 전체 주문 건수와 Furniture 주문건수를 구한후, where문으로 order_date기준 주문이 10건이상이고, 구매중 40%이상이 가구일때를 뱉으면된다.

---

## solution
```sql
select
  total.order_date,
  Furniture_cnt as funiture,
  round(
    (Furniture_cnt + 0.00) / (total.total_cnt + 0.00) * 100,2) as furniture_pct
from --order_date 기준 전체 주문건수/ Furniture 주문건수
  (
    select
      order_date,
      count(distinct order_id) as total_cnt
    from
      records
    group by
      order_date
  ) total
  left outer join (
    select
      order_date,
      count(distinct order_id) as Furniture_cnt
    from
      records
    where
      category = 'Furniture'
    group by
      order_date
  ) F_count on total.order_date = F_count.order_date 
where furniture_pct >= 40 and total_cnt >= 10
order by
  furniture_pct desc,total.order_date
```
