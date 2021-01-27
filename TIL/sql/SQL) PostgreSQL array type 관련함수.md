# SQL) PostgreSQL array type 관련함수



```sql
-- 데이터를 각 로우로 변경
unnest(arr)

-- array 타입끼리 합치기
array_cat(arr1, arr2)

-- array 에서 string(1개 row)로 변경
array_to_string(arr, '구분자', 'null값 대체 구분자')

-- string을 array로 변경
string_to_array(string, '구분자', 'null로 변경할 값')

-- row들을 array로 합치기
array_agg(col)

-- ex) 
WITH tmp as (
	SELECT col1, UNNEST(col2) AS col2 FROM table
)
 SELECT col1, ARRAY_AGG(col2) AS col2 
 FROM tmp 
 GROUP BY col1;
 
 -- 중복제거, 정렬
 array_agg(DISTINCT col2 ORDER BY col2)
	
```

