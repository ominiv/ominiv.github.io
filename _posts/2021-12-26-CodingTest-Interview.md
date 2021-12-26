---
title: HackerRank/Oracle interview
date: 2021-12-25 23:30:09
categories:
- CodingTest
tags:
- oracle
- JOIN
---

# [HackerRank/Oracle] interview

📌[문제링크](https://www.hackerrank.com/challenges/interviews/problem)  

  <BR>

join 문제다.  

view_stats에만 데이터가 있거나 submission_stats에만 데이터가 있는경우를 위해 outer join 실행

<BR>

```sql
select con.contest_id,
        con.hacker_id, 
        con.name, 
        sum(total_submissions), 
        sum(total_accepted_submissions), 
        sum(total_views), sum(total_unique_views)
from contests con 
inner join colleges col on con.contest_id = col.contest_id 
inner join challenges cha on  col.college_id = cha.college_id 
left outer join (select challenge_id, 
           sum(total_views) as total_views, 
           sum(total_unique_views) as total_unique_views
           from view_stats 
           group by challenge_id) vs on cha.challenge_id = vs.challenge_id 
left outer join (select challenge_id, 
           sum(total_submissions) as total_submissions, 
           sum(total_accepted_submissions) as total_accepted_submissions 
           from submission_stats 
           group by challenge_id) ss on cha.challenge_id = ss.challenge_id
group by con.contest_id, con.hacker_id, con.name
having sum(total_submissions) + sum(total_accepted_submissions) + sum(total_views) + sum(total_unique_views) >0
order by contest_id;
```

