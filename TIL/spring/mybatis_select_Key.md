# select Key 

### selectKey

```xml
	<selectKey keyProperty="idx" resultType="String" order="BEFORE">
        SELECT MAX(idx) 
        FROM tbl_2
  	</selectKey>
```

##### INSERT 하기 전후 사용 가능하며  mybatis의 xml문서에서 insert 태그 안에 위치한다. 

- ###### 	keyProperty => 이름

- ###### 	resultType => type

- ###### 	order => 순서 (BEFORE, AFTER)

  

```xml
	<selectKey keyProperty="idx" resultType="String" order="BEFORE">
        SELECT 
        	MAX(idx) + 1
        FROM tbl_2
  	</selectKey>
```

###### 위와같이 조작도 가능.



### selectKey(before)

```xml
	<insert id="tableRecord" parameterType="caseMap">
		INSERT INTO 
			tbl_2 (reg_date)        
		VALUES (now());
	</insert>
    
    <insert id="tableRegist" parameterType="caseMap">
		INSERT INTO tbl (
			<if test="idx != null and idx != ''">
				idx,
			</if>
				col_
        	<if test="col_2 != null and col_2 != ''">
				, col_2
			</if>	
		)
		VALUES
		(
			<if test="idx != null and idx != ''">
				#{idx},
			</if>
				#{col_1}
			<if test="col_2 != null and col_2 != ''">
				, #{col_2}
			</if>		
		);
		
		<selectKey keyProperty="idx" resultType="String" order="BEFORE">
   			SELECT MAX(idx) 
   			FROM tbl_2
  		</selectKey>	
  		
	</insert>
```

###### INSERT 하기 전에 tbl_2에서 idx를 가져온다.





### 후

```xml
	<insert id="tableRecord" parameterType="caseMap">
		INSERT INTO 
			tbl_2 (reg_date)        
		VALUES (now());
        
        <selectKey keyProperty="idx" resultType="String" order="AFTER">
   			SELECT MAX(idx) 
   			FROM tbl_2
  		</selectKey>
	</insert>
    
    <insert id="tableRegist" parameterType="caseMap">
		INSERT INTO tbl (
			<if test="idx != null and idx != ''">
				idx,
			</if>
				col_
        	<if test="col_2 != null and col_2 != ''">
				, col_2
			</if>	
		)
		VALUES
		(
			<if test="idx != null and idx != ''">
				#{idx},
			</if>
				#{col_1}
			<if test="col_2 != null and col_2 != ''">
				, #{col_2}
			</if>		
		);			
  		
	</insert>
```

###### INSERT 하고나서 가져온다. 





###### ** mybatis에서 if문사용시 , 사용에 유의한다!! 

```xml
    <if test="idx != null and idx != ''">
   		#{idx},
    </if>
   	 	#{col_1}
    <if test="col_2 != null and col_2 != ''">
    	, #{col_2}
    </if>	
```

