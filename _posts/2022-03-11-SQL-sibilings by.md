---
title: Oracle Sbilings by
date: 2022-03-11 23:30:09
categories:
- SQL
tags:
- 계층정렬
---

# [Oracle] Sbilings by

계층적으로 정렬을 해야할 때가 있다. <br> 그럴 땐 아래 구문이 유용하게 사용된다.

`sbilings by`는 계층구조는 유지하면서, 동일 부모를 가진 자식들끼리의 정렬 기준을 주는 것이다. 

## Example

|자식id|부모id|CODE|
|-|-|-|
|1|null|A|
|2|1|B|
|3|1|C|
|4|2|D|

```sql
select CODE
from TEMP_TABLE
start with 부모id is null
connect by prior 자식id = 부모id
order sibilings by CODE DESC 
```
### 결과
가장 상위 계층인 A를 먼저 뱉는다<br>그 후 부모 노드가 1인 자식 2,3의 경우 code기반 내림차순으로 C - B 순으로 결과를 뱉는다.
```txt
A
C
B
D
```

