#  Database

### 1.DDL (Data Definition Language)

#### 1. 데이터 유형

|    MySQL    |    ORACLE     |      MS-SQL       |
| :---------: | :-----------: | :---------------: |
|   INT(11)   |  NUMBER(11)   |       FLOAT       |
| VARCHAR(30) | VARCHAR2(30)  |    VERCHAR(30)    |
|  CHAR(30)   |   CHAR(30)    |  CHAR([1-2000])   |
|   TINYINT   |   NUMBER(3)   |                   |
|     INT     |  NUMBER(10)   |    NUMERIC(38)    |
|   INTEGER   |  NUMBER(10)   |                   |
|   BIGINT    |  NUMBER(20)   |                   |
|   DOUBLE    | NUMBER(10,5)  |                   |
|    BLOB     |   BLOB,RAW    |  VARBINARY(MAX)   |
|    DATE     |     DATE      |     DATETIME      |
|  DATETIME   |     DATE      |     DATETIME      |
|   DECIMAL   |   FLOAT(24)   |  NUMERIC([1-38])  |
|   DOUBLE    |   FLOAT(24)   |  NUMERIC([1-38])  |
|    FLOAT    |     FLOAT     |       FLOAT       |
|   LONTEXT   |   CLOB,RAW    |   VARCHAR(MAX)    |
|   NUMERIC   |    NUMBER     |       FLOAT       |
|    REAL     |   FLOAT(24)   |  NUMERIC([1-38])  |
|     SET     |   VARCHAR2    | VARCHAR([1-4000]) |
|    TEXT     | VARCHAR2,CLOB | VARCHAR([1-4000]) |
|    TIME     |     DATE      |     DATETIME      |
|  TIMESTAMP  |     DATE      |     DATETIME      |
|  TINYBLOB   |      RAW      |                   |
|  TINYTEXT   |   VARCHAR2    | VARCHAR([1-4000]) |
|    YEAR     |    NUMBER     |                   |



###### 제약조건

```sql
PRIMARY KEY - 기본키 NULL 불가능
FOREIGN KEY - 외래키 (참조 테이블에 값이 있어야 select, update가능, 값이 없어야 delete 가능)
UNIQUE KEY  - 데이터의 유일성을 보장(중복되는 데이터가 존재할수 없다) n자동으로 인덱스가 생성 된다. 			  Null 허용
NOT NULL    - 빈 값 불가능
CHECK   	- 컬럼 값을 특정 범위로 제한
```

###### 사용 예

```sql
CONSTRAINT [제약조건명] PRIMARY KEY ( [컬럼명]);

CONSTRAINT [제약조건명] FOREIGN KEY ( [컬럼명] ) REFERENCES [참조테이블] ( [참조할 열] );

CONSTRAINT [제약조건명] UNIQUE( [컬럼명] );

조건1, 조건2, 조건3 만 입력가능
CONSTRAINT [제약조건명] CHECK ( [컬럼명] IN( [조건1],[조건2],[조건3] );

1보다 같거나 크거가 100보다 같거나 작은 경우
CONSTRAINT [제약조건명] CHECK ( [컬럼명] >= 1 AND [컬럼명] <= 100);

ORACLE 에서는 BOOLEAN형이 없기 때문에 CHECK조건 IN(1,0)을 이용
```



#### 2. CREATE TABLE(테이블 생성)

```sql
CREATE TABLE [테이블명](
    [컬럼명1] [데이터 타입] [DEFAULT 형식]
    ,[컬럼명2] [데이터 타입] [DEFAULT 형식]
); 
```



```sql
DESC 테이블명 - ORACLE에서 테이블 구조 확인
ORACLE은 시퀀스 생성해서 넣어야 하고 MYSQL은 AUTO INCREASING 사용
```



CTAS(Create Table ~ As Select ~ ) - 테이블 복제

```sql
CREATE TABLE [새로운 테이블명] 
AS SELECT * FROM [복제할 테이블명];

* NOT NULL만 복제 테이블에 적용되고, 기본키, 고유키, 외래키, CHECK등의 다른 제약조건은 없어짐
```





#### 3. ALTER TABLE(테이블 변경)

###### 	1. ADD COLUMN (컬럼 추가)

​	`	ALTER TABLE [테이블명] ADD [추가할 컬럼명] [데이터 유형];`



###### 	2. DROP COLUMN (컬럼 삭제)

​	`ALTER TABLE [테이블명] DROP COLUMN [삭제할 컬럼명] `;



###### 	3. MODIFY COLUMN (컬럼 수정)

​	`ALTER TABLE [테이블명] `

​	`MODIFY (컬럼명1 데이터유형 [DEFAULT 식], 컬럼명2 데이터유형..);`



###### 	4. RENAME COLUMN(컬럼명 수정)

​	`ALTER TABLE [테이블명] RENAME COLUMN [변경해야 할 컬럼명] TO [새로운 컬럼명];`



###### 	5. DROP CONSTRAINT(제약조건 삭제)

​	`ALTER TABLE [테이블명] DROP CONSTRAINT [제약조건명];`



###### 	6. ADD CONSTRAINT(제약조건 추가)

​	`ALTER TABLE [테이블명] ADD CONSTAINT [제약조건명] [제약조건] ( [컬럼명] )`;





#### 4. RENAME TABLE(테이블명 변경)

```sql
RENAME [변경전 테이블명] TO [변경후 테이블명];
```



#### 5. DROP TABLE(테이블 삭제)

