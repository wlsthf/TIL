# SQL - Case 표현식

#### 하나의 컬럼에 대해서 조건에 따른 컬럼의 결과를 변환



#### CASE 두 개

```sql
SELECT
    CASE
    	WHEN 컬럼명 = '값1' THEN '결과값1'
    	ELSE '결과값2'
    END AS 별명2
FROM 테이블명 		
```



#### CASE 세 개

```sql
SELECT
    CASE 컬럼명
    	WHEN '값1' THEN '결과값1'
    	WHEN '값2' THEN '결과값2'
    	WHEN '값3' THEN '결과값3'
    END AS 별명2
FROM 테이블명	
```

###### * 컬럼명 CASE 뒤에 사용 가능



#### CASE 네 개

```sql
SELECT
    CASE 컬럼명
    	WHEN '값1' THEN '결과값1'
    	WHEN '값2' THEN '결과값2'
    	WHEN '값3' THEN '결과값3'
    	ELSE '결과값4'
    END AS 별명2
FROM 테이블명 
```

###### * ELSE 사용 지향



#### AND가 들어간 CASE

```sql
SELECT
    CASE
    	WHEN 컬럼명1 = '값1' AND 컬럼명2 = '값A' THEN '결과값1'
    	WHEN 컬럼명1 = '값2' AND 컬럼명2 = '값B' THEN '결과값2'
    	WHEN 컬럼명1 = '값3' AND 컬럼명2 = '값C' THEN '결과값3'
    	ELSE '결과값4'
    END AS 별명2
FROM 테이블명 	
```

###### * WHEN 절에 OR도 사용 가능

