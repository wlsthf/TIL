# SQL_case count & distinct



```sql
SELECT 
	COUNT(CASE WHEN 컬럼='1번' THEN 1 END) AS '1번'
	, COUNT(CASE WHEN 컬럼='2번' THEN 1 END) AS '2번'
	, COUNT(CASE WHEN 컬럼='3번' THEN 1 END) AS '3번' 
FROM 테이블
--|1번|2번|3번|
--------------
--| 5 | 4 | 3 |
```





```sql
SELECT 
	번호
	, COUNT(*) AS '개수' 
FROM 테이블 GROUP BY 번호

--|번호|개수|
------------
--| 1 | 5  |
--| 2 | 4  |
--| 3 | 3  |
```





```sql
SELECT 
	번호
	, COUNT(*) AS '중복포함' 
	, COUNT(DISTINCT 이름) AS '중복제거' 
FROM 테이블 
GROUP BY 번호

--|번호|중복포함|중복제거|
-----------------------
--| 1 |   5    |   6   |
--| 2 |   4    |   7   |
--| 3 |   3    |   8   |
```