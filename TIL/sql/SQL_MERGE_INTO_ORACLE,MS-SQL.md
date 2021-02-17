# MERGE INTO - Oracle

###### table에 해당하는 값이 있으면 UPDATE,  없으면 INSERT 해주는 MARGE INTO





#### MARGE INTO

```sql
MERGE INTO table_name 별명
	USING ((table | view | subquery) 별명 | DUAL) 
	ON (join 조건)              
	WHEN MATCHED THEN 
		UPDATE SET 
			컬럼명 = 값             
	WHEN NOT MATCHED THEN 
		INSERT 
			(
            	컬럼명
        	) 
        VALUES 
        	(
            	값
        	);  
```





#### table to table

```sql
MERGE INTO table_name a
	USING table b
	ON (a.컬럼명 = b.컬럼명)
	WHEN MATCHED THEN 
		UPDATE SET 
			a.컬럼명 = b.컬럼명            
	WHEN NOT MATCHED THEN 
		INSERT 
			(
            	a.컬럼명
        	) 
        VALUES 
        	(
            	b.컬럼명
        	);  
```

###### b테이블에서 a테이블로 옮길때 중복되는 것은 빼고 옮긴다.



#### 한 개의 table

```sql
MERGE INTO table_name 
	USING DUAL 
	ON (컬럼명 = 값)
	WHEN MATCHED THEN 
		UPDATE SET 
			컬럼명 = 값
	WHEN NOT MATCHED THEN 
		INSERT 
			(
                컬럼명
            ) 
        VALUES 
        	(
                값
            );  
```





#### view to table

```sql
MERGE INTO 테이블명 a
	USING 
		(
    		SELECT 
        		컬럼명
        		, 컬럼명2
       		FROM DUAL	--비교 대상이 같을 경우
    	) b
    ON 
    	(
            a.컬럼명 = b.컬럼명
       		AND a.컬럼명2 = b.컬럼명2 
        )
    WHEN MATCHED THEN
    	UPDATE SET
    		a.컬럼명 = b.컬럼명
    WHEN NOT MATCHED THEN 
    	INSERT 
    		(
            	a.컬럼명
        	)
        VALUES 
        	(
        		b.컬럼명
        	);    	
```



##### *Oracle 10g 이후

###### 	WHEN MATCHED THEN 이하 UPDATE, INSERT, DELETE 구문에도 WHERE 절 사용가능

###### 	UPDATE 대신 DELETE 사용가능



##### *불필요하게 MERGE INTO를 남발 하면 쿼리의 성능이 느려질 수 있다.



#### *특정 DBMS에서만 작동하기 때문에 그냥 확인하고 인서트 혹은 업데이트 