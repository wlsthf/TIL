# SQL_PostgreSQL 배열 부분 update



```sql
SELECT * FROM 테이블;
--컬럼1 | 컬럼2 |
------/------/
--1 | {1,2,3}|

UPDATE 테이블
SET 컬럼2[2] = 0
WHERE 컬럼1 = 1;

SELECT * FROM 테이블;
--컬럼1 | 컬럼2 |
------/------/
--1 | {1,0,3}|

```

