---
title: SQLite/solvesql 작품이 없는 작가 찾기
date: 2022-03-08 00:00:01
categories:
- CodingTest
tags:
- SQLite

---

# [SQLite/solvesql] 작품이 없는 작가 찾기

📌[문제링크](https://solvesql.com/problems/artists-without-artworks/) 


살아있지 않은 작가중 MoMa에 등록된 작품이없는 작가의 id와 이름을 출력하면된다.

---

## solution
```sql
select
  Death.artist_id,
  Death.name
from
  (
    select
      artist_id,
      name
    from
      artists
    where
      death_year is not null
  ) Death -- death_artist
  left outer join artworks_artists Work on Work.artist_id = Death.artist_id
where
  Work.artwork_id is null
```
