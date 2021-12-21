---
title: HackerRank/Oracle New Companies
date: 2021-12-19 23:30:09
categories:
- CodingTest
tags:
- oracle
- JOIN
---

# [HackerRank/Oracle] New Companies

📌[문제링크](https://www.hackerrank.com/challenges/the-company/problem) [풀이참고](https://techblog-history-younghunjo1.tistory.com/163) 

  

*풀이 참고 링크에 들어가셔서 보시면 됩니다.   

join을 활용하는 문제다.

  

## 1. INNER JOIN 이용

```sql
SELECT  company.company_code , company.founder, lead.lead_count, senior.senior_count, manager.manager_count, employee.employee_count
FROM    company

INNER JOIN  (
    SELECT  company_code, 
            count(distinct(lead_manager_code))as lead_count 
    from lead_manager 
    group by company_code
) lead on company.company_code = lead.company_code

INNER JOIN (
    SELECT  company_code,
            count(distinct(senior_manager_code)) as senior_count
    from Senior_Manager
    group by company_code  
) senior on company.company_code = senior.company_code

INNER JOIN(
    SELECT  company_code,
            count(distinct(manager_code)) as manager_count
    from manager
    group by company_code
)manager on company.company_code = manager.company_code

INNER JOIN(
    SELECT company_code,
            count(distinct(employee_code)) as employee_count
    from employee
    group by company_code
) employee on company.company_code = employee.company_code
ORDER BY company.COMPANY_CODE;
```

  

## 2. 다른 풀이

```SQL
SELECT  C.COMPANY_CODE, C.FOUNDER,
        COUNT(DISTINCT(L.LEAD_MANAGER_CODE)),           
        COUNT(DISTINCT(S.SENIOR_MANAGER_CODE)),
        COUNT(DISTINCT(M.MANAGER_CODE)),
        COUNT(DISTINCT(E.EMPLOYEE_CODE))
FROM COMPANY C, LEAD_MANAGER L, SENIOR_MANAGER S, MANAGER M, EMPLOYEE E
WHERE C.COMPANY_CODE = L.COMPANY_CODE AND 
    C.COMPANY_CODE = S.COMPANY_CODE AND 
    C.COMPANY_CODE = M.COMPANY_CODE AND 
    C.COMPANY_CODE = E.COMPANY_CODE
GROUP BY C.COMPANY_CODE, C.FOUNDER
ORDER BY C.COMPANY_CODE;
```

  

## 3. 결과

```txt
C1 Angela 1 2 5 13 
C10 Earl 1 1 2 3 
C100 Aaron 1 2 4 10 
C11 Robert 1 1 1 1 
C12 Amy 1 2 6 14 
C13 Pamela 1 2 5 14 
C14 Maria 1 1 3 5 
C15 Joe 1 1 2 3 
C16 Linda 1 1 3 5 
C17 Melissa 1 2 3 7 
C18 Carol 1 2 5 6 
C19 Paula 1 2 4 7 
C2 Frank 1 1 1 3 
C20 Marilyn 1 1 2 2 
C21 Jennifer 1 1 3 7 
C22 Harry 1 1 3 6 
C23 David 1 1 1 2 
C24 Julia 1 1 2 6 
C25 Kevin 1 1 2 5 
C26 Paul 1 1 1 3 
{-truncated-}
```

