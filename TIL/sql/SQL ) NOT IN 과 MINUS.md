# DB ) NOT IN 과 MINUS

###### A테이블 에서 서울지역에 위치하고 주변에 공원이 없는 {인덱스, 아이디, 이름, 전화번호}를 선택



###### A테이블에 선택해야 하는 정보가 있고,

###### B테이블에 지역

###### C테이블에 공원 여부가 있다



###### A테이블과 B 테이블 => 인덱스로 연결

###### B테이블과 C테이블 => 지역으로 연결



### MINUS SELECT

```sql
SELECT 
	A.인덱스
	, A.아이디
    , A.이름
    , A.전화번호 
FROM tbl_a A
INNER JOIN tbl_b B on A.인덱스 = B.인덱스
WHERE 1=1
AND B.지역 LIKE '%서울%'
MINUS SELECT
	A.인덱스
	, A.아이디
    , A.이름
    , A.전화번호 
FROM tbl_b B
INNER JOIN tbl_a A ON B.인덱스 = A.인덱스
INNER JOIN tbl_c C on B.지역 = C.지역
WHERE C.편의시설 = '공원';
```

###### Oracle 에서만 지원





### NOT IN 

```sql
SELECT 
	A.인덱스
	, A.아이디
    , A.이름
    , A.전화번호 
FROM tbl_a A
INNER JOIN tbl_b B on A.인덱스 = B.인덱스
WHERE
	B.지역 NOT IN 
		(
          SELECT
            U.user_code                
          FROM tbl_c C
          INNER JOIN tbl_b B ON C.지역 = B.지역
          WHERE C.편의시설 = '공원'
       	 )
AND B.지역 LIKE '%서울%'
```

###### 더 간단하게 모든 RDMS에서 사용가능!