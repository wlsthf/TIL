# SQL)  join 정리



```sql
-- A에만 있는 자료 찾기 
SELECT 컬럼 
FROM 테이블1 A
LEFT JOIN 테이블2 B ON B.컬럼 = A.컬럼
WHERE B.컬럼 IS NULL

-- B에만 있는 자료 찾기 
SELECT 컬럼 
FROM 테이블1 A
RIGHT JOIN 테이블2 B ON B.컬럼 = A.컬럼
WHERE A.컬럼 IS NULL

-- A + B 
SELECT 컬럼 
FROM 테이블1 A
FULL OUTER JOIN 테이블2 B ON B.컬럼 = A.컬럼

-- A + B 에서 교집합을 제외한 자료 찾기
SELECT 컬럼 
FROM 테이블1 A
FULL OUTER JOIN 테이블2 B ON B.컬럼 = A.컬럼
WHERE A.컬럼 IS NULL
OR B.컬럼 IS NULL

-- A 와 B 둘 다 있는 자료 찾기 
SELECT 컬럼 
FROM 테이블1 A
INNER JOIN 테이블2 B ON B.컬럼 = A.컬럼
```

