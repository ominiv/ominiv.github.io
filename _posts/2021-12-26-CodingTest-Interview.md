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

๐[๋ฌธ์ ๋งํฌ](https://www.hackerrank.com/challenges/interviews/problem)  

  <BR>

join ๋ฌธ์ ๋ค.  

view_stats์๋ง ๋ฐ์ดํฐ๊ฐ ์๊ฑฐ๋ submission_stats์๋ง ๋ฐ์ดํฐ๊ฐ ์๋๊ฒฝ์ฐ๋ฅผ ์ํด outer join ์คํ

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

