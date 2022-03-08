---
title: SQLite/solvesql 지역별 주문의 특징
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- SQLite
- 오답노트

---

# [SQLite/solvesql] 지역별 주문의 특징

📌[문제링크](https://solvesql.com/problems/characteristics-of-orders/) 

SQLite의 경우, pivot 함수가 없다. <Br> Case When Then End 구절으로 데이터를 조작해야한다. 

컬럼명 오타없이 입력하자.

---

## solution
```sql
select
  region as Region,
  max(Furniture) as 'Furniture',
  max(Office) as 'Office Supplies',
  max(Technology) as 'Technology'
from
  (
    select
      Result.region,
      case
        when category = 'Furniture' then sum(cnt)
        else 0
      end as Furniture,
      case
        when category = 'Office Supplies' then sum(cnt)
        else 0
      end as Office,
      case
        when category = 'Technology' then sum(cnt)
        else 0
      end as Technology
    from
      (
        select
          region,
          category,
          count(distinct order_id) as cnt
        from
          records
        group by
          region,
          category
      ) Result
    group by
      Result.region,
      category
  )
group by
  region
```