```sql
DROP TABLE [테이블명] [CASCADE CONSTRANINT];
* 해당 테이블에 참조되는 제약조건에 대해서도 삭제
```



#### 6. TRUNCATE TABLE(테이블 비우기)

```sql
TRUNCATE TABLE [테이블명];
* 테이블에 들어있던 모든 행들이 제거되고 저장 공간을 재사용 가능하도록 해제
```





### 2.DML( Data Manipulation Language)



#### 1. INSERT

```sql
INSERT INTO 
    [테이블명] 
        (
            [컬럼 이름]
            ,[컬럼 이름]
        ) 
VALUES
	(
		'문자'
		,숫자
	);
	
	
INSERT INTO 
	[테이블명] 
VALUES 
	(
		'값'
		,값
	);

* SELECT해서 INSERT 하기
INSET INTO 
	[테이블명]
SELECT 
	* 
FROM 
	[테이블명]; 

```





#### 2. UPDATE

```sql
UPDATE 
    [테이블명] 
SET 
	[컬럼명] = [값]
	,[컬럼명] = [값]
WHERE
	[바꿀 값을 찾을 컬럼명] = [값];
```

###### WHERE 절이 없으면 그 컬럼의 값을 변경





#### 3. DELETE

```sql
DELETE FROM 
	[테이블명] 
WHERE 
	[컬럼명] = [값]; 
```

###### WHERE 절이 없으면 테이블의 데이터 전부를 삭제



#### 4. SELECT

```sql
SELECT [ALL/DISTINCT] 
	[컬럼명]
	,[컬럼명]
	... 
FROM 
	[테이블명];
 	
 	
 	ALL 	 : 중복된 데이터 표시, Default 옵션
 	DISTINCT : 중복된 데이터 1건으로 표시 

	WILDCARD : SELECT * FROM [테이블명]
```

###### ALIAS (별명)

```sql
SELECT
	[컬럼명] AS [별명]
	,[컬럼명] AS [별명]
FROM 
	[테이블명]
```



#### 5. 산술 연산자와 합성 연산자

##### Java와 동일..

###### 산술연산

```sql
SELECET 
	[컬럼명] AS [별명]
	,ROUND([컬럼명](([컬럼명]/100)*([컬럼명]/100)),2) AS " [결과 별명] " 
FROM 
	[테이블명]
```









###### 합성

```sql
SELECET 
	[컬럼명]||' [추가단어], ' || [컬럼명] ||' [추가단어] ' AS " [결과 별명] "
FROM 
	[테이블명]
```



### 3. GROUP 함수

#### count, max, min, avg



##### ex) CAR  TABLE



#### 1. 회사별 차량수

```sql
SELECT 
    corp
    ,COUNT(*) AS cnt
FROM
    CAR
GROUP BY
    corp;
```



#### 2. 회사, 연료기준으로 몇 대씩 있는지

```sql
SELECT 
    corp
    ,fuel
   ,COUNT(*) AS cnt
FROM 
    CAR
GROUP BY
   [컬럼명1]
   [컬럼명2];
```









#### 3. 회사, 연료기준으로 몇 대씩 있는지 -> 가장 낮은 가격

```sql
SELECT
    corp
    ,fuel
    ,COUNT(*) AS cnt
    ,MIN(price) AS minPrice
FROM
    CAR
GROUP BY
    corp
    ,fuel;
```

###### GROUP BY ->  SELECT 같아야 하고, 그룹함수만 올 수 있음. 그룹함수는 GROUP BY를 쓰지 않아도 사용가능. 



### 4.많이 쓰이는 JOIN

INNER JOIN, LEFT OUTER JOIN



##### CONTENT TABLE





##### CONTENT_COMMENT  TABLE





#### 1. INNER JOIN

###### 두 테이블의 중복되는 자료를 찾아야할 때

```sql
SELECT 
    a.content_idx, b.contents
FROM 
    CONTENT a
INNER JOIN 
    CONTENT_COMMENT b ON a.content_idx = b.content_idx
ORDER BY 
    a.content_idx;
```

#### 2. LEFT OUTER JOIN

###### 두 테이블의 중복자료와 중복 되지 않는 기준테이블의 자료까지 찾아야할 때

```sql
SELECT 
    a.content
    ,b.contents
FROM 
    CONTENT a
LEFT OUTER JOIN 
    CONTENT_COMMENT b ON a.content_idx = b.content_idx
ORDER BY 
    a.content_idx;
```

#### 3. 게시글 제목과 댓글 개수

```sql
SELECT 
     a.content_idx
     ,a.content
     ,COUNT(b.content_idx) AS cnt
FROM 
    CONTENT a
LEFT OUTER JOIN 
    CONTENT_COMMENT b ON a.content_idx = b.content_idx
GROUP BY 
    a.content_idx, a.content;
```

#### 4. 안 좋은 방법

```sql
SELECT a.content_idx, a.content, COUNT(b.content_idx) AS cnt
FROM CONTENT a, CONTENT_COMMENT b
WHERE a.content_idx = b.content_idx(+)
GROUP BY a.content_idx, a.content;       
```

#### 5. 다른 방법

```sql
SELECT
     a.content_idx
     ,a.content
     ,(
           SELECT COUNT(*) 
           FROM CONTENT_COMMENT 
           WHERE content_idx = a.content_idx 
      ) AS cnt       
FROM 
    CONTENT a;
```

######  *  WHERE 절에서 data가 여러개 이면 in으로 감싸주기           







UNION, INTERSECT, EXECPT