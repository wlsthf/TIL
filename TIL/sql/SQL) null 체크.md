# SQL) null 체크

```sql
-- ORACLE
NVL(컬럼명, 0)
-- SQL Server
IFNULL(컬럼명, 0)
-- 표준 SQL
COALESCE(컬럼명, 0)

-- 다른 컬럼도 가능 
COALESCE(컬럼1, 컬럼2)
```

