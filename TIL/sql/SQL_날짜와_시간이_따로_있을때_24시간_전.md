## SQL ) 날짜와 시간이 따로 있을때 24시간 전

```sql
SELECT *
FROM 테이블
WHERE
		( date = #{date} AND time > #{time} )
	OR ( date > #{date} AND time <= #{time} )
```

