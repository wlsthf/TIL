# mapper

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
   PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
   "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="CRUD">
    
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
			<if test="col_3 != null and col_3 != ''">
				, col_3
			</if>
		)
		VALUES
		(
			<if test="idx != null and idx != ''">
				#{idx},
			</if>
			#{col_1}
			<if test="col_3 != null and col_3 != ''">
				, #{col_2}
			</if>
			<if test="col_4 != null and col_4 != ''">
				, #{col_3}
			</if>			
		);
		
		<selectKey keyProperty="idx" resultType="String" order="BEFORE">
   			SELECT MAX(idx) 
   			FROM tbl_2
  		</selectKey>	
  		
	</insert>
    
	<select id="tableSelect" parameterType="caseMap" resultType="caseMap">
		SELECT 
			idx
			, col_1
			, col_2
			, col_3
		FROM tbl
		ORDER BY idx;			
	</select>    
    
    <update id="localCivilComplaintPopupModify" parameterType="caseMap">
		UPDATE tbl_mdata_record_DATA
		<set><if test="column_name == 'col_0'">col_0 = #{data}</if></set>
		<set><if test="column_name == 'col_2'">col_2 = #{data}</if></set>
		<set><if test="column_name == 'col_3'">col_3 = #{data}</if></set>
		<set><if test="column_name == 'col_4'">col_4 = #{data}</if></set>
		<set><if test="column_name == 'col_5'">col_5 = #{data}</if></set>
		<set><if test="column_name == 'col_6'">col_6 = #{data}</if></set>		
		WHERE idx = #{idx};
	</update>
    
    <update id="tableDelete" parameterType="caseMap">
		DELETE 
		FROM tbl
		WHERE idx = #{idx}
	</update>   
	
</mapper>
```

