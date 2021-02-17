# SQL) GROUP BY 로 묶었을 때 갯수 세기



mysql..

```sql
SELECT 
	COUNT(*) AS cnt 
FROM 
(
	SELECT 
		A.idx AS idx 
	FROM 테이블 A 
	INNER JOIN 테이블 B ON A.idx = B.idx 
	GROUP BY A.어떤거
) AS C
```



별명을 다 줘야함!