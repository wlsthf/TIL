# DUPLICATE - MySQL

###### 데이터가 없으면 INSERT, 있으면 UPDATE ( MERGE INTO와 비슷한 기능 )



#### ON DUPLICATE KEY

```sql
INSERT INTO 테이블명 
	(
    	컬럼명
	)
VALUES 
	(
    	값
	)
ON DUPLICATE KEY
UPDATE 
	컬럼명 = 값;
```





#### 여러개의 데이터를 입력

```sql
INSERT INTO 테이블명 
	(
    	컬럼명
    	, 컬럼명2
	)
VALUES 
	(
    	값
    	, 값2
	)
ON DUPLICATE KEY
UPDATE 컬럼명 = 값;
```

