# SQL ) INSERT or UPDATE ( DUPLICATE )



MySQL

```mysql
INSERT INTO 테이블
(
    a
    , b
    , c
)
VALUES
(
	1
    , 2
    , 3
)
ON DUPLICATE KEY UPDATE 
	c = c + 1;
	-- c = 4;
```



PostgreSQL 9.5 이상

```sql
INSERT INTO 테이블
(
    a
    , b
    , c
)
VALUES
(
	1
    , 2
    , 3
)
ON CONFLICT DO UPDATE SET 
	c = 테이블이름.c + 1;
	--  c = 4;
```



case2 

```SQL
INSERT INTO 테이블
VALUSE
(
	2
    , 3
)
ON CONFLICT (PK_column_name) UPDATE SET
	b = 2
    , c = 3;
```

