# Mybatis - isEqual

```xml
<isNotEmpty property="check_type" prepend="and">
	<isEqual property="check_type" compareValue="이름">
		이름 LIKE '%$이름$%'
		AND 전화번호 = #전화번호#
	</isEqual>
	<isEqual property="check_type" compareValue="아이디">
		아이디 = #아이디#
	</isEqual>
</isNotEmpty>
```

