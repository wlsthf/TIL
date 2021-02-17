# mybatis) 배열 컬럼 처리



### mybatis config xml

```xml
<typeAliases>
	<typleAlias alias="dto" type="a.b.c.Dto"/>
</typeAliases>

<typeHandlers>
	<typeHandler handler="a.b.c.CustomTypeHandler" javaType="java.util.ArrayList"/>
</typeHandlers>
```



### mybatis mapper xml

```xml
<resultMap id="customMap" type="dto">
	<result property="field1" column="column1"/>
    <result property="field2" column="column2"/>
    <result property="field3" column="column3" typeHandler="a.b.c.CustomTypeHandler"/>
</resultMap>

<select id="getSomething" resultMap="customMap">
	SELECT
    	column1 as field1
        , column2 as field2
    	, column3 as field3
    FROM tbl
</select>

<insert id="insertSomething" parameterType="dto">
    INSERT INTO tbl
    (
    	column1
    	, column2
    	, column3
    )
    VALUES
    (
    	#{field1}
    	, #{field2}
    	, #{field3, typeHandler=a.b.c.CustomTypeHandler}
    )
</insert>
```



### CustomTypeHandler.java

```java
@MappedTypes(java.util.ArrayList.class)
@MappedJdbcTypes(JdbcType.ARRAY)
public class CustomTypeHandler extends BaseTypeHandler<List<String>> {

    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, List<String> parameter, JdbcType jdbcType) throws SQLException {
        if ( parameter == null || parameter.size() == 0 ) {
            ps.setArray(i, null);
            return;
        }
        
        String[] datum = new String[parameter.size()];
        
        for ( int j = 0; j < parameter.size(); j++ ) {
            datum[j] = parameter.get(j);
        }
        
        ps.setArray(i, ps.getConnection().createArrayOf("varchar", datum));
        
    }

    @Override
    public List<String> getNullableResult(ResultSet rs, String columnName) throws SQLException {
        return getArrayListFromSqlArray(rs.getArray(columnName));
    }

    @Override
    public List<String> getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
        return getArrayListFromSqlArray(rs.getArray(columnIndex));
    }

    @Override
    public List<String> getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
        return getArrayListFromSqlArray(cs.getArray(columnIndex));
    }
    
    private List<String> getArrayListFromSqlArray(Array array) throws SQLException {
        if ( array == null )  return null; 
        
        String[] datum = (String[]) array.getArray();
        
        if ( datum == null ) return null; 
        
        List<String> list = new ArrayList<>();
        
        for ( int i = 0; i < datum.length; i++ ) {
            list.add(datum[i]);
        }
        
        return list;
    }

}
```

