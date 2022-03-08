---
title: SQLite/solvesql 할부는 몇 개월로 해드릴까요
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- SQLite

---

# [SQLite/solvesql] 할부는 몇 개월로 해드릴까요

📌[문제링크](https://solvesql.com/problems/installment-month/) 

고전적인 groupby 문제다.<Br> 할부개월별 주문 count를 체크할때 order_id의 중복여부를 체크하자

---

## solution
```sql
select
  payment_installments,
  count(distinct order_id) as order_count,
  min(payment_value) as min_value,
  max(payment_value) as max_value,
  avg(payment_value) as avg_value
from
  olist_order_payments_dataset
where
  payment_type = 'credit_card'
group by
  payment_installments

```
