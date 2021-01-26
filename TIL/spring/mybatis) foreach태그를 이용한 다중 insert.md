# mybatis) foreach태그를 이용한 다중 insert

```xml
<insert id="인서트쿼리" parameterType="java.util.Map">
    INSERT INTO 테이블명
    (
    	컬럼1
    	, 컬럼2
    )
    VALUES
    <foreach collection="list" item="item" separator=" , ">
    (
    	#{item.컬럼1}
        , #{item.컬럼2}
    )
    </foreach>
</insert>
```



- ###### collection : parameterType으로 넘어온 map의 키값

- ###### seperator : 반복 문자열을 구분할 문자



### 대량 다중 인서트 할 때!!!

```sql
<insert id="인서트쿼리" parameterType="java.util.Map">
    INSERT INTO 테이블명
    VALUES
    <foreach collection="list" item="item" separator=" , ">
    (
    	#{item.컬럼1}
        , #{item.컬럼2}
    )
    </foreach>
</insert>
```

이렇게 컬럼명 빼면 훨 씬 빠르다 (  preparedstatement 안하고 바로 해서 그런듯.. 알아봐야함 )