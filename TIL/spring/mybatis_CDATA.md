# 1.Mybatis에서 CDATA 사용

###### CDATA는 태그안에서는 전부 문자열로 치환시켜버리기 때문에 비교연산자, 부등호, 특수문자를 사용가능

###### 하나의 규칙같이 부등호가 없는 쿼리문에도 전부CDATA를 쓰기도 함

###### WHERE 1=1



## 1.CDATA 를 사용한 쿼리

```xml
<SELECT id="findAll" resultMap="MemberResultMap">
<![CDATA[
    SELECT 
  		*
    FROM 
		table
    WHERE
 		column > 100
]]>
</SELECT>
```



## 2. 조건태그에서의 CDATA 

```xml
<SELECT id="findAll" resultMap="MemberResultMap">
    SELECT 
		*
    FROM 
		table
    WHERE  1=1
    <choose>
        <when test='user_type != null and user_type =="1"'>
            <![CDATA[ column1 > 100 ]]>
        </when> 
        <otherwise>
            <![CDATA[ column2 < 100 ]]>
        </otherwise>
    </choose>
    <if test = 'startDate != NULL and startDate != "" '>
		AND	CAST(column3 AS DATETIME) <![CDATA[ >= ]]> #{startDate} + ' 00:00:00'	  
		AND CAST(column3 AS DATETIME) <![CDATA[ <= ]]> #{endDate}   + ' 23:59:59'
	</if>	 
</SELECT>
```

