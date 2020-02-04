# mapper

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
   PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
   "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="civilComplaintData">
<sql id="reg_getCivilComplaintListSearch">
		<!-- <if test = "type2 != NULL and type2 != ''"> AND a.inactive_flag = ${type2}</if> -->

	  	<if test = "searchKeyword != NULL and searchKeyword != '' ">
			AND a.service_name like '%' || #{searchKeyword} || '%'
		</if>
		
	</sql>

<select id="localCivilComplaintPopup" parameterType="caseMap" resultType="caseMap">
		SELECT 
			a.record_id
			, a.row_no 
			, a.col_0
			, (SELECT cv_name FROM tbl_mdata_cd_value WHERE cd_code = 'ISCD' AND cv_value = a.col_0) AS local_name
			, a.col_2
			, (SELECT cv_name FROM tbl_mdata_cd_value WHERE cd_code = 'SUB_ISCD' AND cv_value = a.col_2) AS local_office_name
			, a.col_3
			, a.col_4
			, a.col_5
			, a.col_6
		FROM tbl_mdata_record_DATA a  	
		INNER JOIN tbl_mdata_record b ON a.record_id = b.record_id
		WHERE b.dset_code = 'MWON_MW_0001DS'
		AND b.rset_code = '02RS'
		AND b.record_yyyy = 2019
		AND b.record_mm = 12
		ORDER BY a.row_no;			
	</select>

    
    	<update id="localCivilComplaintPopupDelete" parameterType="caseMap">
		delete 
		from tbl_mdata_record_DATA
		where  record_id = #{record_id}
		and row_no = #{row_no};
	</update>
    
    	<insert id="localCivilComplaintPopupRecord" parameterType="caseMap">
		INSERT INTO 
			tbl_mdata_record(
				dset_code
				,rset_code
				,record_yyyy
				,record_mm
				,reg_date
				,log_flag) 
		VALUES(
			'MWON_MW_0001DS'
			,'02RS'
			,2019
			,12
			,now()
			,0);
	</insert>
    
    <insert id="localCivilComplaintPopupRegist" parameterType="caseMap">
		INSERT INTO tbl_mdata_record_DATA (
			<if test="record_id != null and record_id != ''">
				record_id,
			</if>
			row_no,
			col_0
			, col_2
			<if test="col_3 != null and col_3 != ''">
				, col_3
			</if>
			<if test="col_4 != null and col_4 != ''">
				, col_4
			</if>
			<if test="col_5 != null and col_5 != ''">
				, col_5
			</if>
			<if test="col_6 != null and col_6 != ''">
				, col_6
			</if>			
		)
		VALUES
		(
			<if test="record_id != null and record_id != ''">
				#{record_id},
			</if>
			#{row_no},
			#{col_0}
			, #{col_2}
			<if test="col_3 != null and col_3 != ''">
				, #{col_3}
			</if>
			<if test="col_4 != null and col_4 != ''">
				, #{col_4}
			</if>
			<if test="col_5 != null and col_5 != ''">
				, #{col_5}
			</if>
			<if test="col_6 != null and col_6 != ''">
				, #{col_6}
			</if>
			
		);
		
		<selectKey keyProperty="record_id" resultType="String" order="BEFORE">
   			SELECT MAX(record_id) 
   			FROM tbl_mdata_record 
   			WHERE 1=1   			 
			AND 
				dset_code = 'MWON_MW_0001DS'
			AND
				rset_code = '02RS'
			AND 
				record_yyyy = 2019
			AND
				record_mm = 12;
  		</selectKey>	
  		
	</insert>
    
    
    <update id="localCivilComplaintPopupModify" parameterType="caseMap">
		UPDATE tbl_mdata_record_DATA
		<set><if test="column_name == 'col_0'">col_0 = #{data}</if></set>
		<set><if test="column_name == 'col_2'">col_2 = #{data}</if></set>
		<set><if test="column_name == 'col_3'">col_3 = #{data}</if></set>
		<set><if test="column_name == 'col_4'">col_4 = #{data}</if></set>
		<set><if test="column_name == 'col_5'">col_5 = #{data}</if></set>
		<set><if test="column_name == 'col_6'">col_6 = #{data}</if></set>		
		WHERE row_no = #{row_no}
		AND record_id = #{record_id};
	</update>
	
	<select id="localCivilComplaintPopupSelectBox" parameterType="caseMap" resultType="caseMap">
		SELECT cv_value, cv_name, cv_abbr, cv_note
		FROM tbl_mdata_cd_value
		WHERE cd_code = 'SUB_ISCD' 
		AND SUBSTRING(cv_value, 0, 2) = SUBSTRING(#{local_name}, 0, 2)		
	</select>
</mapper>
```

